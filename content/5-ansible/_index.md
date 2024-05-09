---
title : "Write Ansible Playbook"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

First, let's create the Ansible directory structure as shown below.

```shell
$ tree
.
├── ansible
│   ├── ansible-playbook-wordpress-nginx
│   │   ├── README.md
│   │   ├── group_vars
│   │   │   └── all
│   │   ├── hosts
│   │   ├── playbook.retry
│   │   ├── playbook.yml
│   │   └── roles
│   │       ├── nginx
│   │       │   ├── handlers
│   │       │   │   └── main.yml
│   │       │   ├── tasks
│   │       │   │   └── main.yml
│   │       │   └── templates
│   │       │       ├── default-site.conf
│   │       │       └── nginx-wp-common.conf
│   │       ├── php
│   │       │   ├── handlers
│   │       │   │   └── main.yml
│   │       │   └── tasks
│   │       │       └── main.yml
│   │       └── wordpress
│   │           ├── README.md
│   │           ├── handlers
│   │           │   └── main.yml
│   │           ├── tasks
│   │           │   └── main.yml
│   │           └── templates
│   │               └── wp-config.php
```

In the group_vars/all, enter the following content:

```shell
## group_vars/all

# WordPress database settings
wp_db_name: wordpress
wp_db_user: wordpress
wp_db_password: wordpress_db_password

mysql_port: 3306
mysql_root_password: root

auto_up_disable: true

server_hostname: 11thfeb

# WordPress Version
wp_version: 4.7.5
wp_sha1sum: fbe0ee1d9010265be200fe50b86f341587187302

#Define Core Update Level
#true  = Development, minor, and major updates are all enabled
#false = Development, minor, and major updates are all disabled
#minor = Minor updates are enabled, development, and major updates are disabled
core_update_level: true
```

In the host, enter the following content:

```shell
[webservers]
localhost
```

In the playbook.retry, enter the following content:

```shell
localhost
```

In the playbook.yml, enter the following content:

```yml
- hosts: localhost

  roles:
    - nginx
    - wordpress
    - php
```

Ansible Roles **provide a structured way to organize tasks, templates, files, and variables**. This structure makes it easier to manage complex automation setups, as everything related to a specific role is contained within its directory.

In the roles/nginx folder, let’s get start write configure for task and handlers.

Create a file main.yml in roles/nginx/handlers:

```yml
---
- name: restart nginx
  service: name=nginx state=restarted
  become: yes
```

Create a file main.yml in roles/nginx/tasks:

```yml
---
# tasks file for nginx

- name: Update apt cache
  apt: update_cache=yes cache_valid_time=3600
  become: yes

- name: Install nginx
  apt: name={{ item }} state=present
  become: yes
  with_items:
    - nginx
    - git

- name: Start nginx
  become: yes
  service:
    name: nginx
    state: started

- name: Update nginx confs for WordPress + PHP
  template: "src=../templates/default-site.conf dest=/etc/nginx/sites-available/default owner=www-data group=www-data mode=0644"
  become: yes

- name: Enable site
  file: src=/etc/nginx/sites-available/default dest=/etc/nginx/sites-enabled/default owner=www-data group=www-data state=link
  notify:
    - restart nginx
  become: yes
```

You need to create two file in roles/nginx/templates:

- default-site.conf

```nginx
server {
  listen 80 default_server;
  listen [::]:80 default_server;

  root /var/www/11thfeb;

  # Add index.php to the list if you are using PHP
  index index.html index.nginx-debian.html readme.html;

  server_name _;

  location / {
    # First attempt to serve request as file, then
    # as directory, then fall back to displaying a 404.
    #try_files $uri $uri/ =404;
    try_files $uri $uri/ /index.php$is_args$args;
  }

  # include /etc/nginx/nginx-wp-common.conf;
}
```

- nginx-wp-common.conf

```nginx
charset utf-8;

location / {
  index index.php index.html readme.html;
  try_files $uri $uri/ /index.php?$args;
}

error_page 404 /404.html;
error_page 500 502 503 504 /50x.html;

location = /50x.html {
  root /usr/share/nginx/html;
}

# Disallow .php files in uploads
location ~* /(?:uploads|files)/.*\.php$ {
  deny all;
}

# Add trailing slash to */wp-admin requests
rewrite /wp-admin$ $scheme://$host$uri/ permanent;

# Prevent hidden files (beginning with a period) from being served
location ~ /\. {
  access_log off;
  log_not_found off;
  deny all;
}

# Pass uploaded files to wp-includes/ms-files.php
rewrite /files/$ /index.php last;

if ($uri !~ wp-content/plugins) {
  rewrite /files/(.+)$ /wp-includes/ms-files.php?file=$1 last;
}

# Rewrite multisite in a subdirectory '.../wp-.*' and '.../*.php'
if (!-e $request_filename) {
  rewrite ^/[_0-9a-zA-Z-]+(/wp-.*) $1 last;
  rewrite ^/[_0-9a-zA-Z-]+.*(/wp-admin/.*\.php)$ $1 last;
  rewrite ^/[_0-9a-zA-Z-]+(/.*\.php)$ $1 last;
}

location ~ \.php$ {
  try_files $uri =404;
  include /etc/nginx/fastcgi_params;
  fastcgi_read_timeout 3600s;
  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
  fastcgi_pass unix:/run/php/php7.0-fpm.sock;
  fastcgi_split_path_info ^(.+\.php)(/.+)$;
  fastcgi_index index.php;
}
```

Continue configuration to download and install wordpress.

Create a file main.yml in roles/wordpress/handlers:

```yml
---
- name: restart nginx
  service: name=nginx state=restarted
  become: yes

- name: restart php5-fpm
  service: name=php5-fpm state=restarted
```

Continue configuration to download and install PHP.

Create a file main.yml in roles/php/handlers:

```yml
---
- name: restart nginx
  service: name=nginx state=restarted
  become: yes
```

Create a file main.yml in roles/php/tasks:

```yml
---
# tasks file for php
- name: Update apt cache
  apt: update_cache=yes cache_valid_time=3600
  become: yes

- name: Add ppa Repository
  become: yes
  apt_repository: repo=ppa:ondrej/php

- name: Install php extensions
  apt:
    name: "{{ item }}"
    state: latest
  become: yes
  with_items:
    - php7.0
    - php7.0-mysql
    - php7.0-gd
    - php7.0-mcrypt

- name: Setup php-fpm
  replace: dest=/etc/php/7.0/cli/php.ini regexp="(;cgi.fix_pathinfo=1)" replace="cgi.fix_pathinfo=0"
  notify:
    - restart nginx
  become: yes

- name: Add php settings
  template: src=../../nginx/templates/nginx-wp-common.conf dest=/etc/nginx/nginx-wp-common.conf owner=www-data group=www-data mode=0644
  notify:
    - restart nginx
  become: yes

- name: Remove apache2
  become: true
  apt:
    name: apache2
    state: absent
```
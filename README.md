# PHP App Environment Builder via Docker Compose

Quickly setup your PHP Web Application environment using Docker Compose

- Choose your PHP version (default latest PHP7) Tested on v5.6, v7.0, v7.1, v7.2, v7.3, and v7.4
- Choose between Apache or Nginx as your web server
- Choose between MariaDB and MySQL sa your DBMS

Best for testing your PHP web application on a variety of environments.

## Requirements

- Docker Compose - https://docs.docker.com/compose/install/

## Installation

The following will build the latest versions of PHP7, Apache, and MariaDB. Once up, you may access your web application at localhost:8080

```sh
wget https://github.com/easterncoder/php-app-docker/archive/master.zip
unzip master.zip
cd php-app-docker-master
docker-compose build --build-arg HOST_UID=$(id -u)
docker-compose up -d
```

You may access the web server at:

- localhost:8080
- localhost:8080/phpinfo.php
- localhost:8080/adminer.php

Note: `--build-arg HOST_UID` is required in order set file permissions for the `app/web` folder

## File Paths

- `app/web` - PHP Files (Put your PHP app here)
- `app/db` - Database Data (This is where database files are stored)

## Default Database Credentials

- HOST: **database_server**
- USER: **root**
- PASS: **root**

## To start the services of an existing build

```sh
docker-compose up -d
```

## To stop the services
```sh
docker-compose stop
```

## Build Options

Build options are specified by passing --build-arg FOO=BAR for each argument you want to pass. Available build arguments are:

Host UID (required)
- `HOST_UID`=num\
Example 1: to set the current user's UID `--build-arg HOST_UID=$(id -u)`
Example 2: to set a specific UID `--build-arg HOST_UID=1001`

Web Servers:
- `WEB`=**httpd** | nginx
- `WEB_VERSION`=**latest** | num

Database Management System:
- `DB`=**mariadb** | mysql
- `DB_VERSION`=**latest** | num

PHP
- `PHP_VERSION`=**7** | 7.4 | 7.3 | 7.2 | 7.1 | 7.0 | 5.6

To build PHP 5.6, Nginx (latest) and MySQL 5.6, the build command would be:

```sh
docker-compose build --build-arg HOST_UID=$(id -u) \
 --build-arg PHP_VERSION=5.6 \
 --build-arg DB=mysql \
 --build-arg DB_VERSION=5.6 \
 --build-arg WEB=nginx
 ```



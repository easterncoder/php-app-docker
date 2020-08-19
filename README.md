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

Note: `--build-arg HOST_UID` is required in order set file permissions for the `app/web` folder

You may access the web server at:

- myapp.local
- myapp.local/phpinfo.php
- myapp.local/adminer.php

To build with your a different hostname.local address, do this:

```
docker-compose build --build-arg HOST_UID=$(id -u) --build-arg APP_HOSTNAME=your_hostname
```

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

- `HOST_UID`=num (required)

  The HOST_UID is used to ensure that the host user and the docker www-data user have the same User ID and keep permissions the same. You'd usually want to use the same user ID as the current logged in user in the host in which case you can just do set the value to `$(id -u)` which should work in most \*NIX systems.

  Example 1: to set the current user's UID `--build-arg HOST_UID=$(id -u)`\
  Example 2: to set a specific UID `--build-arg HOST_UID=1001`

- `APP_HOSTNAME`=**myapp** | _string_ (optional)

  The host name that you want to use for for your application. This makes your web server accessible via **appname.local** on your host machine. Default value is **myapp** which makes the web server accessible via **myapp.local**

- `WEB`=**httpd** | nginx (optional)

  The web server that you want to use. Available values are httpd (apache) or nginx. Default is httpd.

- `DB`=**mariadb** | mysql (optional)

  The DBMS that you want to use. Default is **mariadb** but you can also choose mysql.

  Warning: Switching DBMS on an existing container is most likely to cause errors due to incompatibility in data formats. It's best to dump the database first, clear the contents of `app/db`, switch DBMS and reimport the sql dump.

- `DB_VERSION`=**latest** | _num_ (optional)

  The DBMS version that you want to use. Default version is **latest**. For a list of available versions, see https://hub.docker.com/_/mariadb and https://hub.docker.com/_/mysql.

  Warning: Switching DBMS on an existing container is most likely to cause errors due to incompatibility in data formats. It's best to dump the database first, clear the contents of `app/db`, switch DBMS and reimport the sql dump.

- `PHP_VERSION`=**7** | 7.4 | 7.3 | 7.2 | 7.1 | 7.0 | 5.6

  The PHP version that you want to use. Currently supports 5.6, 7.0, 7.1, 7.2, 7.3 and 7.4. Setting the version to just *7* will setup the latest PHP 7 available (ie 7.4)


## Build Example

To build PHP 5.6, Nginx (latest) and MySQL 5.6, the build command would be:

```sh
docker-compose build --build-arg HOST_UID=$(id -u) \
 --build-arg PHP_VERSION=5.6 \
 --build-arg DB=mysql \
 --build-arg DB_VERSION=5.6 \
 --build-arg WEB=nginx
 ```



# PHP App Builder on Docker

Easily create a PHP Web Application

- Choose your PHP version (default latest PHP7) Tested on v5.6, v7.0, v7.1, v7.2, v7.3, and v7.4
- Choose between Apache or Nginx as your web server
- Choose your MySQL version (default latest)

Best for testing your PHP web application on a variety of environments.

## Requirements

- Docker Compose https://docs.docker.com/compose/install/

## Installation

The following will build the latest versions of PHP7, Apache, and MySQL. Once up, you may access your web application at localhost:8080

- `git clone https://github.com/easterncoder/php-app-docker.git`
- `cd php-app-docker`
- `export UID; docker-compose up --build`

## File Paths

- PHP Files (Put your PHP app here): `app/web`
- MySQL Data (This is where MySQL will store its data): `app/mysql`

## To start/stop an existing build

- `docker-compose start/stop`

## Other Build Options

Build options are specified by the following environment variables.

- WEBSERVER
  - apache (default)
  - nginx
- MYSQLVER
  - Any version as listed on https://hub.docker.com/_/mysql?tab=tags
- PHPVER
  - 7 (default: will build latest available version of PHP 7)
  - 7.4
  - 7.3
  - 7.2
  - 7.1
  - 7.0
  - 5.6

Examples:

- Latest versions of PHP7, Nginx and MySQL
  `export UID; export WEBSERVER=nginx; docker-compose up --build`

- PHP5.6, Apache (latest) and MySQL 5.6
  `export UID; export WEBSERVER=apache; export MYSQLVER=5.6; docker-compose up --build`



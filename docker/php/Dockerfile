ARG PHP_VERSION=7
FROM php:${PHP_VERSION}-fpm

# attempt to set www-data's UID to our host user's UID
ARG HOST_UID
RUN test -n "$HOST_UID" && usermod -u $HOST_UID www-data && groupmod -g $HOST_UID www-data || true

# Install some stuff
RUN apt-get update -y && apt-get install -y sendmail libpng-dev

# Install necessary extensions
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install gd
RUN docker-php-ext-install sockets

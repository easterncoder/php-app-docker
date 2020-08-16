ARG PHPVER
FROM php:${PHPVER}-fpm

# set www-data to our host user's UID
ARG HOSTUID
RUN usermod -u $HOSTUID www-data; groupmod -g $HOSTUID www-data

# Install some stuff
RUN apt-get update -y && apt-get install -y sendmail libpng-dev

# Install necessary extensions
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install gd
RUN docker-php-ext-install sockets

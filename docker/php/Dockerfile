ARG PHPVER
FROM php:${PHPVER}-fpm

# attempt to set www-data's UID to our host user's UID
ARG HOSTUID
CMD [ "$HOSTUID" -gt "1" ] && usermod -u $HOSTUID www-data && groupmod -g $HOSTUID www-data

# Install some stuff
RUN apt-get update -y && apt-get install -y sendmail libpng-dev

# Install necessary extensions
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install gd
RUN docker-php-ext-install sockets

ARG PHP_VERSION=7
FROM php:${PHP_VERSION}-fpm

# attempt to set www-data's UID to our host user's UID
ARG HOST_UID
RUN test -n "$HOST_UID" && usermod -u $HOST_UID www-data && groupmod -g $HOST_UID www-data || true

# Install some stuff
RUN apt-get update -y && apt-get install -y sendmail libpng-dev

RUN echo "sendmail_path=/usr/sbin/sendmail -t -i" >> /usr/local/etc/php/conf.d/sendmail.ini 

# Install necessary extensions
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install gd
RUN docker-php-ext-install sockets

RUN sed -i '/#!\/bin\/sh/aservice sendmail restart' /usr/local/bin/docker-php-entrypoint
RUN sed -i '/#!\/bin\/sh/aecho "$(hostname -i)\t$(hostname) $(hostname).localhost" >> /etc/hosts' /usr/local/bin/docker-php-entrypoint

# And clean up the image
RUN rm -rf /var/lib/apt/lists/*

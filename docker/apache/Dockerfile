FROM httpd:latest
RUN apt-get update -y

# Copy apache vhost file to proxy php requests to php-fpm container
COPY vhost.conf /usr/local/apache2/conf/vhost.conf
RUN echo "Include /usr/local/apache2/conf/vhost.conf" \
    >> /usr/local/apache2/conf/httpd.conf

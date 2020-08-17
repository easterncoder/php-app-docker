ARG WEB=httpd
ARG WEB_VERSION=latest

FROM $WEB:$WEB_VERSION
RUN apt-get update -y

# Copy apache config
COPY httpd/vhost.conf /usr/local/apache2/conf/vhost.conf
RUN echo "Include /usr/local/apache2/conf/vhost.conf" \
    >> /usr/local/apache2/conf/httpd.conf

# Copy nginx config
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

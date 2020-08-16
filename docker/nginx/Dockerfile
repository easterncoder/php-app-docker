FROM nginx:latest
RUN apt-get update -y

# Copy apache vhost file to proxy php requests to php-fpm container
COPY default.conf /etc/nginx/conf.d/default.conf

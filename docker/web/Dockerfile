ARG WEB=httpd

FROM $WEB:latest
RUN apt-get update -y
RUN apt-get install -y --no-install-recommends avahi-daemon libnss-mdns

# Copy apache config
COPY httpd/vhost.conf /usr/local/apache2/conf/vhost.conf
RUN echo "Include /usr/local/apache2/conf/vhost.conf" \
    >> /usr/local/apache2/conf/httpd.conf

# Copy nginx config
COPY nginx/default.conf /etc/nginx/conf.d/default.conf

# avahi
RUN printf "[server]\nenable-dbus=no\n" >> /etc/avahi/avahi-daemon.conf
RUN update-rc.d avahi-daemon defaults

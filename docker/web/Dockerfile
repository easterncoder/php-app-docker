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

# setup avahi
RUN printf "[server]\nenable-dbus=no\n" >> /etc/avahi/avahi-daemon.conf

# run avahi and the web server
CMD avahi-daemon --daemonize --no-drop-root; httpd -DFOREGROUND || nginx -g "daemon off;"
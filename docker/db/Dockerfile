ARG DB=mariadb
ARG DB_VERSION=latest

FROM ${DB}:${DB_VERSION}

# attempt to set www-data's UID to our host user's UID
ARG HOST_UID
RUN test -n "$HOST_UID" && usermod -u $HOST_UID mysql && groupmod -g $HOST_UID mysql || true

COPY init/myapp.sql /docker-entrypoint-initdb.d/

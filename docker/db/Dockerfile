ARG DB=mariadb
ARG DB_VERSION=latest

FROM ${DB}:${DB_VERSION}

COPY init/myapp.sql /docker-entrypoint-initdb.d/

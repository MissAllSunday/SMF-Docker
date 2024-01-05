FROM ubuntu:22.04

ARG PHP_VERSION
ARG PHP_REPOSITORY
ARG DB_DRIVER
ARG DB_HOST
ARG DB_PORT
ARG DB_NAME
ARG DB_USERNAME
ARG DB_PASSWORD
ARG MYSQL_VERSION
ARG SMF_VERSION
ARG WORKING_DIR
ARG TIMEZONE

RUN apt update && apt install -y curl && apt clean
ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install -y software-properties-common && apt-add-repository --yes ${PHP_REPOSITORY}
RUN apt update && apt install -y php${PHP_VERSION} \
  php${PHP_VERSION}-fpm \
  php${PHP_VERSION}-cli \
  php${PHP_VERSION}-gd \
  php${PHP_VERSION}-xml \
  php${PHP_VERSION}-mysql \
  php${PHP_VERSION}-curl \
  php${PHP_VERSION}-redis \
  php${PHP_VERSION}-xdebug \
  php${PHP_VERSION}-memcached \
  php${PHP_VERSION}-mbstring \
  php${PHP_VERSION}-zip \
  && apt clean

RUN apt update && apt install -y mysql-client memcached libmemcached-tools && apt clean

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN mkdir -p /run/php
RUN useradd -r -g www-data --uid 1000 php -d /run/php
ENV PATH="/run/php/bin:/run/php/personalBin/:${PATH}"
RUN chown -R php /run/php
RUN echo ${TIMEZONE} | tee /etc/timezone
RUN ln -sf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime

COPY smf/ .
USER root

RUN cp other/install.php install.php && \
    cp other/install_2-1_mysql.sql install_2-1_mysql.sql && \
    cp other/Settings.php Settings.php && \
    chmod 777 Settings.php && \
    cp Settings.php Settings_bak.php
FROM php:7.3-fpm
COPY smf/ .
RUN chmod 777 attachments/ && \
    chmod 777 avatars/ && \
    chmod 777 custom_avatar/ && \
    chmod 777 cache/ && \
    chmod 777 Packages/ && \
    chmod 777 Smileys/ && \
    chmod 777 Themes/ && \
    chmod 777 agreement.txt && \
    cp other/install.php install.php && \
    cp other/install_2-1_mysql.sql install_2-1_mysql.sql && \
    cp other/Settings.php Settings.php && \
    chmod 777 Settings.php
RUN apt-get update && apt-get install -y --no-install-recommends \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) mysqli

ARG WITH_XDEBUG=true

RUN if [ $WITH_XDEBUG = "true" ] ; then \
        pecl install xdebug; \
        docker-php-ext-enable xdebug; \
        echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
        echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
        echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
        echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini; \
    fi ;
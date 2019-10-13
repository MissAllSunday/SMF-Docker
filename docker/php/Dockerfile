FROM php:7.2-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN pecl install redis-4.0.1 \
    && pecl install xdebug-2.6.0 \
    && docker-php-ext-enable redis xdebug

RUN apt-get install git -y
RUN git clone git@github.com:SimpleMachines/SMF2.1.git smf
RUN cd smf \
    && cp other/install_2-1_mysql.sql install.php \
    && cp other/install_2-1_mysql.sql install_2-1_mysql.sql \
    && cp other/Settings.php Settings.php
FROM php:7.3-fpm
LABEL author "Melvin Versluijs <https://github.com/melvinversluijs/>"
RUN apt-get -y update
RUN apt-get -y install libpng-dev  libjpeg-dev libfreetype6-dev

## Install mysqli php extension.
RUN docker-php-ext-install mysqli

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
  && docker-php-ext-install gd

## Install xdebug.
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

## Copy wordpress files.
COPY ./wordpress/ /code

## Set custom php variables.
COPY ./docker/php/php_custom.ini /usr/local/etc/php/conf.d/php_custom.ini
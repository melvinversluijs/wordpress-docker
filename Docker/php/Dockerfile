FROM php:7.2-fpm
LABEL author "Melvin Versluijs <melvin.versluijs@outlook.com>"
RUN apt-get -y update
RUN docker-php-ext-install \
  mysqli 
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
COPY ./php_xdebug.ini /usr/local/etc/php/conf.d/php_xdebug.ini
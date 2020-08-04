FROM php:7.4-apache
LABEL author "Melvin Versluijs <https://github.com/melvinversluijs/>"
RUN apt-get -y update
RUN apt-get -y install libpng-dev  libjpeg-dev libfreetype6-dev

## Install mysqli php extension.
RUN docker-php-ext-install mysqli

RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install gd

## Install xdebug.
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

## Install WP-CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar && mv wp-cli.phar /usr/local/bin/wp

## Set custom php variables.
COPY ./docker/php/php_custom.ini /usr/local/etc/php/conf.d/php_custom.ini

## Set apache config.
COPY ./docker/php/apache.conf /etc/apache2/sites-enabled/apache.conf
COPY ./docker/php/certs/*  /etc/apache2/ssl/

RUN a2enmod rewrite && a2enmod ssl && service apache2 restart

## Copy wordpress files.
COPY ./wordpress/ /var/www/html

EXPOSE 80
EXPOSE 443
FROM php:8.1-apache

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get -y install wget zip

RUN pecl install redis xdebug xml soap json curl mysqli

RUN docker-php-ext-enable redis xdebug

RUN a2enmod rewrite

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"

RUN php composer-setup.php
RUN mv composer.phar /usr/local/bin/composer
RUN php -r "unlink('composer-setup.php');"

RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN apt install -y libicu-dev libxml2 libxml2-dev nano libpng-dev git ffmpeg
RUN docker-php-ext-configure intl; docker-php-ext-install intl gd soap

RUN docker-php-ext-enable gd

RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
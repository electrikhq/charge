FROM php:8.1-fpm

RUN apt-get update -y && apt-get install -y nodejs npm
RUN apt-get install zip unzip

RUN docker-php-ext-install pdo pdo_mysql bcmath

RUN pecl install redis \
    && docker-php-ext-enable redis

# Installing composer
RUN curl -sS https://getcomposer.org/installer -o composer-setup.php
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN rm -rf composer-setup.php

# Setup working directory
WORKDIR /var/www/html

RUN composer create-project laravel/laravel /var/www/html --prefer-dist
RUN composer require electrik/electrik:dev-development
RUN php /var/www/html/artisan electrik:install --no-interaction

# Expose
CMD php artisan serve --host=0.0.0.0 --port=8000
EXPOSE 8000
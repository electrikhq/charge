FROM php:8.1-fpm

RUN apt-get update -y
RUN apt-get install zip unzip

RUN docker-php-ext-install pdo pdo_mysql

RUN pecl install redis \
    && docker-php-ext-enable redis

RUN apt-get install -y supervisor

ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf

# CMD ["/usr/bin/supervisord"]
CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisor.conf"]


FROM php:8.1-fpm

RUN apt-get update -y

RUN apt-get install -y cron nodejs npm
RUN apt-get install zip unzip

RUN docker-php-ext-install pdo pdo_mysql

RUN pecl install -f redis \
    && docker-php-ext-enable redis

COPY scheduler /etc/cron.d/scheduler
RUN chmod 0644 /etc/cron.d/scheduler
RUN crontab /etc/cron.d/scheduler


CMD ["cron", "-f"]

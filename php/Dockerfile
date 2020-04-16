FROM php:7.4.1-fpm-alpine3.11

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

COPY composer.phar /usr/local/bin/composer
COPY swoole-src-4.4.15.tar.gz /tmp/swoole.tar.gz
COPY phpredis-5.0.2.tar.gz /tmp/reids.tar.gz

RUN apk update \

    && apk add --no-cache tzdata autoconf gcc g++ make zlib-dev curl-dev libmcrypt-dev libpng-dev libzip-dev \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del tzdata \

    && docker-php-ext-install mysqli opcache gd pcntl zip pdo pdo_mysql bcmath \

    && docker-php-source extract \

    && tar -xzf /tmp/reids.tar.gz \
    && mv phpredis-5.0.2 /usr/src/php/ext/reids \
    && docker-php-ext-install reids \

    && tar -xzf /tmp/swoole.tar.gz \
    && mv swoole-src-4.4.15 /usr/src/php/ext/swoole \
    && docker-php-ext-install swoole \

    && chmod 755 /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
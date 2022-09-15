FROM php:8.0-fpm

ENV PHP_UPLOAD_MAX_FILESIZE=32M
ENV PHP_POST_MAX_SIZE=32M
ENV PHP_MAX_INPUT_VARS=50000
ENV PHP_MEMORY_LIMIT=128M

ENV PHP_APP_DIRECTORY=/app

ENV COMPOSER_MEMORY_LIMIT=-1

WORKDIR ${PHP_APP_DIRECTORY}

RUN mkdir -p ${PHP_APP_DIRECTORY}

RUN apt-get update && apt-get install -y \
# php-ext gd
    libjpeg62-turbo-dev libpng-dev libwebp-dev\
# php-ext intl
    zlib1g-dev libicu-dev g++ \
# php-ext zip
    libzip-dev \
# composer
    zip \
# https://symfony.com/blog/fast-smart-flex-recipe-upgrades-with-recipes-update#hello-recipes-update
    git

RUN docker-php-ext-configure gd --enable-gd --with-webp --with-jpeg \
    && docker-php-ext-configure exif \
    && docker-php-ext-configure intl \
    && docker-php-ext-install gd exif intl mysqli pdo_mysql zip

RUN pecl install xdebug-3.1.4 \
    && docker-php-ext-enable xdebug

COPY xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY php.ini /usr/local/etc/php/php.ini

RUN usermod -u 1000 www-data

COPY --from=composer:2.3 /usr/bin/composer /usr/bin/composer

RUN mkdir -p /var/www/.composer \
    && chown www-data:www-data /var/www/.composer

USER www-data

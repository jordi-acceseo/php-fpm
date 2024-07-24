FROM php:8.1.29-fpm

LABEL org.opencontainers.image.title="PHP-FPM"
LABEL org.opencontainers.image.description="Opinionated PHP-FPM container for development"
LABEL org.opencontainers.image.version=1.0.0
LABEL org.opencontainers.image.authors="acceseo Projects S.L."
LABEL org.opencontainers.image.url="https://github.com/acceseo/php-fpm"
LABEL org.opencontainers.image.licenses="MIT License"

ENV PHP_UPLOAD_MAX_FILESIZE=32M
ENV PHP_POST_MAX_SIZE=32M
ENV PHP_MAX_INPUT_VARS=50000
ENV PHP_MEMORY_LIMIT=128M
ENV PHP_MAX_EXECUTION_TIME=30
ENV PHP_MAX_INPUT_TIME=60
ENV TZ=Europe/Madrid

ENV PHP_IDE_CONFIG="serverName=localhost"

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
    git \
#php-ext pgsql
    libpq-dev

RUN docker-php-ext-configure gd --enable-gd --with-webp --with-jpeg \
    && docker-php-ext-configure exif \
    && docker-php-ext-configure intl \
    && docker-php-ext-install gd exif intl mysqli pdo_mysql zip pgsql pdo_pgsql

RUN pecl install xdebug-3.3.1 \
    && docker-php-ext-enable xdebug

COPY xdebug.ini $PHP_INI_DIR/conf.d/xdebug.ini
COPY php.ini $PHP_INI_DIR/php.ini

RUN usermod -u 1000 www-data

COPY --from=composer/composer:2.5.1-bin /composer /usr/bin/composer

COPY --from=wordpress:cli-2.7.1-php8.1 /usr/local/bin/wp /usr/local/bin/wp

RUN mkdir -p /var/www/.composer \
    && chown www-data:www-data /var/www/.composer

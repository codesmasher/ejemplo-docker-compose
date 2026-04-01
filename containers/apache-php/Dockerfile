FROM php:apache-bookworm

COPY php.ini "$PHP_INI_DIR/php.ini"

# Download and install dependencies
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libpq-dev \
    libzip-dev \
    libicu-dev \
    zip
# Install from docker-php
RUN docker-php-source extract \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install pdo pdo_pgsql pgsql \
    && docker-php-ext-install zip \
    && docker-php-source delete
# Install xDebug from pecl
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

EXPOSE 80

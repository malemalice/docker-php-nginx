FROM php:7.4-fpm-alpine
# RUN docker-php-ext-install opcache
# COPY php/production/opcache.ini /usr/local/etc/php/conf.d/opcache.ini
# Install dependencies
COPY php/php.ini /usr/local/etc/php/conf.d/docker-php-custom.ini
RUN apk update
RUN apk add --no-cache git libzip-dev zip unzip icu-dev $PHPIZE_DEPS \
    && pecl install xdebug-3.1.0 \
    && docker-php-ext-enable xdebug && \
    echo -e "xdebug.remote_enable=1\n\
        xdebug.remote_autostart=1\n\
        xdebug.remote_connect_back=0\n\
        xdebug.remote_log=/var/www/html/xdebug.log\n\
        xdebug.mode=develop,coverage\n\
        xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN docker-php-ext-install pdo pdo_mysql mysqli zip exif \
    && curl -sS https://getcomposer.org/installer | php -- \
    --install-dir=/usr/local/bin --filename=composer
RUN docker-php-ext-configure intl && docker-php-ext-install intl


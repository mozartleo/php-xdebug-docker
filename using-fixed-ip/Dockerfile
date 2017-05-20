FROM php:5.6-fpm
RUN pecl install xdebug-2.5.3 \
    && docker-php-ext-enable xdebug

COPY 99-xdebug.ini /usr/local/etc/php/conf.d/


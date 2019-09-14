FROM composer:latest as composer 
WORKDIR /app 
COPY . /app 
RUN composer install --optimize-autoloader --no-dev

FROM node:carbon-alpine as npm 

WORKDIR /app
COPY --from=composer /app /app

RUN npm install 

FROM php:7-fpm-alpine as app

WORKDIR /var/www

RUN apk --update add wget \
  curl \
  git \
  grep \
  build-base \
  libmemcached-dev \
  libmcrypt-dev \
  libxml2-dev \
  imagemagick-dev \
  pcre-dev \
  libtool \
  make \
  autoconf \
  g++ \
  cyrus-sasl-dev \
  libgsasl-dev \
  supervisor

RUN docker-php-ext-install mysqli mbstring pdo pdo_mysql tokenizer xml
RUN pecl channel-update pecl.php.net \
    && pecl install memcached \
    && pecl install imagick \
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable memcached \
    && docker-php-ext-enable imagick \
    && docker-php-ext-enable mcrypt

RUN rm /var/cache/apk/*

EXPOSE 9000 

COPY --from=npm /app /var/www 

RUN chown -R www-data:www-data \
        /var/www/storage \
        /var/www/bootstrap/cache

RUN php artisan passport:keys --force

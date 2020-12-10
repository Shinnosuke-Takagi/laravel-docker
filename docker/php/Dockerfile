FROM php:7.3-fpm-alpine
LABEL maintainer "Shinnosuke-Takagi"

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies \
  tzdata \
  freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev && \
  cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
  docker-php-ext-configure gd \
    --with-freetype-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-png-dir=/usr/include/ && \
  docker-php-ext-install bcmath pdo_mysql gd && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer config -g repos.packagist composer https://packagist.jp 

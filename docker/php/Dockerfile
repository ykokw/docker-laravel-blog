FROM php:7.4-fpm-alpine
LABEL maintainer "ykokw"

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
  apk del .build-dependencies && \
  docker-php-ext-install bcmath pdo_mysql && \
  composer config -g repos.packagist composer https://packagist.jp && \
  composer global require hirak/prestissimo
FROM php:8.3.36-cli-alpine3.24@sha256:9e3f659660bf060ac3baaa56bfdfb07ef92d12cda24e702cc762ef7fb036cfb6

WORKDIR /usr/share/www

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

RUN apk add --no-cache --virtual .pipeline-deps \
      autoconf \
      automake \
      libtool  \
      linux-headers \
      nasm \
      gcc \
      g++ \
      make \
      pkgconf && \
    apk --no-cache add \
      nodejs \
      npm \
      bash \
      git \
      openssh \
      mariadb-connector-c-dev \
      mariadb-client \
      zip \
      unzip \
      libzip-dev \
      icu-dev \
      jpeg-dev \
      libpng-dev \
      curl-dev \
      oniguruma-dev \
      libxml2-dev && \
    docker-php-ext-configure gd --with-jpeg && \
    docker-php-ext-install \
      gd \
      soap \
      zip \
      bcmath \
      exif \
      intl \
      dom \
      curl \
      mbstring \
      opcache \
      mysqli \
      pdo_mysql && \
    pecl install xdebug && \
    docker-php-ext-enable xdebug
#  leaved as it's needed for "npm install" shits
#    apk del .pipeline-deps

# Supress composer root warning
ENV COMPOSER_ALLOW_SUPERUSER=1
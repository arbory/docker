FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
ARG NODE_MAJOR=18

RUN apt-get update \
    && apt-get install -y gnupg gosu curl ca-certificates zip unzip git libcap2-bin software-properties-common libpng-dev \
    && add-apt-repository ppa:ondrej/php \
    && mkdir -p /etc/apt/keyrings \
    && curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg \
    && echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | tee /etc/apt/sources.list.d/nodesource.list \
    && apt-get update \
    && apt-get install -y \
      openssh-client \
      rsync \
      bzip2 \
      mysql-client \
      php8.2-cli \
      php8.2-curl \
      php8.2-dom \
      php8.2-fpm \
      php8.2-gd \
      php8.2-iconv \
      php8.2-mbstring \
      php8.2-mysql \
      php8.2-soap \
      php8.2-xml \
      php8.2-xmlreader \
      php8.2-xmlwriter \
      php8.2-intl \
      php8.2-ldap \
      php8.2-opcache \
      php8.2-bcmath \
      php8.2-zip \
      nodejs

# Supress composer root warning
ENV COMPOSER_ALLOW_SUPERUSER=1

# Copy composer from already built image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive

# Prepare to get repository with php7.4
# Repository is added cause Ubuntu 18.04 don't have php7.4 in its package.
RUN apt-get update && \
    apt install -y \
    curl \
    wget \
    gnupg2 \
    ca-certificates \
    lsb-release \
    apt-transport-https \
    software-properties-common

# Add Ondřej Surý repository.
RUN add-apt-repository ppa:ondrej/php && \
    apt-get update

# Install git, php, e.t.c.
RUN apt-get update -qq && apt-get install --no-install-recommends -y \
    openssh-client \
    rsync \
    git \
    unzip \
    bzip2 \
    postgresql-client \
    gpg-agent \
    curl \
    gnupg \
    ca-certificates \
    php7.4-cli \
    php7.4-curl \
    php7.4-dom \
    php7.4-fpm \
    php7.4-gd \
    php7.4-iconv \
    php7.4-mbstring \
    php7.4-pgsql \
    php7.4-soap \
    php7.4-xml \
    php7.4-xmlreader \
    php7.4-xmlwriter \
    php7.4-zip

# Add yarn repository
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Add node 12.x repository
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

# apt-get update is called by node setup script already
RUN apt-get install --no-install-recommends -y \
    nodejs \
    yarn

# Configure FPM to run properly on docker
RUN sed -i "s/upload_max_filesize = .*/upload_max_filesize = 10M/" /etc/php/7.4/fpm/php.ini
RUN sed -i "s/post_max_size = .*/post_max_size = 12M/" /etc/php/7.4/fpm/php.ini
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.4/fpm/php.ini

RUN sed -i -e "s/pid =.*/pid = \/var\/run\/php7.4-fpm.pid/" /etc/php/7.4/fpm/php-fpm.conf
RUN sed -i -e "s/error_log =.*/error_log = \/proc\/self\/fd\/2/" /etc/php/7.4/fpm/php-fpm.conf
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php/7.4/fpm/php-fpm.conf
RUN sed -i "s/listen = .*/listen = 9000/" /etc/php/7.4/fpm/pool.d/www.conf
RUN sed -i "s/;catch_workers_output = .*/catch_workers_output = yes/" /etc/php/7.4/fpm/pool.d/www.conf
RUN sed -i "s/;clear_env = no/clear_env = no/" /etc/php/7.4/fpm/pool.d/www.conf

# Supress composer root warning
ENV COMPOSER_ALLOW_SUPERUSER=1

# Copy composer from already built image
COPY --from=composer:1 /usr/bin/composer /usr/bin/composer

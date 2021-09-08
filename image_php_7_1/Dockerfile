FROM php:7.1-fpm

# Set default php ini
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN sed -i'' 's/archive\.ubuntu\.com/us\.archive\.ubuntu\.com/' /etc/apt/sources.list

# make sure apt is up to date
RUN apt-get update --fix-missing

RUN apt-get install -y apt-utils

# install git
RUN apt-get install -y git

# install supervisor
RUN apt-get install -y supervisor

# install cron
RUN apt-get install -y cron

# install Nano
RUN apt-get install -y nano

# install iputils-ping
RUN apt-get install -y iputils-ping

# install net-tools
RUN apt-get install -y net-tools

# install curl
RUN apt-get install -y curl

# install composer
RUN curl -s https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# install php gettext
RUN docker-php-ext-install gettext

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Install debian main library
RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev

# install nodejs
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 12.18.2
RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

WORKDIR /var/www/html

# configure php gd
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd \
    --with-png-dir=/usr/include/ \
    --with-jpeg-dir=/usr/include/ \
    --with-freetype-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# install pdo pdo_mysql mysqli
RUN docker-php-ext-install pdo pdo_mysql mysqli

# install zip
RUN apt-get install -y libzip-dev zlib1g-dev \
    && docker-php-ext-install zip
    
# Install imagick
RUN apt-get install -y \
    libmagickwand-dev --no-install-recommends \
    && pecl install imagick \
    && docker-php-ext-enable imagick




FROM php:7.0-apache

RUN apt-get update

# install supervisor
RUN apt-get install supervisor -y

# install cron
RUN apt-get install -y cron

# install git
RUN apt-get install -y git

# install Nano
RUN apt-get install -y nano

# install iputils-ping
RUN apt-get install -y iputils-ping

# install net-tools
RUN apt-get install -y net-tools

RUN curl -s https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# make sure apt is up to date
RUN apt-get update --fix-missing
RUN apt-get install -y curl
RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 9.2.0

# Install nvm with node and npm
RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

WORKDIR /var/www/html

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

RUN docker-php-ext-install pdo pdo_mysql mysqli

RUN apt-get install -y libzip-dev zlib1g-dev \
    && docker-php-ext-install zip

# ADD vhost/000-default.conf /etc/apache2/sites-enabled/000-default.conf

# remove index.php from the URL
RUN a2enmod rewrite

# Join www-data to root group
RUN usermod -a -G root www-data

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
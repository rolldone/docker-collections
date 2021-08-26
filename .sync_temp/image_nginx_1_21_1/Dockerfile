FROM nginx:1.21.1

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

WORKDIR /var/www/html

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Check default config
RUN cat /etc/nginx/conf.d/default.conf
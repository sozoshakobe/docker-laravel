FROM php:7.2-fpm

# install composer
RUN cd /usr/bin && curl -s http://getcomposer.org/installer | php && ln -s /usr/bin/composer.phar /usr/bin/composer
RUN apt-get update \
&& apt-get install -y \
git \
zip \
unzip \
vim

RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_mysql pdo_pgsql

RUN apt-get install -y sudo

#install node.js
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash - \ 
    && apt-get update \
    && apt-get install -y nodejs \
    && npm install npm@latest -g

WORKDIR /var/www/html

ARG DOCKER_UID=1000
ARG DOCKER_USER=docker
ARG DOCKER_PASSWORD=docker

RUN useradd -m --uid ${DOCKER_UID} --groups sudo ${DOCKER_USER} \
&& echo ${DOCKER_USER}:${DOCKER_PASSWORD} | chpasswd

USER ${DOCKER_USER}
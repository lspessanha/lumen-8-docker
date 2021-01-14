FROM ubuntu:20.04

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget curl nano htop git unzip bzip2 software-properties-common locales tzdata

ENV TZ=America/Fortaleza
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

WORKDIR /var/www/html

RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt update
RUN apt-get install -y \
    php8.0-fpm \ 
    php8.0-common \ 
    php8.0-curl \ 
    php8.0-mysql \ 
    php8.0-mbstring \ 
    php8.0-xml

RUN echo "date.timezone = $TZ" >> /etc/php/8.0/cli/php.ini
ADD docker/conf/www.conf /etc/php/8.0/fpm/pool.d/www.conf
RUN mkdir -p /var/run/php

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C
RUN echo "deb http://nginx.org/packages/ubuntu/ trusty nginx" >> /etc/apt/sources.list
RUN echo "deb-src http://nginx.org/packages/ubuntu/ trusty nginx" >> /etc/apt/sources.list
RUN apt-get update

RUN apt-get install -y nginx

ADD docker/conf/default /etc/nginx/sites-enabled/

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
ADD docker/conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80

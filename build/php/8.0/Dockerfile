FROM php:8.0.22-fpm-buster

RUN apt-get update \
    && apt-get install -y autoconf \
    joe \
    make \
    gcc \
    automake \
    pkg-config \
    zlib1g-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libldb-dev \
    libldap2-dev \
    libbz2-dev \
    libxml2-dev \
    libzip-dev \
    libc-client-dev \
    libkrb5-dev
    

RUN docker-php-ext-configure gd --with-jpeg --with-freetype && \
  docker-php-ext-install gd  
RUN docker-php-ext-configure ldap && \
  docker-php-ext-install ldap
RUN docker-php-ext-configure bz2 && \
  docker-php-ext-install bz2 
RUN docker-php-ext-configure bcmath && \ 
  docker-php-ext-install bcmath
RUN docker-php-ext-configure soap && \
  docker-php-ext-install soap
RUN pecl install redis &&  \
  docker-php-ext-enable redis
RUN docker-php-ext-install zip
RUN docker-php-ext-install mysqli pdo pdo_mysql && \
  docker-php-ext-enable pdo_mysql
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && \
  docker-php-ext-install imap && \
  docker-php-ext-enable imap


COPY php-fpm.conf /usr/local/etc/php-fpm.conf
COPY www.conf /usr/local/etc/php-fpm.d/www.conf
COPY tuning.ini /usr/local/etc/php/tuning.ini
RUN mv "/usr/local/etc/php/php.ini-production" "/usr/local/etc/php/php.ini" && \
  cat /usr/local/etc/php/tuning.ini >> /usr/local/etc/php/php.ini


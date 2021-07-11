FROM php:7.2-fpm

#Defining user and uid
ARG uid=1000
ARG user=diegosp

RUN apt-get update && apt-get install -y \
	git \
	curl \
	libpng-dev \
	libonig-dev \
	libxml2-dev \
	zip \
	unzip

RUN apt-get clean && rm -rf /var/lib/apt/list/*
RUN docker-php-ext-install pdo_mysql mysqli mbstring exif pcntl bcmath gd

RUN pecl install xdebug \
	&& docker-php-ext-enable xdebug

#Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
	chown -R $user:$user /home/$user

#Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

#Set Working directory
WORKDIR /var/www/html

USER $user

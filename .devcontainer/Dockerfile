FROM php:8.1-apache

# Set new document root
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Install additional php modules - https://hub.docker.com/_/php
RUN apt-get update && \
    apt-get install -y htop libpq-dev zlib1g-dev libzip-dev && \
    docker-php-ext-install pdo pdo_mysql mysqli zip

# Activate Apache modules
RUN a2enmod -q rewrite

# Install composer so we can install required packages
RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer
RUN alias composer='php composer.phar'

# Install packages
VOLUME /var/www/html
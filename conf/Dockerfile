ARG PHP_VERSION
FROM php:${PHP_VERSION}-apache

WORKDIR /app

# update & upgrade
RUN apt-get update -y && apt-get upgrade -y && apt-get install apt-utils -y

# Php extensions
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions intl bcmath gd pdo_mysql pdo_pgsql opcache uuid exif pcntl zip

COPY php.ini /usr/local/etc/php/conf.d/app.ini

## Apache
COPY vhost.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite
RUN chown -R www-data:www-data /app

## Install composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Install nodeJS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs

CMD /usr/sbin/apache2ctl -D FOREGROUND
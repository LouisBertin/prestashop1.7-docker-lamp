FROM php:7.3-apache

# update and upgrade
RUN apt-get update && apt-get upgrade -y
# dependencies
RUN apt-get install -y git cron g++ gettext libicu-dev openssl libc-client-dev libkrb5-dev libxml2-dev libfreetype6-dev libgd-dev libmcrypt-dev bzip2 zip libzip-dev libbz2-dev libtidy-dev libcurl4-openssl-dev libz-dev libmemcached-dev libxslt-dev libicu-dev libmagickwand-dev

## php modules
RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr
RUN docker-php-ext-install gd
RUN docker-php-ext-install mysqli
RUN docker-php-ext-configure calendar && docker-php-ext-install calendar
RUN docker-php-ext-configure intl && docker-php-ext-install intl
RUN docker-php-ext-configure zip --with-libzip && docker-php-ext-install zip
RUN pecl install imagick && docker-php-ext-enable imagick
RUN pecl install memcached && docker-php-ext-enable memcached
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install opcache

ADD ./php.ini /usr/local/etc/php/conf.d/app.ini
ADD ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

## apache modules
RUN a2enmod rewrite

# composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php --install-dir=/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

EXPOSE 80
CMD /usr/sbin/apache2ctl -D FOREGROUND

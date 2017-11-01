FROM php:7.1-fpm

RUN apt-get update
RUN apt-get install -y git-core
RUN apt-get install -y zip unzip
RUN apt-get install -y mc
RUN apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql pdo_mysql
RUN apt-get install -y libicu-dev && docker-php-ext-install intl
RUN apt-get install -y libcurl4-gnutls-dev && docker-php-ext-install curl
RUN docker-php-ext-install opcache
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install zip
# Install GD
RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

RUN pecl install xdebug && docker-php-ext-enable xdebug
RUN pecl install redis && docker-php-ext-enable redis

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN usermod -u 1000 www-data

USER www-data

WORKDIR /var/www

EXPOSE 9000
CMD ["php-fpm"]
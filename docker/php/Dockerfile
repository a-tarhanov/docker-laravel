ARG PHP_VERSION=8.0
FROM php:${PHP_VERSION}-fpm

# Update apt-get
RUN apt-get update

# Install git
RUN apt-get install -y git

# Install zip unzip
RUN apt-get install -y zip unzip

# Install opcache
RUN docker-php-ext-install opcache

# Install pdo
RUN apt-get install -y libpq-dev
RUN docker-php-ext-install pdo mysqli pgsql pdo_mysql pdo_pgsql

# Install mbstring
RUN apt-get install -y libonig-dev
RUN docker-php-ext-install mbstring

# Install bcmath
RUN docker-php-ext-install bcmath

# Install tokenizer
RUN docker-php-ext-install tokenizer

# Install xml
RUN apt-get install -y libxml2-dev
RUN docker-php-ext-install xml

# Install zip
RUN apt-get install -y libzip-dev
RUN docker-php-ext-install zip

# Install sockets
RUN docker-php-ext-install sockets

# Install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Install composer
RUN curl -s http://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Install redis
RUN pecl install -o -f redis
RUN rm -rf /tmp/pear
RUN docker-php-ext-enable redis

# Install gd
RUN apt-get install -y zlib1g-dev libpng-dev libwebp-dev libjpeg62-turbo-dev libfreetype6-dev
RUN docker-php-ext-configure gd \
    --with-freetype=/usr/include/ \
    --with-webp=/usr/include/ \
    --with-jpeg=/usr/include/;
RUN docker-php-ext-install gd

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update
RUN apt install -y yarn

# Install crontab
RUN apt-get install -y cron
COPY ./crontab /etc/cron.d
RUN chmod -R 0644 /etc/cron.d

# Install supervisor
RUN apt-get install -y supervisor
COPY ./supervisor.conf /etc/supervisor/supervisor.conf
RUN chmod -R 0644 /etc/supervisor/supervisor.conf

# Config php
COPY ./config/user.ini /usr/local/etc/php/conf.d
COPY ./config/opcache.ini /usr/local/etc/php/conf.d
COPY ./config/xdebug.ini /usr/local/etc/php/conf.d

# Config user
RUN groupmod -o -g 1000 www-data
RUN usermod -o -u 1000 -g www-data www-data

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisor.conf"]

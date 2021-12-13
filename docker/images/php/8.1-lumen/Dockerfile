FROM php:8.1-fpm

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
RUN docker-php-ext-install pdo pgsql pdo_pgsql mysqli pdo_mysql

# Install mbstring
RUN apt-get install -y libonig-dev
RUN docker-php-ext-install mbstring

# Install zip
RUN apt-get install -y libzip-dev
RUN docker-php-ext-install zip

# Install exif
RUN docker-php-ext-install exif

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

# Install cron
RUN apt-get install -y cron
RUN echo "* * * * * root /usr/local/bin/php /var/www/html/artisan schedule:run >> /dev/null 2>&1" | tee /etc/cron.d/root
RUN chmod 0644 /etc/cron.d/root

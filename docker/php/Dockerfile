FROM php:7.2-fpm

RUN apt update \
    && apt install -y libxml2-dev zlib1g-dev \
    && docker-php-ext-install mbstring pdo pdo_mysql tokenizer xml bcmath zip

RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

WORKDIR /var/www/html
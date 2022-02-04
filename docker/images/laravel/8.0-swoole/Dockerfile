FROM php:8.0-cli

# Install dependencies
RUN apt-get update && \
    apt-get install -y \
        git \
        zip unzip \
        libpq-dev \
        libonig-dev \
        libxml2-dev \
        libzip-dev  \
        zlib1g-dev libpng-dev libwebp-dev libjpeg62-turbo-dev libfreetype6-dev \
        cron

# Install extensions
RUN docker-php-ext-configure gd \
        --with-freetype=/usr/include/ \
        --with-webp=/usr/include/ \
        --with-jpeg=/usr/include/ && \
    docker-php-ext-install \
        opcache \
        pdo pgsql pdo_pgsql mysqli pdo_mysql \
        mbstring \
        bcmath \
        xml \
        zip \
        exif \
        pcntl \
        gd

# Install redis
RUN pecl install redis && \
    docker-php-ext-enable redis

# Install swoole
RUN pecl install swoole && \
    docker-php-ext-enable swoole

# Install composer
RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
    apt-get install -y nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

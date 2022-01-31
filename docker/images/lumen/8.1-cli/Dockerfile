FROM php:8.1-cli

# Install dependencies
RUN apt-get update && \
    apt-get install -y \
        git \
        zip unzip \
        libpq-dev \
        libonig-dev \
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
        zip \
        sockets \
        exif \
        gd

# Install redis
RUN pecl install redis && \
    docker-php-ext-enable redis

# Setup cron
RUN echo "* * * * * root /usr/local/bin/php /var/www/html/artisan schedule:run >> /dev/null 2>&1" | tee /etc/cron.d/root && \
    chmod 0644 /etc/cron.d/root

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

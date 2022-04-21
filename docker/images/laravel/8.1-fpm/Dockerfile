FROM php:8.1-fpm

# Install dependencies

RUN apt-get update && apt-get install -y \
    bash \
    curl \
    git \
    make \
    nodejs \
    npm \
    yarn

# Install php extensions

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions \
    @composer \
    bcmath \
    calendar \
    exif \
    gd \
    imagick \
    intl \
    opcache \
    pcntl \
    pdo_mysql \
    pdo_pgsql \
    redis \
    soap \
    sockets \
    xdebug \
    zip

# Clean up

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

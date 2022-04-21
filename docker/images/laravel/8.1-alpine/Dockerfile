FROM php:8.1-alpine

# Install dependencies

RUN apk add --no-cache \
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

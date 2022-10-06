FROM php:8.1-alpine

# Install dependencies

RUN apk add --no-cache \
    bash \
    curl \
    git \
    postgresql-client \
    make \
    nodejs \
    npm \
    shadow \
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
    pgsql \
    redis \
    soap \
    sockets \
    xdebug-stable \
    zip

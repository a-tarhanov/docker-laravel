ARG PHP_CONTAINER_VERSION=7.4
FROM php:${PHP_CONTAINER_VERSION}-fpm

ARG PHP_CONTAINER_VERSION=7.4

# Install dependencies
RUN apt-get update
RUN apt-get install -y \
    build-essential \
    libpng-dev libjpeg62-turbo-dev libwebp-dev libfreetype6-dev \
    jpegoptim optipng pngquant gifsicle libmagickwand-dev imagemagick \
    libxml2-dev zlib1g-dev libonig-dev libzip-dev libpq-dev \
    zip unzip locales vim curl cron supervisor

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update
RUN apt install -y yarn

# Install extensions
RUN if [ ${PHP_CONTAINER_VERSION} = "7.4" ] || [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ]; then \
    docker-php-ext-configure gd \
        --with-freetype=/usr/include/ \
        --with-webp=/usr/include/ \
        --with-jpeg=/usr/include/; \
else \
    docker-php-ext-configure gd \
        --with-freetype-dir=/usr/include/ \
        --with-png-dir=/usr/include/ \
        --with-webp-dir=/usr/include/ \
        --with-jpeg-dir=/usr/include/; \
fi

RUN docker-php-ext-install \
    pdo mysqli pdo_mysql pgsql pdo_pgsql \
    mbstring tokenizer xml bcmath zip gd exif pcntl opcache sockets

# Install redis
RUN pecl install -o -f redis && \
    rm -rf /tmp/pear && \
    docker-php-ext-enable redis

# Install imagick
RUN if [ $(php -r "echo PHP_MAJOR_VERSION;") = "8" ]; then \
        apt-get install -y git && \
        cd /tmp && \
        git clone https://github.com/Imagick/imagick; \
        cd imagick && \
        phpize && \
        ./configure && \
        make && \
        make install && \
        rm -r /tmp/imagick; \
    else \
        pecl install imagick; \
    fi && \
    docker-php-ext-enable imagick

# Install XDebug
RUN pecl install xdebug && \
   docker-php-ext-enable xdebug

COPY ./xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini

# Install composer
RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Set Timezone
ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# PHP Config
COPY ./user.ini /usr/local/etc/php/conf.d
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

# Crontab Config
COPY ./crontab /etc/cron.d
RUN chmod -R 0644 /etc/cron.d

# Supervisor Config
COPY ./supervisor.conf /etc/supervisor/supervisor.conf
RUN chmod -R 0644 /etc/supervisor/supervisor.conf

# User Config
RUN groupmod -o -g 1000 www-data && \
    usermod -o -u 1000 -g www-data www-data

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisor.conf"]

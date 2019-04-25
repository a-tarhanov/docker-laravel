FROM php:7.2-fpm

### PHP Extension ###

RUN apt update \
    && apt install -y libxml2-dev zlib1g-dev libjpeg-dev libpng-dev libfreetype6-dev \
    && docker-php-ext-configure gd \
      --with-jpeg-dir=/usr/lib \
      --with-freetype-dir=/usr/include/freetype2 \
    && docker-php-ext-install mbstring pdo pdo_mysql tokenizer xml bcmath zip gd

### Composer ###

RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

### Cron ###

RUN apt install -y cron
COPY ./crontab /etc/cron.d
RUN chmod -R 0644 /etc/cron.d

### Timezone ###

ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

### Opcache ###

RUN docker-php-ext-install opcache
COPY ./opcache.ini /usr/local/etc/php/conf.d/opcache.ini

### Final ###

COPY ./entrypoint.sh /
ENTRYPOINT /entrypoint.sh
# Generated via generate.sh. Please don't edit directly

FROM php:7.4-fpm-alpine

ENV RUN_DEPS \
    zlib \
    libzip \
    libpng \
    libjpeg-turbo \
    postgresql-libs

ENV BUILD_DEPS \
    zlib-dev \
    libzip-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    postgresql-dev

ENV PHP_EXTENSIONS \
    opcache \
    zip \
    gd \
    bcmath \
    mysqli \
    pdo_mysql \
    pgsql \
    pdo_pgsql

ENV PECL_EXTENSIONS \
    redis

RUN apk add --no-cache --virtual .build-deps $BUILD_DEPS \
    && docker-php-ext-configure gd --with-jpeg \
    && pecl install $PECL_EXTENSIONS \
    && docker-php-ext-install -j "$(nproc)" $PHP_EXTENSIONS \
    && docker-php-ext-enable $PECL_EXTENSIONS \
    && apk del .build-deps

RUN apk add --no-cache --virtual .run-deps $RUN_DEPS

RUN mv /usr/local/bin/docker-php-entrypoint /usr/local/bin/docker-php-entrypoint-base

COPY rootfs /

RUN apk add --no-cache fcgi

# For backward compatibility
RUN ln -s /usr/local/bin/docker-php-entrypoint /usr/local/bin/php-fpm-entrypoint

ENTRYPOINT [ "docker-php-entrypoint" ]

CMD [ "php-fpm" ]

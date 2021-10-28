FROM php:8-fpm-alpine3.12

# Adding generally used extensions
RUN apk add --no-cache --virtual build-deps autoconf gcc g++ coreutils make gettext-dev icu-dev imap-dev zlib-dev libpng-dev libxml2-dev libzip-dev oniguruma-dev \
    && docker-php-ext-install intl gettext pdo_mysql gd bcmath mbstring iconv zip \
    && docker-php-ext-enable xdebug redis \
    && apk del build-deps

# Setting the correct timezone in Alpine
RUN set -xe \
    && apk --no-cache add tzdata \
    && cp /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime \
    && echo "Europe/Amsterdam" > /etc/timezone \
    && apk del tzdata

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#
# Stage 1 - Composer
#
FROM composer/composer:2-bin as composer
# end Stage 1 #

#
# Stage 2 - Prep App's PHP Dependencies
#
FROM php:8.2-fpm-alpine as phpserver

# add cli tools
RUN apk update \
    && apk upgrade \
    && apk add nginx

# silently install 'docker-php-ext-install' extensions
RUN set -x

RUN docker-php-ext-install pdo_mysql bcmath

COPY docker/nginx.conf /etc/nginx/nginx.conf

WORKDIR /var/www

COPY . /var/www/

COPY --from=composer /composer /usr/bin/composer

EXPOSE 80

COPY --link --chmod=755 docker/docker-entrypoint.sh /usr/local/bin/docker-entrypoint
ENTRYPOINT ["docker-entrypoint"]

FROM php:8.2-fpm

ARG WORKDIR=/var/www/html
ARG HOST_UID=1000

ENV COMPOSER_MEMORY_LIMIT='-1'
ENV DOCUMENT_ROOT=${WORKDIR}
ENV USER=www-data

# Install system dependencies
RUN apt-get update && apt-get install -y \
    cron \
    curl \
    git \
    libfreetype6-dev \
    libgmp-dev \
    libjpeg-dev \
    libmemcached-dev \
    libonig-dev \
    libpng-dev \
    libpq-dev \
    librdkafka-dev \
    libreadline-dev \
    libssl-dev \
    libxml2-dev \
    libzip-dev \
    nano \
    openssh-server \
    sqlite3  \
    supervisor \
    unzip \
    zip \
    && docker-php-ext-install soap \
    && docker-php-ext-install exif \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install zip \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install intl \
    && docker-php-ext-install gmp \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && pecl install memcached && docker-php-ext-enable memcached \
    && pecl install xdebug && docker-php-ext-enable xdebug \
    && pecl install redis && docker-php-ext-enable redis

#####################################
# MySQL:
#####################################

RUN docker-php-ext-install mysqli pdo pdo_mysql

#####################################
# Composer:
#####################################

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require laravel/envoy

###########################################################################
# Cleanup
###########################################################################

ADD ./laravel.ini $PHP_INI_DIR/conf.d/

RUN apt-get clean && rm -rf /var/lib/apt/lists/* \
    && usermod -u ${HOST_UID} ${USER} \
    && groupmod -g ${HOST_UID} ${USER} \
    && chmod -R 775 ${WORKDIR} \
    && chown -R ${USER}:${USER} ${WORKDIR} \
    && git config --global --add safe.directory ${WORKDIR}

EXPOSE 9000
CMD ["php-fpm"]

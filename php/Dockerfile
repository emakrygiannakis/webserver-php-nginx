FROM php:8.1-fpm

# Arguments defined in docker-compose.yml
ARG user
ARG uid

# Install system dependencies
RUN apt-get update && apt-get install -y \
    ssh \
    procps \
    bash-completion \
    vim \
    git \
    curl \
    supervisor \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    libzip-dev \
    unzip \
    cron \
    nodejs \
    npm \
    libmemcached-dev zlib1g-dev \
    imagemagick \
    libmagickwand-dev --no-install-recommends \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libjpeg-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install PHP extensions
#RUN docker-php-ext-install zip pdo_mysql mbstring exif pcntl bcmath intl
#RUN pecl install -o -f redis \
#    &&  rm -rf /tmp/pear \
#    &&  echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

#RUN pecl install -o -f memcached \
#    &&  rm -rf /tmp/pear \
#   &&  echo "extension=memcached.so" > /usr/local/etc/php/conf.d/memcached.ini

#RUN pecl install imagick \
 #   &&  echo "extension=imagick.so" > /usr/local/etc/php/conf.d/imagick.ini

# Get latest Composer
#COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Create system user to run Composer and Artisan Commands
RUN useradd -ms /bin/bash -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    mkdir -p /home/$user/.shh && \
    touch /home/$user/.shh/authorized_keys && \
    chown -R $user:$user /home/$user

USER root

COPY bashscript/start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container
COPY supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY cron/crontab /etc/cron.d/crontab

EXPOSE 8000

ENTRYPOINT ["start-container"]

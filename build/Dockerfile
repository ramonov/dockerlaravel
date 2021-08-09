FROM php:7.4-fpm
LABEL maintainer="rajshakya2000@gmail.com"

# Installing dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpng-dev \
    libonig-dev \
    libzip-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    libmcrypt-dev \
    jpegoptim optipng pngquant gifsicle \
    unzip \
    git \
    curl \
    openssl \
    gnupg2
    
# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Installing extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd  \
    --with-freetype=/usr/include/ \
    --with-jpeg=/usr/include/
RUN docker-php-ext-install gd

# Installing composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN rm -rf /var/lib/apt/lists/ && curl -sL https://deb.nodesource.com/setup_14.x | bash -

#Installing nodejs
#RUN apt-get install nodejs -y

# Allow container to write on host
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Change current user to www
USER www

# Copy existing application directory permissions
COPY --chown=www:www . /www/var

# Changing Workdir
WORKDIR /www/var

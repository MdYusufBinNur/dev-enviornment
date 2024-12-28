FROM php:8.2-fpm

# Install required system packages
RUN apt-get update && apt-get install -y \
    git \
    build-essential \
    libmcrypt-dev \
    libreadline-dev \
    zip \
    unzip \
    zlib1g-dev \
    libonig-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libevent-dev \
    libhiredis-dev \
    && apt-get clean

# Install PHP extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install pcntl

# Install Redis extension via PECL
RUN pecl install redis \
    && docker-php-ext-enable redis

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

# Set custom PHP configurations
RUN echo "post_max_size = 50M" > /usr/local/etc/php/conf.d/custom.ini

# Set the working directory
WORKDIR /var/www/html

CMD ["php-fpm"]

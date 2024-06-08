FROM php:8.1-fpm

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
    libfreetype6-dev

# Install GD extension
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"

RUN docker-php-ext-install pdo_mysql

# Set custom PHP configurations
RUN echo "post_max_size = 20M" > /usr/local/etc/php/conf.d/custom.ini

# Set the working directory
WORKDIR /var/www/html

CMD ["/usr/local/sbin/php-fpm"]

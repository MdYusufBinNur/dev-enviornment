FROM php:7.4-fpm

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php composer-setup.php \
  && php -r "unlink('composer-setup.php');" \
  && chmod +x composer.phar \
  && mv composer.phar /usr/local/bin/composer


RUN apt-get update && apt-get install -y \
    git build-essential libmcrypt-dev libreadline-dev zip unzip


RUN docker-php-ext-install pdo_mysql pcntl bcmath

#WORKDIR /var/www/app

CMD ["/usr/local/sbin/php-fpm"]


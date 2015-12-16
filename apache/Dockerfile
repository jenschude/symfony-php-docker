FROM php:5.6-apache

RUN apt-get update \
    && apt-get install -y git curl libicu-dev zlib1g-dev \
    && docker-php-ext-install intl \
    && pecl install apcu-4.0.10 \
    && docker-php-ext-enable apcu \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

RUN usermod -u 1000 www-data

RUN a2enmod rewrite

ADD sunrise.conf /etc/apache2/sites-enabled/
ADD 60-user.ini /usr/local/etc/php/conf.d/

RUN mkdir /var/www/sunrise \
    && cd /var/www/sunrise \
    && composer create-project -n --no-dev commercetools/sunrise . dev-master \
    && chown -R www-data:www-data /var/www

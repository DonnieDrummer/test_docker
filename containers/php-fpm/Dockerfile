FROM php:7.2-fpm

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils \
    gcc g++ make git autoconf tzdata openntpd libssl-dev libcurl4-openssl-dev pkg-config \
    coreutils libmcrypt-dev libxpm-dev libvpx-dev libpng-dev libxml2-dev libpq-dev

RUN docker-php-ext-install gd mbstring mysqli pdo pdo_mysql

RUN pecl install mcrypt-1.0.1 \
    && docker-php-ext-enable mcrypt

RUN docker-php-ext-configure intl \
    && docker-php-ext-configure opcache

RUN docker-php-ext-install -j$(nproc) bcmath  opcache

RUN yes | pecl install apcu xdebug-beta \
    && echo "extension=apcu.so" > /usr/local/etc/php/conf.d/apcu.ini \
    && echo "apc.enable_cli=1" >> /usr/local/etc/php/conf.d/apcu.ini \
    && echo ";zend_extension=xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=on" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=on" >> /usr/local/etc/php/conf.d/xdebug.ini

RUN curl --silent --show-error https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin/ --filename=composer && \
    composer global require hirak/prestissimo && \
    composer clear-cache

WORKDIR /var/www/application

RUN chown -R www-data:www-data /var/www/application
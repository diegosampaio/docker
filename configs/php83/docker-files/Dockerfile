FROM php:8.3.3-fpm

# Atualize o sistema e instale dependências
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libzip-dev \
    zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql mysqli zip

RUN apt-get install -y \
    libicu-dev \
    g++ \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

# Instale o Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Instale o Xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# Configurações do Xdebug
RUN echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host=host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Defina o diretório de trabalho como /var/www
# WORKDIR /var/www/html

CMD ["php-fpm"]

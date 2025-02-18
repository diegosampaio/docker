# Use a imagem base do PHP 7.4.0-fpm-alpine
FROM php:7.4.0-fpm-alpine

RUN apk add --update --no-cache \
    imagemagick-dev \
    imagemagick \
    imagemagick-libs \
    gnupg \
    vim \
    git \
    bash \
    autoconf \
    g++ \
    make \
    libzip-dev \
    libedit-dev \
    icu-dev \
    libxml2-dev \
#    libmcrypt-dev \
    # freetds \
    php7-common \
    php7-odbc \
    php7-pdo \
    freetds \
    unixodbc \
    freetype \
    libpng \
    jpeg-dev \
    libjpeg-turbo \
    freetype-dev \
    libwebp-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    libxpm-dev \ 
    php7-exif \
    postgresql-dev \
    rabbitmq-c-dev \
  &&  printf "no\n" \
   | pecl install redis-5.0.2 \
#  && printf "yes\n" \
#   | pecl install mcrypt-1.0.2 \
  && pecl install zip-1.15.5 \
  && pecl install xdebug-2.8.0 \
  && pecl install imagick \
  && pecl install amqp \
  && docker-php-ext-install gd \
  && docker-php-ext-install -j$(nproc) \
    readline \
    intl \
    soap \
    gd \
    mysqli \ 
    pgsql \
    bcmath \
    sockets \
    pcntl \
    pdo_mysql \
  && docker-php-ext-enable \
    imagick \
    redis \
 #   mcrypt \
    zip 
RUN apk --update add nginx
RUN mkdir -p /var/log/nginx && \
    touch /var/log/nginx/access.log && \
    mkdir -p /run/nginx
RUN apk add --no-cache net-tools

RUN apk add unixodbc-dev

RUN pecl channel-update pecl.php.net

RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql

RUN apk add --no-cache $PHPIZE_DEPS \
    && docker-php-ext-install calendar


RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp
RUN docker-php-ext-install gd

RUN docker-php-ext-configure pdo_odbc --with-pdo-odbc=unixODBC,/usr \
 && docker-php-ext-install pdo_odbc

RUN curl -sS https://getcomposer.org/installer | \
     php -- --install-dir=/usr/local/bin --filename=composer

# Copie os arquivos de configuração
COPY ./configs-php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY ./configs-php/php.ini /usr/local/etc/php/php.ini

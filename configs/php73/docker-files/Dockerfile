FROM php:7.3.33-fpm-alpine


RUN apk add --update --no-cache \
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
    freetype \
    libpng \
    libjpeg-turbo \
    freetype-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    postgresql-dev \
  &&  printf "no\n" \
   | pecl install redis-5.0.2 \
#  && printf "yes\n" \
#   | pecl install mcrypt-1.0.2 \
  && pecl install zip-1.15.5 \
  && pecl install xdebug-2.8.0
RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) \
    intl \
    soap \
    gd \
    mysqli \
    pgsql \
    bcmath \
    sockets \
    pcntl \
    pdo_mysql
RUN docker-php-ext-enable \
    redis \
 #   mcrypt \
    zip \
    xdebug

RUN set -ex \
  && apk --no-cache add \
    postgresql-dev

RUN docker-php-ext-install pdo pdo_pgsql

RUN curl -sS https://getcomposer.org/installer | \
     php -- --install-dir=/usr/local/bin --filename=composer
RUN pecl download mongodb-1.10.0 \
	&& tar zxf mongodb-1.10.0.tgz \
	&& rm -fr mongodb-1.10.0.tgz \
	&& cd mongodb-1.10.0 \
	&& phpize \
	&& ./configure \
		--prefix=/usr/share/php \
		--bindir=/usr/bin \
		--libdir=/usr/lib/ \
		--mandir=/usr/share/man/man1 \
		--localstatedir=/var \
		--sharedstatedir=/usr/lib/php/extensions \
		--sysconfdir=/etc/php \
		--with-config-file-path=/etc/php \
		--with-config-file-scan-dir=/etc/php/conf.d \
	&& make \
	&& make install

COPY ./configs-php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
COPY ./configs-php/php.ini /usr/local/etc/php/php.ini

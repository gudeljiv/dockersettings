FROM php:7.3-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog libxml2-dev

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl zip
RUN apt-get -y install openssl libssl-dev libxrender-dev git-core libx11-dev libxext-dev libfontconfig1-dev libfreetype6-dev fontconfig xvfb wkhtmltopdf

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Other PHP7 Extensions
RUN docker-php-ext-install pdo pdo_mysql bcmath soap mbstring exif
RUN docker-php-ext-install mysqli
# RUN apt-get -y install bcrypt

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev

# WebP support
RUN apt-get install -y \
	libwebp-dev \
	libjpeg62-turbo-dev \
	libpng-dev libxpm-dev \
	libfreetype6-dev

RUN docker-php-ext-configure gd \
	--with-gd \
	--with-webp-dir \
	--with-jpeg-dir \
	--with-png-dir \
	--with-zlib-dir \
	--with-xpm-dir \
	--with-freetype-dir

#RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 
#RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-install gd

# Enable apache modules
RUN a2enmod rewrite headers

# INSTALL IMAGIC
RUN apt-get install -y libmagickwand-dev
RUN pecl install imagick
RUN docker-php-ext-enable imagick

# symfony installer
RUN curl -sS https://get.symfony.com/cli/installer | bash

# install vim
RUN apt-get -y install vim

# install php intl
RUN apt-get install -y zlib1g-dev libicu-dev g++ \
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install intl

RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
	xz-utils \
	ca-certificates \
	xfonts-100dpi \
	xfonts-75dpi \
	xfonts-base \
	fonts-roboto \
	fonts-inconsolata \
	fontconfig \
	xorg

# install WKHTMLTOPDF
RUN apt-get update && apt-get install -y wkhtmltopdf xvfb

# ext-imap *
RUN apt-get install -y libc-client-dev libkrb5-dev && rm -r /var/lib/apt/lists/* && docker-php-ext-configure imap --with-kerberos --with-imap-ssl && docker-php-ext-install imap

# supervisor for managing workers and sockets
RUN apt-get -y update
RUN apt-get install -y supervisor
RUN docker-php-ext-install sockets

RUN apt-get install -y sendmail

RUN apt-get install -y \
	libzip-dev \
	zip \
	&& docker-php-ext-configure zip --with-libzip \
	&& docker-php-ext-install zip

# add php deployer
RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep

RUN apt-get install -y rsync
RUN apt-get install -y npm
RUN apt-get install -y ffmpeg


# Install PHP Extensions (igbinary & memcached)
# RUN apt-get update && apt-get install -y \
# 	libpq-dev \
# 	libmemcached-dev \
# 	pecl install memcached && \
# 	docker-php-ext-enable memcached

# RUN apt-get upgrade -y
# RUN apt-get install -y memcached
# RUN apt-get install -y libmemcached-dev zlib1g-dev libicu-dev
# RUN git clone -b php7 https://github.com/php-memcached-dev/php-memcached/usr/src/php/ext/memcached \
# 	&& docker-php-ext-configure /usr/src/php/ext/memcached \
# 	--disable-memcached-sasl \
# 	&& docker-php-ext-install /usr/src/php/ext/memcached \
# 	&& rm -rf /usr/src/php/ext/memcached


# RUN apt-get update \
# 	&& buildDeps=" \
# 	git \
# 	libmemcached-dev \
# 	zlib1g-dev \
# 	" \
# 	&& doNotUninstall=" \
# 	libmemcached11 \
# 	libmemcachedutil2 \
# 	" \
# 	&& apt-get install -y $buildDeps --no-install-recommends \
# 	&& rm -r /var/lib/apt/lists/* \
# 	\
# 	&& docker-php-source extract \
# 	&& git clone --branch php7 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached/ \
# 	&& docker-php-ext-install memcached \
# 	\
# 	&& docker-php-source delete \
# 	&& apt-mark manual $doNotUninstall \
# 	&& apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps

# RUN /usr/local/bin/phpize && ./configure --enable-sasl && make && make install


# start supervisor deamon
# CMD ["/usr/bin/supervisord"]
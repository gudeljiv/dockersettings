FROM php:7.2-apache

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
RUN apt-get -y install bcrypt

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
RUN wget -nv -O /tmp/wkhtmltox.deb https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb
RUN apt-get -qy install /tmp/wkhtmltox.deb
RUN cp /usr/local/bin/wkhtmlto* /usr/bin/


# ext-imap *
RUN apt-get install -y libc-client-dev libkrb5-dev && rm -r /var/lib/apt/lists/* && docker-php-ext-configure imap --with-kerberos --with-imap-ssl && docker-php-ext-install imap

# supervisor for managing workers and sockets
RUN apt-get -y update
RUN apt-get install -y supervisor
RUN docker-php-ext-install sockets

# start supervisor deamon
# CMD ["/usr/bin/supervisord"]
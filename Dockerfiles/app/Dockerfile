FROM php:7.1-apache

WORKDIR /var/www/html

RUN set -ex \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
      libmcrypt-dev mysql-client \
      libxml2-dev \
      curl \
      zip \
      unzip \
      vim \

      # For gd
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      libpng12-dev \
      libxpm-dev \
      libvpx-dev \
  && docker-php-ext-configure gd \
       --with-freetype-dir=/usr/lib/x86_64-linux-gnu/ \
       --with-jpeg-dir=/usr/lib/x86_64-linux-gnu/ \
       --with-xpm-dir=/usr/lib/x86_64-linux-gnu/ \
       --with-vpx-dir=/usr/lib/x86_64-linux-gnu/ \

  && docker-php-ext-install \
      mysqli \
      gd \
      mcrypt \
      pdo_mysql \
      mbstring \
      tokenizer \
      xml \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
  && rm -rf /var/lib/apt/lists/* \

RUN rm -rf /var/www/*

# php conf
COPY php.ini /usr/local/etc/php/

# timezone
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# apache conf
COPY apache.conf /etc/apache2/sites-enabled/000-default.conf

# apache2.conf
COPY httpd.conf /etc/apache2/apache2.conf

# apache enable module
RUN a2enmod rewrite
FROM php:7.4-fpm
COPY php/7.4/mysql.key /mysql.key
COPY php/7.4/mysql.list /mysql.list
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y gpg gpg-agent \
  && apt-key add /mysql.key \
  && rm /mysql.key \
  && mv /mysql.list /etc/apt/sources.list.d/mysql.list \
  && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y \
  && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
   libfreetype6-dev \
   libjpeg62-turbo-dev \
   libpng-dev \
   libgmp-dev \ 
   libxml2-dev \
   libzip-dev \
   libmcrypt-dev \
   libmysqlclient-dev \
   libmysqlclient21 \
   socat \
  && apt-mark manual libfreetype6 libjpeg62-turbo libpng-tools libpng16-16 libzip4 libmysqlclient21 \
  && docker-php-source extract \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-configure gmp \  
  && docker-php-ext-install -j$(nproc) \
     bcmath \
     calendar \
     exif \
     gd \
     gmp \
     mysqli \
     opcache \
     pcntl \
     pdo_mysql \
     soap \
     sockets \
     zip \ 
  && pecl install mcrypt-1.0.3 \
  && docker-php-ext-enable mcrypt \
  && docker-php-source delete \
  && apt-get purge -y \
   libfreetype6-dev \
   libjpeg62-turbo-dev \
   libpng-dev \
   zlib1g-dev \
   linux-libc-dev \
   dpkg-dev \
   libc-dev-bin \
   libgcc-8-dev \
   libzip-dev \
   gpg \
   gpg-agent \
  && apt-get autoremove -y \
  && apt-get clean all \
  && find /var/lib/apt/lists -type f -delete \
  && find /tmp /var/tmp -type f -delete
COPY common/tini-amd64 /sbin/tini
COPY php/7.4/oprid-php-manager /oprid-php-manager
RUN chmod +x /sbin/tini /oprid-php-manager && rm -f /usr/local/etc/php-fpm.d/*
COPY php/7.4/php.conf /usr/local/etc/php-fpm.d/
VOLUME /bus
ENTRYPOINT ["/sbin/tini", "/oprid-php-manager"]

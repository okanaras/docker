FROM php:8.2-fpm

RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install libzip-dev -y
RUN apt-get install zip unzip -y
RUN apt-get install -y git
RUN apt-get install -y curl

RUN apt-get install -y libxml2-dev

RUN apt-get install -y libldap2-dev

RUN apt-get install -y libgd-dev
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y libicu-dev g++

RUN apt-get install -y libfreetype6-dev
RUN apt-get install -y libpng-dev
RUN apt-get install -y libjpeg-dev
RUN apt-get install -y libjpeg62-turbo-dev

RUN docker-php-ext-configure intl && docker-php-ext-install intl
RUN docker-php-ext-configure gd --with-freetype --with-jpeg && docker-php-ext-install gd

RUN docker-php-ext-install ldap
RUN docker-php-ext-install soap
RUN docker-php-ext-install zip
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install ctype
RUN docker-php-ext-install fileinfo
RUN docker-php-ext-install pdo
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install exif
#RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install pcntl # laravel 12 icin gerekli

RUN apt-get update -y
RUN apt-get install cron -y
RUN apt-get install supervisor -y
RUN apt-get install -y nano

# composer kurulumu
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Laravel installer kurulumu
ENV COMPOSER_HOME="/root/.composer"
ENV PATH="${COMPOSER_HOME}/vendor/bin:${PATH}"
RUN composer global require laravel/installer

# nodejs & npm kurulumu
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g npm

# 135. derste eklendi. Cron jobları için
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD ["/usr/bin/supervisord", "-c","/etc/supervisor/supervisord.conf"]

RUN chown -R www-data:www-data /var/www/html/
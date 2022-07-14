FROM php:7.4-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    libonig-dev \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev

# Install extensions
RUN docker-php-ext-install pdo_mysql mbstring zip exif pcntl
RUN docker-php-ext-configure gd --enable-gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/
RUN docker-php-ext-install gd

# Add user for laravel application
# Создать группу с gid=1000(как и gid хоста) и названием www
RUN groupadd -g 1000 www
# Создать пользователя с uid=1000(как и uid хоста). -s установить оболочку пользователя /bin/bash по умолчанию
# указать группу пользователя www и дать имя пользователю www
RUN useradd -u 1000 -ms /bin/bash -g www www

# Copy existing application directory permissions
# Скопировать текущий раздел хоста в /var/www с правами www:www
COPY --chown=www:www . /var/www

# Change current user to www
# Переключиться на пользователя www
USER www

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php-fpm"]

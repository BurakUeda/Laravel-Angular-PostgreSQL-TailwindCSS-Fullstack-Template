FROM php:8.3-fpm

# Install dependencies
RUN apt-get update && apt-get install -y \
    git curl unzip zip libpng-dev libjpeg-dev libfreetype6-dev \
    libzip-dev libonig-dev libxml2-dev libicu-dev libpq-dev \
    libmagickwand-dev libexif-dev libxslt1-dev libssl-dev \
    --no-install-recommends && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install \
        pdo \
        pdo_pgsql \
        zip \
        intl \
        gd \
        bcmath \
        exif \
        xml \
        dom \
        mbstring \
        opcache && \
    pecl install imagick && docker-php-ext-enable imagick

# Install Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www

# Set permissions
RUN chown -R www-data:www-data /var/www

EXPOSE 9000
CMD ["php-fpm"]

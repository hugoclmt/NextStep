FROM php:8.3-fpm

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git unzip curl zip default-mysql-client libmariadb-dev \
    libzip-dev libpng-dev libonig-dev libxml2-dev \
    && docker-php-ext-install pdo pdo_mysql zip intl opcache


# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Define working directory
WORKDIR /var/www

# Copy application source code
COPY . .

# Install PHP dependencies
RUN composer install --no-interaction --prefer-dist --optimize-autoloader

# Set permissions for the application
RUN chown -R www-data:www-data var

# Expose port 9000 for PHP-FPM
EXPOSE 9000

# Start PHP-FPM server
CMD ["php-fpm"]

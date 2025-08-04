FROM php:8.1-apache

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip \
    curl \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    sqlite3 \
    libsqlite3-dev \
    && docker-php-ext-install pdo pdo_mysql zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Enable Apache Rewrite Module
RUN a2enmod rewrite

# Set working directory
WORKDIR /var/www/html

# Copy existing application code
COPY . /var/www/html

# Permissions
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Set Apache document root
ENV APACHE_DOCUMENT_ROOT /var/www/html/public

# Configure Apache
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
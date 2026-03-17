FROM php:8.2-apache

# Install System Dependencies
RUN apt-get update && apt-get install -y \
    libpng-dev libjpeg-dev libfreetype6-dev libzip-dev libxml2-dev \
    libmagickwand-dev ghostscript zbar-tools texlive-base unzip mariadb-client \
    && rm -rf /var/lib/apt/lists/*

# Install PHP Extensions
RUN docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd mysqli zip xml

# Install Imagick
RUN pecl install imagick && docker-php-ext-enable imagick

# Enable Apache Rewrite
RUN a2enmod rewrite

WORKDIR /var/www/html

# --- KEY CHANGE: Copy from the build context root ---
# Copies ~/XP/tcexam-deploy/source_code/tcexam -> /var/www/html
COPY source_code/ .

# Copy entrypoint from the linux folder
COPY linux/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

# Permissions
RUN chown -R www-data:www-data /var/www/html && chmod -R 755 /var/www/html

EXPOSE 80
ENTRYPOINT ["entrypoint.sh"]
CMD ["apache2-foreground"]
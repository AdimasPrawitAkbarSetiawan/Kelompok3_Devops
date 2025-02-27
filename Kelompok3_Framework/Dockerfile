# Gunakan image resmi PHP dengan Apache
FROM php:8.2-apache

# Install ekstensi yang diperlukan
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql mysqli

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Aktifkan mod_rewrite untuk Laravel & CodeIgniter
RUN a2enmod rewrite

# Atur direktori kerja
WORKDIR /var/www/html

# Salin semua file aplikasi ke dalam container
COPY . /var/www/html

# Berikan izin pada storage dan bootstrap (khusus Laravel)
RUN chmod -R 777 /var/www/html/storage /var/www/html/bootstrap/cache

# Expose port 80
EXPOSE 80

# Jalankan Apache
CMD ["apache2-foreground"]

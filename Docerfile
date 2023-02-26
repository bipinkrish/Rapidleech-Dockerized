# Use the official PHP runtime as a parent image
FROM php:7.4-apache

# Set the working directory to /app
WORKDIR /var/www/html/

# Copy the source files to the container
COPY . .
RUN chown -R www-data:www-data /var/www/html/ && \
    chmod -R 777 /var/www/html/
RUN mkdir ./files/ && chmod 777 ./files/

# Install any necessary dependencies
RUN apt-get update && \
    apt-get install -y \
        libpng-dev \
        libjpeg-dev \
        libfreetype6-dev \
        libzip-dev \
        zip \
        unzip && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd mysqli pdo pdo_mysql zip && \
    a2enmod rewrite

# Expose port 8080 for the web server
EXPOSE 8080

# Start the Apache web server
CMD ["apache2-foreground"]

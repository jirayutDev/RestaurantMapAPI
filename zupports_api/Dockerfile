FROM php:8.0-apache

# Set working directory
WORKDIR /var/www/html

# Install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends libpq-dev libcurl4-openssl-dev pkg-config libssl-dev libldap2-dev && \
    pecl install mongodb && \
    docker-php-ext-enable mongodb && \
    docker-php-ext-install pdo pdo_mysql && \
    docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap && \
    a2enmod rewrite && \
    apt-get install -y --no-install-recommends git zip unzip && \
    php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Copy application files
COPY upload.ini /usr/local/etc/php/conf.d/upload.ini
COPY vhost.conf /etc/apache2/sites-available/000-default.conf
COPY . /var/www/html

# Expose port 80
EXPOSE 80

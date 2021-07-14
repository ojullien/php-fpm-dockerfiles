FROM --platform=linux/amd64 php:7.4-fpm-alpine

LABEL Description="Fork of php:7.4-fpm-alpine"
LABEL Vendor="Olivier Jullien"
LABEL License="MIT"
LABEL Version=7.4-fpm-alpine

# Configure php
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"; \
    sed -i "s/^;security.limit_extensions =.*/security.limit_extensions = .php/g" /usr/local/etc/php-fpm.d/www.conf
COPY conf.d /usr/local/etc/php/conf.d

# Configure extensions
ARG user_extension=""
RUN curl --location --silent https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions --output /usr/local/bin/install-php-extensions \
    && chmod +x /usr/local/bin/install-php-extensions \
    && sync \
    && install-php-extensions opcache ${user_extension} \
    && rm -rf /var/cache/apk/*

# Configure network
EXPOSE 9000

# Configure source
WORKDIR /var/www

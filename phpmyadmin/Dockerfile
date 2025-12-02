FROM debian:trixie-slim

RUN apt-get update && apt-get install -y \
    apache2 \
    php \
    libapache2-mod-php \
    php-mysql \
    php-mbstring \
    php-zip \
    php-gd \
    php-json \
    php-curl \
    wget \
    unzip \
    openssl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html

ENV PMA_VERSION=5.2.1

RUN wget https://files.phpmyadmin.net/phpMyAdmin/${PMA_VERSION}/phpMyAdmin-${PMA_VERSION}-all-languages.zip \
    && unzip phpMyAdmin-${PMA_VERSION}-all-languages.zip \
    && mv phpMyAdmin-${PMA_VERSION}-all-languages/* . \
    && rm -rf phpMyAdmin-${PMA_VERSION}-all-languages.zip phpMyAdmin-${PMA_VERSION}-all-languages \
    && chown -R www-data:www-data /var/www/html

COPY entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

EXPOSE 80

ENTRYPOINT ["entrypoint.sh"]

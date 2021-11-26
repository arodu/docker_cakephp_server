FROM webdevops/php-apache:7.4

RUN apt-get update && apt-get install -y default-mysql-client

RUN apt-get update -y && \
    apt-get install -y libmcrypt-dev && \
    pecl install mcrypt-1.0.4 && \
    docker-php-ext-enable mcrypt
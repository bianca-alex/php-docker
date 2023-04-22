FROM php:8.1-fpm
LABEL name="bianca.lk.alex@outlook.com"
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak \
    && echo 'deb http://mirrors.ustc.edu.cn/debian stable main contrib non-free' > /etc/apt/sources.list \
    && echo 'deb-src http://mirrors.ustc.edu.cn/debian stable main contrib non-free ' >> /etc/apt/sources.list \
    && echo 'deb http://mirrors.ustc.edu.cn/debian stable-proposed-updates main contrib non-free' >> /etc/apt/sources.list \
    && echo 'deb-src http://mirrors.ustc.edu.cn/debian stable-proposed-updates main contrib non-free' >> /etc/apt/sources.list

RUN apt-get update && \
        apt-get install -y git \
        libfreetype6-dev libwebp-dev libjpeg-dev libpng-dev \
        zip \
        wget

RUN pecl install -o -f redis 

RUN docker-php-ext-configure gd \
        --with-jpeg=/usr/include \
        --with-freetype=/usr/include && \
    docker-php-ext-install -j$(nproc) gd \
                 pdo \
                 pdo_mysql \
                 bcmath \
                 pcntl && \
    docker-php-ext-enable \
                 redis
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer

FROM php:7.3-fpm

RUN apt-get update && apt-get install -y \
    zlib1g-dev \
    libzip-dev \
    unzip \
    vim \
    git \
    rename \
    procps \
    wget \
    openssh-client && \
    curl -s https://getcomposer.org/installer > composer-setup.php && \
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    wget https://get.symfony.com/cli/installer -O - | bash && \
    echo 'export PATH="$HOME/.symfony/bin:$PATH"' >> /root/.bashrc && \
    mv /root/.symfony/bin/symfony /usr/local/bin/symfony && \
     # php extensions
    docker-php-ext-install -j$(nproc) pdo_mysql bcmath sockets zip && \
    pecl install xdebug-2.7.2 && \
    docker-php-ext-enable xdebug && \
    apt-get remove --purge -y $BUILD_PACKAGES && rm -rf /var/lib/apt/lists/* && \
    apt-get clean;

WORKDIR /usr/share/nginx/html
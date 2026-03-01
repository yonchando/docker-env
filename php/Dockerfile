FROM php:8.4-fpm

ARG USER="web"

WORKDIR /var/www/html

# PHP Extension
ADD --chmod=0755 https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN apt-get update && apt-get install -y vim less grep nginx supervisor && \
    mkdir -p /var/log/supervisor && \
    install-php-extensions gd zip pcntl pgsql pdo_pgsql opentelemetry protobuf redis imagick

RUN groupadd -r $USER && useradd -ms /usr/bin/bash --no-log-init -r -g $USER $USER && \
    mkdir -p /home/$USER && \
    echo "alias ll='ls -la'" >> /home/$USER/.bashrc && echo "alias c='clear'" >> /home/$USER/.bashrc

COPY ./.docker/supervisor.conf /etc/supervisor/supervisord.conf
COPY .docker/supervisor /etc/supervisor/conf.d
COPY .docker/php/www.conf /usr/local/etc/php-fpm.d/www.conf
COPY .docker/nginx.conf /etc/nginx/nginx.conf
COPY .docker/php/conf.d "$PHP_INI_DIR/conf.d"

# Set permission and change config
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" && \
    mkdir -p /var/run/supervisor && \
    mkdir -p /run/nginx && \
    chown -R $USER:$USER \
    /var/www/html \
    /var/log/supervisor \
    /var/run/supervisor \
    /run/nginx \
    /var/lib/nginx \
    /var/log/nginx

EXPOSE 8000

USER $USER:$USER

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf", "-n"]

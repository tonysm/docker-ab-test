FROM madewithlove/images:php-7.1-fpm

RUN apt-get update \
    && apt-get install -y nginx curl exiftool zip unzip git supervisor sqlite3 \
    && apt-get install -y php7.1-imagick \
    && apt-get remove -y --purge software-properties-common \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

COPY default /etc/nginx/sites-available/default
COPY php-fpm.conf /etc/php/7.1/fpm/php-fpm.conf
COPY xdebug.ini /etc/php/7.1/mods-available/xdebug.ini
COPY www.conf /etc/php/7.1/fpm/pool.d/www.conf

EXPOSE 80
WORKDIR /var/www/html

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/start-container

CMD ["start-container"]

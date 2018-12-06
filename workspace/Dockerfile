FROM laradock/workspace:2.2-7.1

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

# 设置时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

# SSH
COPY insecure_id_rsa /tmp/id_rsa
COPY insecure_id_rsa.pub /tmp/id_rsa.pub

RUN if [ ! -d /root/.ssh ]; then \
    mkdir -p /root/.ssh \
;fi

RUN cat /tmp/id_rsa.pub >> /root/.ssh/authorized_keys \
    && cat /tmp/id_rsa.pub >> /root/.ssh/id_rsa.pub \
    && cat /tmp/id_rsa >> /root/.ssh/id_rsa \
    && rm -f /tmp/id_rsa* \
    && chmod 644 /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub \
    && chmod 400 /root/.ssh/id_rsa

# supervisord
RUN apt-get update
RUN apt-get install -y supervisor
COPY laravel-worker.conf /etc/supervisor/conf.d/laravel-worker.conf

RUN php -r "readfile('https://getcomposer.org/installer');" | php \
    && mv composer.phar /usr/bin/composer

RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

WORKDIR /var/www/example

CMD [ "/usr/bin/supervisord", "-n" ]

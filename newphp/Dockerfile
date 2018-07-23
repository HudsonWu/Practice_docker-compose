FROM centos:7

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"


# 修改时区
RUN ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 添加php安装所需要的yum源
RUN wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm

# 设置php版本
ARG PHP_VERSION=${PHP_VERSION}

RUN yum update -y && \
    yum -y install yum-utils && \
    yum-config-manager --enable ${PHP_VERSION}
    
# 安装php
RUN yum install -y php-cli php-fpm php-mcrypt php-mysqlnd php-gd mod_php php-pdo \
    php-pear php-xml php-xmlrpc php-mbstring php-pecl-igbinary php-opcache \
    php-pecl-redis php-bcmath php-process
    
# 检查php安装
RUN php -v | head -n 1 | grep -q "PHP"

# 全局安装composer
RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer
    
# composer中国镜像
RUN composer config -g repo.packagist composer https://packagist.phpcomposer.com

# 开启php-fpm
RUN systemctl start php-fpm



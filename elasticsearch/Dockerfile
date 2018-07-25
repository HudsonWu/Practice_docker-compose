FROM docker.elastic.co/elasticsearch/elasticsearch:6.3.2

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

USER root

# 设置时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

# 添加用户
RUN useradd elsearch -g root -p elsearch

# 解决bootstrap checks failed问题
RUN sed -i '$a \* soft nofile 65536 \n* hard nofile 131072 \n* soft nproc 2048 \n* hard nproc 4096' \
    /etc/security/limits.conf
# RUN sysctl -w vm.max_map_count=655360
RUN if [ ! -f /etc/sysctl.conf ]; then \
    touch /etc/sysctl.conf \
;fi
RUN sed -i '$a \vm.max_map_count=655360' /etc/sysctl.conf \
    && sysctl -p

RUN chown elsearch /usr/share/elasticsearch -R

USER elsearch

EXPOSE 9200 9300

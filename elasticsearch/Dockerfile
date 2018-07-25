FROM docker.elastic.co/elasticsearch/elasticsearch:6.2.3

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

USER root

RUN groupadd elsearch && \
    useradd elsearch -g elsearch -p elasticsearch

RUN sed -i '$a \* soft nofile 65536 \n* hard nofile 131072 \n* soft nproc 2048 \n* hard nproc 4096' \
    /etc/security/limits.conf

RUN chown elsearch /usr/share/elasticsearch -R

USER elsearch

EXPOSE 9200 9300

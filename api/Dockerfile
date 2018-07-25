FROM node:alpine

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

# 更改源
RUN echo http://mirrors.ustc.edu.cn/alpine/v3.6/main > /etc/apk/repositories && \
    echo http://mirrors.ustc.edu.cn/alpine/v3.6/community >> /etc/apk/repositories

# 安装基础包+配置时区
RUN apk update && apk add curl bash tree tzdata && \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

WORKDIR /usr/src/api

EXPOSE 8085

CMD [ "node", "app.js" ]

FROM node:alpine

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

# 更改源
RUN echo http://mirrors.ustc.edu.cn/alpine/v3.6/main > /etc/apk/repositories && \
    echo http://mirrors.ustc.edu.cn/alpine/v3.6/community >> /etc/apk/repositories

# 安装基础包+设置时区
RUN apk update && apk add curl bash tree tzdata && \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# 淘宝npm镜像
RUN npm install -g cnpm --registry=https://registry.npm.taobao.org

WORKDIR /usr/src/portal

RUN echo -e "#!/bin/bash\ncd /usr/src/portal && cnpm install axios \
    && cnpm install && node app.js" > /start.sh \
    && chmod +x /start.sh

EXPOSE 1338

CMD [ "/start.sh" ]

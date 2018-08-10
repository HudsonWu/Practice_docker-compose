FROM node:alpine

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

# 更改源
RUN echo http://mirrors.ustc.edu.cn/alpine/v3.6/main > /etc/apk/repositories && \
    echo http://mirrors.ustc.edu.cn/alpine/v3.6/community >> /etc/apk/repositories

# 安装基础包+设置时区
RUN apk update && apk add curl bash tree tzdata bzip2 python && \
    cp -r -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

WORKDIR /usr/src/consult

RUN echo -e "#!/bin/bash\ncd /usr/src/consult \
    && npm install chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver \
    && npm install && npm start" > /start.sh && chmod +x /start.sh

EXPOSE 8088

CMD [ "/start.sh" ]

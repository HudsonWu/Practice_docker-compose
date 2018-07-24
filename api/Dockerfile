FROM node

LABEL maintainer="wuhaishui <wuhaishui@zwehs.com>"

# 设置时区
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

# 更改源
RUN npm config set registry http://registry.npm.taobao.org/

WORKDIR /usr/src/api

EXPOSE 8085

CMD [ "node", "app.js" ]

FROM node:alpine

# Create app directory
RUN if [ ! -d /usr/src/member ]; then \
    echo "directory no found, will auto create" && \
    mkdir -p /usr/src/member \
;fi

WORKDIR /usr/src/member

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base

RUN npm install

RUN npm install -g pm2

EXPOSE 8085
CMD [ "pm2", "start", "app.js" ]

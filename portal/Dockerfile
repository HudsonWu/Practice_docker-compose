FROM node:alpine

# Create app directory
RUN if [ ! -d /usr/src/portal ]; then \
    echo "directory no found, will auto create" && \
    mkdir -p /usr/src/portal \
;fi

WORKDIR /usr/src/portal

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base

RUN npm install

RUN npm install -g pm2

EXPOSE 8085
CMD [ "pm2", "start", "app.js" ]

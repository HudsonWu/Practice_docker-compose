FROM node:alpine

# Create app directory
RUN if [ ! -d /usr/src/consult ]; then \
    echo "directory no found, will auto create" && \
    mkdir -p /usr/src/consult \
;fi

WORKDIR /usr/src/consult

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base

RUN npm install

EXPOSE 8088
CMD [ "npm", "start" ]

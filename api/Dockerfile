FROM node:10-alpine

WORKDIR /srv

ADD . .

RUN \
    apk add git python make gcc g++

RUN \ 
    yarn

EXPOSE 8000
CMD ["yarn", "start"]


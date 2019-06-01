FROM node:10-alpine

WORKDIR /srv

ADD . .

RUN \
    apk add --no-cache --virtual .build-deps \
    git python make gcc g++ \
    yarn \
    rm -rf /yarn-cache ./node_modules/.cache && \
    apk del .build-deps

EXPOSE 8000
CMD ["yarn", "start"]


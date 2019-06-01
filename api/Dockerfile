FROM node:10-alpine

WORKDIR /srv

ADD . .

RUN \ 
    yarn

EXPOSE 8000
CMD ["yarn", "start"]


FROM python:3.7-alpine

WORKDIR /srv

ADD . .

RUN \
    apk add --no-cache --virtual .build-deps \
    git python3-dev make gcc g++ && \
    mkdir -p ~/.pip && \
    cp pip.conf ~/.pip/pip.conf && \
    pip install -r requirements.txt &&\
    apk del .build-deps

EXPOSE 8001
CMD ["python", "./server.py", "-h", "127.0.0.1", "-p", "8001", "-d", "/srv/images"]


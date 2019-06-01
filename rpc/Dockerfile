FROM python:3-alpine

WORKDIR /srv

ADD . .

RUN \
    sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk add --no-cache --virtual .build-deps \
    git make gcc g++ build-base libffi-dev && \
    mkdir -p ~/.pip && \
    cp pip.conf ~/.pip/pip.conf && \
    pip install -r requirements.txt &&\
    apk del .build-deps

EXPOSE 8001
CMD ["python", "./server.py", "-h", "0.0.0.0", "-p", "8001", "-d", "/srv/images"]


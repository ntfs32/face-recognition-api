FROM python:3.6-alpine

RUN mkdir -p /root/.pip
COPY ./pip.conf /root/.pip/pip.conf

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk --update add --virtual scipy-runtime python3 py3-pip \
    && apk add --virtual scipy-build \
    build-base python3-dev openblas-dev freetype-dev pkgconfig gfortran \
    && ln -s /usr/include/locale.h /usr/include/xlocale.h \
    && pip3 install --no-cache-dir numpy \
    && pip3 install --no-cache-dir matplotlib \
    && pip3 install --no-cache-dir scipy \
    && apk del scipy-build \
    && apk add --virtual scipy-runtime \
    freetype libgfortran libgcc libpng libstdc++ musl openblas tcl tk \
    && rm -rf /var/cache/apk/*

COPY ./requirements.txt /app/requirements.txt
WORKDIR /app/

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    apk add --no-cache --virtual .build-deps gfortran cmake \
    jpeg jpeg-dev python3-dev py-pip wget freetype-dev libpng-dev \
    openblas-dev git make gcc g++ build-base libffi-dev musl-dev linux-headers && \
    # pip install -r requirements.txt && \
    pip3 install --no-cache-dir zerorpc && \
    pip3 install --no-cache-dir scipy && \
    pip3 install --no-cache-dir face_recognition && \
    apk del .build-deps

COPY ./server.py /app/server.py
EXPOSE 8001

ENTRYPOINT ["python3"]
CMD ["./server.py", "-h", "0.0.0.0", "-p", "8001", "-d", "/srv/images"]


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
RUN pip3 --version \
    && apk --no-cache --update add --virtual scipy-build \
    build-base python3-dev openblas-dev freetype-dev pkgconfig gfortran \
    && apk --no-cache --update add mariadb-dev jpeg-dev \
    make gcc g++ cmake \
    # pip3 install --no-cache-dir scipy && \
    pip3 install --no-cache-dir zerorpc && \
    pip3 install --no-cache-dir face_recognition \
    # && pip3 install --no-cache-dir -r requirements.txt \
    && apk del scipy-build \
    && rm -rf /var/cache/apk/* 

COPY ./server.py /app/server.py
EXPOSE 8001

ENTRYPOINT ["python3"]
CMD ["./server.py", "-h", "0.0.0.0", "-p", "8001", "-d", "/srv/images"]


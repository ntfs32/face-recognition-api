FROM python:3.7-alpine

WORKDIR /srv

ADD . .

RUN \ 
    pip install -r requirements.txt

EXPOSE 8001
CMD ["python", "./server.py", "-h", "127.0.0.1", "-p", "8001", "-d", "/srv/images"]


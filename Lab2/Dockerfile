FROM alpine:latest

COPY . /myapp

WORKDIR /myapp

RUN apk update && apk add python3 py3-flask

ENTRYPOINT [ "python3","routes.py" ]

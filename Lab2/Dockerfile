FROM alpine:latest

RUN apk update && apk add python3 py3-flask

COPY . /myapp

WORKDIR /myapp



ENTRYPOINT [ "python3","routes.py" ]

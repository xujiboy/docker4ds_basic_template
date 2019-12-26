FROM python:3.7.4-slim

WORKDIR /app

COPY ./requirement.txt /app/

ENV USERNAME=user1

RUN apt update && apt install -y graphviz

RUN pip --no-cache-dir install -r requirement.txt

EXPOSE 8888

VOLUME /app
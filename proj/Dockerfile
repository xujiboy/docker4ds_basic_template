FROM python:3.7.4-slim

WORKDIR /app

COPY ./requirement.txt /app/

RUN pip --no-cache-dir install -r requirement.txt

EXPOSE 8888

VOLUME /app
## base image
FROM python:3.7.4-alpine

## install dependencies
RUN apk update && \
    apk add --virtual build-deps gcc python-dev musl-dev && \
    apk add postgresql-dev && \
    apk add netcat-openbsd

## set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

## set working directory
WORKDIR /usr/src/app

## add user
RUN adduser -D user
RUN chown -R user:user /usr/src/app && chmod -R 755 /usr/src/app

## add and install requirements
RUN pip install --upgrade pip
COPY ./requirements.txt /usr/src/app/requirements.txt
RUN pip install -r requirements.txt

## add entrypoint.sh
COPY ./entrypoint.sh /usr/src/app/entrypoint.sh
RUN chmod +x /usr/src/app/entrypoint.sh

## switch to non-root user
USER user

## add app
COPY . /usr/src/app

## run server
CMD python manage.py run -h 0.0.0.0

# nginx-cachet

[![dockeri.co](http://dockeri.co/image/lgatica/nginx-cachet)](https://hub.docker.com/r/lgatica/nginx-cachet/)

[![Build Status](https://travis-ci.org/lgaticaq/nginx-cachet.svg?branch=master)](https://travis-ci.org/lgaticaq/nginx-cachet)

> Docker image for proxy of cachet with alpine


Example docker-compose-yml:

```yml
version: "2"

services:
  nginx:
    image: nginx-cachet
    ports:
      - 80:80
    links:
      - cachet
    volumes_from:
      - cachet
    depends_on:
      - cachet
  postgres:
    image: postgres:9.5
    volumes:
      - /var/lib/postgresql/data
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
  cachet:
    image: cachethq/docker:2.3.10
    expose:
      - 9000
    links:
      - postgres:postgres
    environment:
      - DB_DRIVER=pgsql
      - DB_HOST=postgres
      - DB_DATABASE=postgres
      - DB_USERNAME=postgres
      - DB_PASSWORD=postgres
    volumes:
      - /var/www
    depends_on:
      - postgres
```

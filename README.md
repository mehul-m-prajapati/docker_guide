### Basics
```
## Pull image from docker hub
$ docker pull mongo

## Pull image & run container from it
$ docker run postgres:9.6 -e POSTGRES_PASSWORD=postgres

## Run commands inside the container
$ docker exec -it testpostgres bash

## Some useful commands
$ docker ps
$ docker ps -a
$ docker logs testpostgres
$ docker network ls
$ docker network create mongo-network

## Start/Stop containers
$ docker stop mongo
$ docker start mongo
```

### Dockerfile
```
FROM node:12.18.0-alpine
LABEL author="Mehul" \
  role="developer"
WORKDIR /home/node
COPY testfile /home/node/
RUN apk update && apk add --no-cache bash python && rm -rf /var/cache/apk*
CMD ["/bin/sh"]
```

```
docker build -t myimage:1.0 .
docker image ls
docker image rm myimage:1.0
docker run --rm -it myimage:1.0
docker inspect myimage:1.0
```

### Docker Compose
```
services:
  web:
    build: .
    container_name: express-app
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    command: ["npm", "start"]
    environment:
      - NODE_ENV=development
```
```
# Start-Stop Services
$ docker-compose up
$ docker-compose down

# Detached Mode
$ docker-compose up -d

# Run service and remove container
$ docker-compose run --rm web
```


### References
- [CMD vs ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint)
- [TechWorldwithNana](https://www.youtube.com/watch?v=3c-iBn73dDE&ab_channel=TechWorldwithNana)

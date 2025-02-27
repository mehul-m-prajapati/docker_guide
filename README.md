### Basics
```
docker build -t myimage:1.0 .
docker image ls
docker image rm myimage:1.0
docker run --rm -it myimage:1.0
docker inspect myimage:1.0
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

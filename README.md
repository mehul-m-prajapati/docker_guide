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
FROM node:18

# Set working directory
WORKDIR /home/app

# Copy package files and install dependencies first (for better caching)
COPY package*.json ./
RUN npm install

COPY . .
COPY .env .

# Set the default command
CMD ["node", "app.js"]
```

```
docker build -t myimage:1.0 .
docker image ls
docker image rm myimage:1.0
docker run --rm -it myimage:1.0
docker inspect myimage:1.0
```

### Docker Compose for Mongodb
```
services:
  mongodb: # container name
    image: mongo
    ports:
      - 30000:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=test
      - MONGO_INITDB_ROOT_PASSWORD=test
    volumes:
      - mongo-data:/data/db
  mongo-express: # container name
    image: mongo-express
    ports:
      - 8081:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=test
      - ME_CONFIG_MONGODB_ADMINPASSWORD=test
      - ME_CONFIG_BASICAUTH_USERNAME=test
      - ME_CONFIG_BASICAUTH_PASSWORD=test
      - ME_CONFIG_MONGODB_SERVER=mongo

volumes:
  mongo-data:
    driver: local
```

### Docker Compose for node app
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

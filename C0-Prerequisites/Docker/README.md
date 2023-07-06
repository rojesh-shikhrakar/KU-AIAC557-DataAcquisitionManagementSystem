# [Docker](https://www.docker.com/)

Deploying applications requires us to setup the environment for the applicaiton which includes OS, databases and other applications that the applicaiton run on and their relevant configurations. Multiple steps are required, and this setup can be tedious if we have multiple services required and more so if we have to deploy the application in multiple servers. Furthermore, there can me dependency version conflicts and misunderstanding between development team and operations team. Container technology allow us to package and deploy  applications with its own isolated envionment packaged with all necessary dependencies and configurations.

Docker is an open platform for developing, shipping, testing, deploying and running applications in production quickly using containers.

## Containers

A **container is a sandboxed process** on your machine that is isolated from all other processes on the host machine. The isolation in docker leverages kernel namespaces and cgroups, features in Linux. A **container is a runnable instance of an image**   which we can create, start, stop, move, or delete using the DockerAPI or CLI. It can be run on local machines, virtual machines or deployed to the cloud, hence it is portable (on any OS) allowing it to be easily shared and reproduce a deployment environment. When running a container, it is isolated from other containers and runs its own software, binaries, dependencies, scripts, configurations and its own isolated filesystem provided by a container image.

Container Docker Registry is opensource stateless server that lets you store your docker images and distribute Docker images. We can have private repositories setup using clooud services or self-hosted services or use public repositories such as [Docker Hub](https://hub.docker.com/).

All Docker Image are build in layers with a base OS layer, usually a lightweight Linux Base and additional application layers add on top of with along with their configurations.

## Install

- Download and Install from [official Docker site](https://docs.docker.com/get-docker/)
  - Install docker desktop

## Docker usage

All commands below are called as options to the base
```docker <command> --help```

- app*  : Docker Application
- assemble* : Framework-aware builds (Docker Enterprise)
- builder : Manage builds
- cluster : Manage Docker clusters (Docker Enterprise)
- config : Manage Docker configs
- context : Manage contexts
- engine : Manage the docker Engine
- image : Manage images
- network : Manage networks
- node : Manage Swarm nodes
- plugin : Manage plugins
- registry* : Manage Docker registries
- secret : Manage Docker secrets
- service : Manage services
- stack : Manage Docker stacks
- swarm : Manage swarm
- system : Manage Docker
- template* : Quickly scaffold services (Docker Enterprise)
- trust : Manage trust on Docker images
- volume : Manage volumes

### Working with Docker Hub Repository

Pull an image (optionally specifying its version tag) from a registry

```docker pull postgres:15```

One can directly pull and run

```docker run postgres```

But before doing so checkout their [documentation page](https://hub.docker.com/_/postgres) on how to use the image, we might have to provide some configurations, password for the setup

Retag a local image with a new image name and tag

```docker tag myimage:1.0 myrepo/myimage:2.0```

Push an image to a registry

```docker push myrepo/myimage:2.0```

### Working with Docker Images

List all images that are locally stored with the Docker Engine

```docker image ls```

Delete an image from local image store

```docker image rm alpine:3.4```

Build an image from the Dockerfile in current directory and tag the image

```docker build -t myimage:1.0```

### Docker Container

Run a container from an image (alpine v3.9) with a new name (web) and expose port 5000 externally and mapped to port 80 inside the container

```docker container run --name web -p 5000:80 alpine:3.9```

List the running containers (add --all to include stopped containers)

```docker container ls```

Stop a running container through SIGTERM

```docker container stop web```

Stop a running container through SIGKILL

```docker container kill web```

Delete all running and stopped containers

```docker container rm -f $(docker ps -aq)```

Print the last 100 lines of a container’s logs

```docker container logs --tail 100 web```

## Docker Network

Docker creates its own isolated docker network where the docker containers are running. If two containers are running in the same docker network they can talk to each other using container name without using host and port, while any other application requires to access an open host and port to access it.

```docker network ls```

Create new network

```docker network create my-network```

when we run we specify the port with `-p` to open up the port

```docker run -p 27017:27017 -d mongo ...```

## Docker Compose - Build and Run Multiple Service

EG: We want to package our app that runs on mongodb.

We start by creating a docker network (Optional: we can use default network as well)

```docker network create mongo-network```

start [mongodb](https://hub.docker.com/_/mongo) and [mongo-express](https://hub.docker.com/_/mongo-express) cluster based on the configuration in the documentation

```console
 docker run -d  \
 --network mongo-network --name mongodb \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=mongoadmin \
  -e MONGO_INITDB_ROOT_PASSWORD=secret \
  mongo

docker run -d  \
    --network mongo-network --name mongo-express\
    -e ME_CONFIG_MONGODB_SERVER=mongodb \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=mongoadmin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=secret \
    -p 8081:8081  \
    mongo-express

```

Docker compose allows to combine multiple commands into a file allowing to run multiple container together that interacts with each other through a common network.

Create `docker-compose.yaml` file with following details

```docker
version: '3'
services:
  # my-app:
  # image: ${docker-registry}/my-app:1.0
  # ports:
  # - 3000:3000
  mongodb:
    image: mongo
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=mongoadmin
      - MONGO_INITDB_ROOT_PASSWORD=secret
    volumes:
      - mongo-data:/data/db
  mongo-express:
    image: mongo-express
    restart: always # fixes MongoNetworkError when mongodb is not ready when mongo-express starts
    ports:
      - 8080:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=mongoadmin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=secret
      - ME_CONFIG_MONGODB_SERVER=mongodb
volumes:
  mongo-data:
    driver: local
```

To use this file run

```docker-compose -f docker-compose.yaml up```

We can now just change this file to modify the container configuration.

### Building a docker image for an application

If we are create a node application we can create a `Dockerfile` in the root folder of our app with following content

```Docker

FROM node:20-alpine

ENV MONGO_DB_USERNAME=mongoadmin \
    MONGO_DB_PWD=secret

RUN mkdir -p /home/app

COPY ./app /home/app

# set default dir so that next commands executes in /home/app dir
WORKDIR /home/app

# will execute npm install in /home/app because of WORKDIR
RUN npm install

# no need for /home/app/server.js because of WORKDIR
CMD ["node", "server.js"]
```

To build docker image from the docker file available at "." location

```docker build -t my-app:1.0 .```

## Reference

- [Docker Hub Repository and community](https://hub.docker.com/)
- [Docker Tutorial for Beginners by TechWorld with Nana](https://www.youtube.com/watch?v=3c-iBn73dDE)

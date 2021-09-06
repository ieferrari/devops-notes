# Docker
* image run inside container,is a part of the container. for example, everthing in dockerHub
* container: running env for image, with ports



## Basic commands

to run an image you must create a container:

    docker run my_image


Stats for every container running:

    docker ps

    CONTAINER ID   IMAGE                        COMMAND                  CREATED        STATUS        PORTS                                         NAMES
    df2b73981c8a   fastapi-redis-tutorial_app   "/start-reload.sh"       33 hours ago   Up 33 hours   0.0.0.0:8080->80/tcp, :::8080->80/tcp         fastapi-redis-tutorial_app_1
    04a7638710da   redislabs/redismod           "redis-server --dir …"   33 hours ago   Up 33 hours   0.0.0.0:16379->6379/tcp, :::16379->6379/tcp   fastapi-redis-tutorial_redis_1


stop and start container:

    docker stop [container_id]
    docker start [container_id]





download image from dockerHub

    docker pull image_name

download isntall and start image, example redis:4.0

    docker run redis:4.0

run deatached  to free terminal (run in background):

    docker run -d ...

See all images in your machine:

    docker images


to specify port bindings  (this avoids port conflicts)


    docker run -p4000:5000   ...
    docker run -p[computer_port]:[container_port] ...

to specify a name for a container

    docker run --name [my_new_name] redis:4.0


### Debugging
show container running and stopped:

  docker ps -a

To check logs in a container:

    docker logs [container_id]
    docker logs [container_id] -f # keeps open waiting for more logs

get a terminal inside  a docker container:

    docker exec -it  [container_id]  /bin/bash
    docker exec -it  [container_id]  sh
    root@[container_id]# env
    [check all env variables]...
    exit




* [install docker engine](https://docs.docker.com/engine/install/#server)
* [install docker compose]( https://docs.docker.com/compose/install/#alternative-install-options)

* docker volume ls
***
## Dockerize

create a Dockerfile in the root of your project

    FROM [doker_base_image:version]

    WORKDIR /app                #cd app (inside the container)
    COPY package*.json ./
    RUN npm install
    COPY . .                     # copy everthing in the Dockerfile folder  to /app
    ENV PORT=8080
    EXPOSE 8080
    CMD ["npm", "start"]     # will run at start


create the docker image

    docker build -t  [tag_name/my_project:version]   .



now you can use this image for a base for other image or use **docker push** to upload to a repository, then download with **docker pull** , or run with  **docker run [tag_name/my_project:version]**

or run exposing ports:

    docker run -p 3000:3000 [tag_name/my_project:version]

***
## Volumes
A dedicated folder in the host (local) machine used for data persistence after you stop a container

create volume

    docker volume create [my_shared_folder]

to use the created volume

    docker run  --mount source=[my_shared_folder]

#### stop everything:

    docker kill $(docker ps -q)


    docker kill $(docker ps -q)

        delete all stopped containers with docker rm $(docker ps -a -q)
        delete all images with docker rmi $(docker images -q)
        update and stop a container that is in a crash-loop with docker update --restart=no && docker stop
        bash shell into container docker exec -i -t /bin/bash - if bash is not available use /bin/sh
        bash shell with root if container is running in a different user context docker exec -i -t -u root /bin/bash



### kill and remove every docker image

    docker system prune


***
## Docker compose
A tool to run multiple docker container at the same time, (1 process for each container)

For example:
* docker image for app
* docker image for db
* docker volume to persist data of db


create a **docker-compose.yml** file:

```yaml
version: '1'
services:
    web:
      build: .
      ports:
        - "8080:8080"
    db:
      image: "postgres"
      environment:
        POSTGRES_PASSWORD:  "my_passwd"
      volumes:
        - db-data:/some_folder

volumes:
  db-data:
```

to run everything:

    docker-compose up
    docker-compose down

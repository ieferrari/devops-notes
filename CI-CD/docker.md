* [install docker engine](https://docs.docker.com/engine/install/#server)
* [install docker compose]( https://docs.docker.com/compose/install/#alternative-install-options)

* docker volume ls


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

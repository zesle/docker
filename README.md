# docker


## Working docker

#### Build docker 
docker-compose build --no-cache

#### Run docker apps
docker-compose up -d

#### run shell into app container
docker exec -it app bash

#### Delete all containers
docker rm -f $(docker ps -a -q)

#### Delete image with hello
docker image rm --force hello

#### Delete all images
docker rmi $(docker images -q)

#### build image
docker build -t hello .

#### Run using image hello
docker exec -it app bash

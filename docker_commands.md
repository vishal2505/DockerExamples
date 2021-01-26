## To pull an image

$ docker pull nginx

Using default tag: latest
latest: Pulling from library/nginx
a076a628af6f: Pull complete 
0732ab25fa22: Pull complete 
d7f36f6fe38f: Pull complete 
f72584a26f32: Pull complete 
7125e4df9063: Pull complete 
Digest: sha256:10b8cc432d56da8b61b070f4c7d2543a9ed17c2b23010b43af434fd40e2ca4aa
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest

## To show the images available

$ docker images

REPOSITORY              TAG                 IMAGE ID            CREATED             SIZE
nginx                   latest              f6d0b4767a6c        13 days ago         133MB
postgres                9.5-alpine          5d81339a1899        17 months ago       37.7MB
hello-world             latest              fce289e99eb9        2 years ago         1.84kB
landoop/fast-data-dev   cp3.3.0             c47ed283fc24        3 years ago         930MB
itzg/elasticsearch      2.4.3               6c03a3ed19e4        3 years ago         166MB

## To run a container

$ docker run nginx:latest

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up

$ docker run -d nginx:latest

c512061ef550dcc2a388bb2c79ccdcbf36f8623e00fac4f7ddf7b37d6b14c221

(-d for  running in detach mode in background) 

## To check running container

$ docker container ls

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES

1b033890d8b0        nginx:latest        "/docker-entrypoint.…"   29 seconds ago      Up 28 seconds       80/tcp              festive_napier

docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS               NAMES

c512061ef550        nginx:latest        "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp              cranky_germain

## To stop running container
$ docker stop c512061ef550

c512061ef550

$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

## Expose Port
$ docker run -d -p 8080:80 nginx:latest

fd51ef1995d019fed8b834cd70a6701abc9abf19f6faadf315d3d3410f256bfe

$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES

fd51ef1995d0        nginx:latest        "/docker-entrypoint.…"   10 seconds ago      Up 8 seconds        0.0.0.0:8080->80/tcp   eloquent_wescoff

## To remove all the containers forcefully

$ docker ps -a -q

fd51ef1995d0
c512061ef550
f43a49470fe4
f0cddaad088e
4940f0bcfe73
7c492e99a096

$ docker rm -f $(docker ps -aq)

fd51ef1995d0
c512061ef550
f43a49470fe4
f0cddaad088e
4940f0bcfe73
7c492e99a096

$ docker ps

CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

## To name a container

$ docker run --name website -d -p 8080:80 nginx:latest

4bfdd2a3be5e60fe3e88901a223fecde4a468c254deceb9bb75d16b05c6b5f1f

$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES

4bfdd2a3be5e        nginx:latest        "/docker-entrypoint.…"   4 seconds ago       Up 2 seconds        0.0.0.0:8080->80/tcp   website

## To run a container with Volume (Host static containt from volume)

$ docker run --name website -v /Users/vishalmishra/projects/Docker/static:/usr/share/nginx/html -d -p 8080:80 nginx

70fe530fae55e3ecba0f4f0321ce9ac5e108b1d19489559acae99abfac19377b


## To share volumes between containers
$ docker run --name website2 --volumes-from website -d -p 8081:80 nginx

## Build your own image
$ docker build --tag user-service-api:latest .

(Dockerfile should be there in the current directory)

## Using Caching while building images
### Dockerfile -
FROM node:latest

WORKDIR /app

ADD package*.json ./

RUN npm install

ADD . .

CMD node index.js


while building images will get -
---> Using cache

## Reducing image size
Use Linux Alpine version of image available (tag:alpine) in docker hub.

example - docker pull nginx:alpine

## Create another tag
$ docker tag website:latest website:1

## Docker Debugging
$ docker inspect <container_id>

$ docker logs <container_id>

$ docker exec -it <container_id> /bin/bash


## To pull the spark jupyter notebook image and run the container

docker run -it -p 8888:8888 jupyter/all-spark-notebook:4.0 ipython notebook --port=8888 --ip=0.0.0.0

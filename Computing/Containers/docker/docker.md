# docker

## Manage Docker as a non-root user

https://docs.docker.com/engine/install/linux-postinstall/

```
sudo groupadd docker
sudo usermod -aG docker $USER
```

## List containers

`docker ps`  
`docker container ls`  
`docker container ls --all`  

## Get IP Address of container

`docker inspect 3038da937544 | grep IPAddress`

## Remove Containers

`docker stop 86f2a0aa6989`  
`docker rm 86f2a0aa6989`

## Manage images

`docker images`  
`docker rmi c31646140327`

### Pull an image

`docker pull docker.elastic.co/elasticsearch/elasticsearch:6.8.9`

## Create a user-defined bridge network

`docker network create web`  
`docker run -e VIRTUAL_HOST=ryanl.co.uk --rm --net web --name web-ryanl -d web-ryanl`

## Run commands inside a container

### Access container with bash shell

`docker exec -it <mycontainer> bash`

## Simple Apache Webserver

https://hub.docker.com/_/httpd

`docker build -t web-name .`
`docker run -dit --name web-name -p 8080:80 web-name`
--

 4355  docker build -t mite .
 4376  docker run --rm -it mite sh
 5157  docker run -d -p 3000:3000 grafana/grafana

 5512  docker build --tag watcher_test .

 5543  docker run --env GR_LIST -d -p 5000:5000 watcher_test
 5567  docker build --tag gr_watcher .\n
 5575  docker run --env GR_LIST -d -p 5000:5000 gr_watcher\n
 5614  docker build --tag gr_watcher .\n
 5616  docker run --env GR_LIST -d -p 5000:5000 gr_watcher\n
 5619  docker run --env GR_LIST -p 5000:5000 gr_watcher\n
 5621  docker run --env GR_LIST -p 5000:5000 gr_watcher\n
 5687  docker build --tag gr_watcher .\n
 5690  docker run --env GR_LIST -d -p 5000:5000 gr_watcher

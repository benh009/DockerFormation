# DockerFormation
## HelloWorld
### Installation 

```
docker --version
```


### HelloWorld container

```
docker run hello-world
```
* pull image de [Docker hub](https://hub.docker.com/search?q=hello-world&type=image) 
* run image

```
docker run hello-world
```
* ~~image déjà pullée~~
* run image 

Les images sur mon pc 
```
docker image ls
```
Les container qui tourne sur le pc
```
docker container ls --all
```

Os container : windows
```
docker inspect --format='{{.Os}}' hello-world
```


### Switch to docker linux

```
docker run hello-world
```
* pull image **linux** de [Docker hub](https://hub.docker.com/search?q=hello-world&type=image) 
* run image


Os container : linux.

```
docker inspect --format='{{.Os}}' hello-world
```
Comment sur un windows => VM

### webserver linux nginx

```
docker run --detach --publish 80:80 --name webserver nginx
```
80:80 port forwarding 

--name webserver (label)

image : nginx (linux)

## kitematic (UI for docker)

Download : [Kitematic](https://kitematic.com/)

* all running containers 
* create new containers
* setting containers
* documentation links
* start/stop containers

## Kubernetes

??? helloworld container
```
 docker run -it mcr.microsoft.com/windows/servercore powershell
 ```
 
 ```
 docker run -it ubuntu bash
 ```
 
 ### docker file docker-compose

linux avec python 

### exo 

https://labs.play-with-docker.com/

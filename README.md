# DockerFormation
## HelloWorld
### Installation 

#### Docker Desktop
Docker Desktop requires Windows 10 Pro or Enterprise version

[Download here](https://hub.docker.com/?overlay=onboarding)

Docker Id

login chwapiexo1 Pwd chwapiexo1


Dans le cmd de windows 
```
docker --version
```
#### Docker Toolbox 

installation de VM VirtualBox car Hyper-v Manager n'est pas sur windows non pro/Entreprise

#### autre OS 
[ubuntu](https://hub.docker.com/editions/community/docker-ce-server-ubuntu)
[Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
 #### Cloud 
 [azure](https://hub.docker.com/editions/community/docker-ce-azure)
 [aws](https://hub.docker.com/editions/community/docker-ce-aws)


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

### run command dans le container
alpine : version légère de linux
```
docker container run alpine ls -l
```
```
 docker container run -it alpine /bin/sh
```

try
```
uname -a (info marchine)
ls
```

### isolation container 
```
docker container run -it alpine /bin/ash
```
```
 echo "hello world" > hello.txt

 ls
```
```
docker container run alpine ls
```
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
 
 ### docker file docker-compose vs commit after update 

linux avec python 

### layer 


docker image history <image ID>
Using cache.

docker image inspect --format "{{ json .RootFS.Layers }}" alpine

### exo 

https://labs.play-with-docker.com/


https://training.play-with-docker.com/#dev

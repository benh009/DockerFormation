# Docker Formation
## Installation 

### Docker Desktop (Windows)
Docker Desktop requires Windows 10 Pro or Enterprise version

[Download here : hub.docker.com](https://hub.docker.com/?overlay=onboarding)

**Docker Id**

**Login** chwapiexo1 **Password** chwapiexo1


Dans le cmd de windows tester si l'installation a fonctionnée
```
docker --version
```
### Docker Toolbox 

[Download here : github.com/docker/toolbox/ ](https://github.com/docker/toolbox/releases)

Installation de VM VirtualBox car Hyper-v Manager n'est pas sur windows non pro/Entreprise

### Autre OS 
* [Ubuntu](https://hub.docker.com/editions/community/docker-ce-server-ubuntu)
* [Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
### Cloud 
 * [Azure](https://hub.docker.com/editions/community/docker-ce-azure)
 * [Aws](https://hub.docker.com/editions/community/docker-ce-aws)


## HelloWorld container

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
Les container sur le pc
```
docker container ls
```

Les container qui **tournent** sur le pc
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

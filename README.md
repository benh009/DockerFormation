# Docker Formation
## Installation 

### Docker Desktop (Windows Pro / Windows Enterprise)
*Docker Desktop require Windows 10 Pro ou Enterprise version*

[Download here : hub.docker.com](https://hub.docker.com/?overlay=onboarding)

**Docker Id**

*Besoin de créer un Docker id pour telecharger Docker Deskop*

**Login** chwapiexo1 **Password** chwapiexo1

Dans le cmd de windows tester si l'installation a fonctionnée
```
docker --version
```
### Docker Toolbox (Windows)

[Download here : github.com/docker/toolbox/ ](https://github.com/docker/toolbox/releases)

Installation de VM VirtualBox car Hyper-v Manager n'est pas sur windows non Pro/Entreprise

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
Egale à
```
docker pull hello-world
docker run hello-world
```
* Pull image de [Docker hub](https://hub.docker.com/search?q=hello-world&type=image) 
* Run image

```
docker run hello-world
```
* ~~Image déjà pullée~~
* Run image 

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
Stop docker
```
docker stop my_container
```
stop et supprime un container
```
docker rm --force linux_tweet_app
```
Os container : windows
```
docker inspect --format='{{.Os}}' hello-world
```


### Switch to Docker linux
Docker Desktop->Switch to linux docker

```
docker run hello-world
```
* pull image **linux** de [Docker hub](https://hub.docker.com/search?q=hello-world&type=image) 
* run image


Os container : linux.

```
docker inspect --format='{{.Os}}' hello-world
```
Comment un container tourne sur host windows => VM linux sur windows

### Docker Desktop setting 
* shared drive 
* Advanced

## Run command dans le container
Alpine : version légère de linux
```
docker container run alpine ls -l
```
Cmd bash dans le container linux
```
 docker container run -it alpine /bin/sh
```

Essayer les commandes suivantes 
```
uname -a (info marchine)
ls
```

## Isolation container  
Il est important de faire la difference entre une image et un container. 

L'image permet de runner un container.

Deux run de container sont bien isolés et n'ont pas d'interaction

```
docker container run -it alpine /bin/ash
```

Ecrire dans un le container 1
```
 echo "hello world" > hello.txt
 ls
```
lister fichier dans le container 2
```
docker container run alpine ls
```

## webserver linux nginx
https://training.play-with-docker.com/beginner-linux/
```
docker run --detach --publish 80:80 --name webserver nginx
```
80:80 port forwarding 

--name webserver (label)

image : nginx (linux)

## kitematic (UI for docker)
partage de volume / folder https://docs.docker.com/kitematic/userguide/

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


### Compose Swarm  
permet d'ochestrer les container entre eux 
compose sur une machine 
swarn plus puissant 

https://training.play-with-docker.com/swarm-mode-intro/#


visualisateur end of this https://training.play-with-docker.com/swarm-stack-intro/

### push image 
https://training.play-with-docker.com/beginner-linux/ end exo

 ```
  docker login
  ```
  Use docker Id 
  
 ```
export DOCKERID=chwapiexo1
echo $DOCKERID
docker image build --tag $DOCKERID/linux_tweet_app:1.0 .
docker image push $DOCKERID/linux_tweet_app:1.0
 ```

* Docker Desktop->repo 



[Pricing](https://hub.docker.com/pricing)

git pull ???


### folder partager avec host

### exo 

https://labs.play-with-docker.com/


https://training.play-with-docker.com/#dev

top exo https://training.play-with-docker.com/microservice-orchestration/

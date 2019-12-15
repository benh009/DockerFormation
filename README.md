# Docker Formation
## Introduction 
* Les conteneurs ne sont pas nouveaux. Ils sont Disponnibles depuis longtemps sur Linux/Solaris/windows
* Docker est un ensemble d'outils, d'api qui rendre les conteneurs plus facilement gérable
* Arrivé au bon moment quand l'industrie cherchait un moyen de mieux gérer le cloud
* Docker et plus qu'une trousse à outils .C'est un Ecosysteme foisonnant
* Google gère plus de deux millards de conteneurs. Exemple : gmail, maps ,search 
* Illusion d'être la seul à avoir accès au système 
* Vm illusion d'être le seul à exploiter le hardware 
* Un conteneur est très léger comparé à une vm 
* Un conteneur est plus simple à gérer pour l'équipe infrastructure


![alt text](https://github.com/benh009/DockerFormation/blob/master/vmvsdocker.jpg "Logo Title Text 1")



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

## HelloWorld container (Console App)

```
docker run hello-world
```
Egale à
```
docker pull hello-world
docker run hello-world
```
* Pull image hello-world de [Docker hub](https://hub.docker.com/_/hello-world) 
* Run image

```
docker run hello-world
```
* ~~Image déjà pullée~~
* Run image 

Liste les images sur mon pc 
```
docker image ls
```
Les container qui **tournent** sur le pc
```
docker container ls
```

Liste tout les container sur le pc
```
docker container ls --all
```

Supprime un container 
```
docker rm 8730
```
Le CONTAINER ID est spécifique à chaque instance de container et est donc différent sur votre machine. 


## HelloWorld container (Console App .net Core + asp.net Core Web App)

[.net Core Samples](https://hub.docker.com/_/microsoft-dotnet-core-samples)

Pull samples
```
docker pull mcr.microsoft.com/dotnet/core/samples
```
Run samples App .net Core
```
docker run --rm mcr.microsoft.com/dotnet/core/samples
```
* --rm supprime le container quand il est terminé

Run web App .net Core
```
docker run --detach --rm -p 8000:80 --name aspnetcore_sample mcr.microsoft.com/dotnet/core/samples:aspnetapp
```
* --name donne un nom au container
* 8000:80 Port mapping le 80000 de l'host docker =  port 80 du container
* -itd interactive pseudo terminal
* --detach detache le terminal 
Liens de l'app 
```
http://localhost:8000/ 
```

Stop docker par le nom défini dans --name
```
docker stop aspnetcore_sample
```

Stop et supprime un container
```
docker rm --force aspnetcore_sample
```

## Docker settings
### Switch vers Docker Linux ou Windows

```
docker run hello-world
```

Os container : windows
```
docker inspect --format='{{.Os}}' hello-world
```


Docker Desktop->Switch vers Linux docker/ windows

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
* Advanced seulement disponible pour la vm linux




## Run command dans le containeur
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
ps
cd
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

Ecrire dans le container 1
```
 echo "hello world" > hello.txt
 ls
```
lister fichier dans le container 2
```
docker container run alpine ls
```
le containeur 2 ne contient pas hello.txt

## Kitematic (UI for docker)


Download : [Kitematic](https://kitematic.com/)

* All running containers 
* Create new containers
* Setting containers
* Documentation links
* Start/stop containers

Guide : [lien](https://docs.docker.com/kitematic/userguide/)
 
 ## Mon containeur custom
 
 ### Commit après changement  
https://training.play-with-docker.com/ops-s1-images/
 
 ```
 docker container run -ti ubuntu bash
```
exit ubuntu 
```
docker images
```
Size : 64MB
 ```
 docker container run -ti ubuntu bash
```

Ajout d'une lib dans mon ubuntu 

[Figlet](http://www.figlet.org/)
```
apt-get update
apt-get install -y figlet
figlet "hello docker"
```

exit ubuntu

Id containeur 
```
docker container ls -a
```

```
docker container commit b6
```
Nouvelle image 
```
docker image ls
```
Ajout de tag 
```
docker image tag 268 ourfiglet
```

run cmd figlet 
```
docker container run ourfiglet figlet hello
```



 ### Docker file
 
Dockerfile 
 ```
FROM ubuntu
RUN apt-get update && apt-get install -y figlet
```
 ```
docker image build -t figlet:v0.1 .
 ```
  ```
 docker images
  ```
  ```
  docker container run figlet:v0.1 figlet hello
  ```
  Install python and call figlet hello
   ```
  FROM figlet:v0.1
RUN apt-get update && apt-get install -y python
CMD ["figlet","hello"]
 ```
```
docker image build -t figlet:v0.1 .
```
 ```
 docker images
 ```
  
  V0.1 continue à fonctionner 
   ```
    docker container run figlet:v0.1 figlet hello
 ```
  Print hello et contient python 
  ```
  docker container run figlet:v0.2 figlet hello
 ```
 
 
   ```
 docker container run -ti figlet:v0.2 bash
   ```

Lancer python dans le bash
```
python
```
 
Layer 

Image Id de figlet:v0.2
```
docker image history 58
```

Utilse la cache quand on build des nouvelles images  

  
  
 ### Docker file utilisé pour les containeurs officiel 
 
```
docker run hello-world
```
* [Docker Hub](https://hub.docker.com/_/hello-world)
* [Docker File Windows](https://github.com/docker-library/hello-world/blob/9c93e37114a7fe99b5fc0d776e0b8dff99cbbb75/amd64/hello-world/nanoserver-1809/Dockerfile)
* [Docker File Linux](https://github.com/docker-library/hello-world/blob/b715c35271f1d18832480bde75fe17b93db26414/amd64/hello-world/Dockerfile)

```
FROM scratch
COPY hello /
CMD ["/hello"]
```

super minimal images 
[scratch](https://hub.docker.com/_/scratch/)

```
docker images
```
size : 1.84kB


### Docker-compose 

db + .net core

### push image 





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


## Exercice 

* [Lab](https://labs.play-with-docker.com/) permet de ne pas devoir installer

* [Exercice ](https://training.play-with-docker.com/microservice-orchestration/)

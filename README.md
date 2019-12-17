# Docker Formation

## Agenda
* [Introduction](https://github.com/benh009/DockerFormation/blob/master/README.md#introduction)
* [Installation](https://github.com/benh009/DockerFormation/blob/master/README.md#Installation)
* [HelloWorld conteneur (Application Console)](https://github.com/benh009/DockerFormation/blob/master/README.md#helloworld-conteneur-application-console)
* [HelloWorld conteneur (Console App .net Core + asp.net Core Web App) ](https://github.com/benh009/DockerFormation/blob/master/README.md#helloworld-conteneur-application-console-net-core--application-web-aspnet-core)
* [Docker configurations](https://github.com/benh009/DockerFormation/blob/master/README.md#docker-configurations)
* [Lancer des commandes dans le conteneur](https://github.com/benh009/DockerFormation/blob/master/README.md#lancer-des-commandes-dans-le-conteneur)
* [Isolation des conteneurs](https://github.com/benh009/DockerFormation/blob/master/README.md#isolation-des-conteneurs)
* [Kitematic (UI pour Docker)](https://github.com/benh009/DockerFormation/blob/master/README.md#kitematic-ui-pour-docker)
* [Mon conteneur custom](https://github.com/benh009/DockerFormation/blob/master/README.md#mon-conteneur-custom)
* [Docker-compose ](https://github.com/benh009/DockerFormation/blob/master/README.md#docker-compose)
* [Push image ](https://github.com/benh009/DockerFormation/blob/master/README.md#push-image)
* [Exercices](https://github.com/benh009/DockerFormation/blob/master/README.md#exercices)
* [Démonstrations](https://github.com/benh009/DockerFormation/blob/master/README.md#démonstrations  )
## Introduction 
* Les conteneurs ne sont pas nouveaux. Ils sont disponibles depuis longtemps sur Linux/Solaris/Windows.
* Docker est un ensemble d'outils, d'API qui rendent les conteneurs plus facilement gérables.
* Ils sont arrivés au bon moment quand l'industrie cherchait un moyen de mieux gérer le cloud.
* Docker est plus qu'une trousse à outils. C'est un Ecosystème foisonnant.
* Google gère plus de deux milliards de conteneurs. Exemple : Gmail, Maps, Search. 
* Un conteneur a l'illusion d'être le seul à avoir accès au système. 
* Une VM a l'illusion d'être la seul à exploiter le hardware.
* Un conteneur est très léger comparé à une VM.
* Un conteneur est plus simple à gérer pour l'équipe infrastructure.


![alt text](https://github.com/benh009/DockerFormation/blob/master/vmvsdocker.jpg "")



## Installation 

### Docker Desktop (Windows Pro/Windows Enterprise)
*Docker Desktop exige Windows 10 Pro ou Enterprise version*

[Download here : hub.docker.com](https://hub.docker.com/?overlay=onboarding)

*Besoin de créer un Docker id pour telecharger Docker Deskop*

**Docker Id**
* **Login** chwapiexo1 
* **Password** chwapiexo1

Avec la commande **cmd** de windows, on peut tester si l'installation a fonctionné.
```
docker --version
```
### Docker Toolbox (Windows)

[Download here : github.com/docker/toolbox/ ](https://github.com/docker/toolbox/releases)

Installation du gestionnaire de VM VirtualBox car Hyper-v Manager n'est pas sur windows non Pro/Entreprise

### Autre OS 
* [Ubuntu](https://hub.docker.com/editions/community/docker-ce-server-ubuntu)
* [Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
### Cloud 
 * [Azure](https://hub.docker.com/editions/community/docker-ce-azure)
 * [Aws](https://hub.docker.com/editions/community/docker-ce-aws)

## HelloWorld conteneur (Application Console)

```
docker run hello-world
```
Est égale à
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
Liste les conteneurs qui **tournent** sur mon pc
```
docker container ls
```

Liste tous les conteneurs sur mon pc
```
docker container ls --all
```

Supprime un conteneur
```
docker rm 8730
```
Le CONTENEUR ID est spécifique à chaque instance de conteneur et est donc différent sur votre machine. 


## HelloWorld conteneur (Application Console .net Core + Application web asp.net Core)

[.net Core Samples](https://hub.docker.com/_/microsoft-dotnet-core-samples)

Pull samples
```
docker pull mcr.microsoft.com/dotnet/core/samples
```
Run samples App .net Core
```
docker run --rm mcr.microsoft.com/dotnet/core/samples
```
* --rm supprime le conteneur quand il est terminé

Run web App .net Core
```
docker run --detach --rm -p 8000:80 --name aspnetcore_sample mcr.microsoft.com/dotnet/core/samples:aspnetapp
```
* --name donne un nom au conteneur
* 8000:80 Port mapping => le port 80000 de l'host docker =  port 80 du conteneur
* -itd interactive pseudo terminal
* --detach détache le terminal

Lien de l'application web
```
http://localhost:8000/ 
```

Stop le conteneur docker par le nom défini dans --name
```
docker stop aspnetcore_sample
```

Stop et supprime un conteneur
```
docker rm --force aspnetcore_sample
```

## Docker configurations
### Changement vers Docker Linux ou Windows

```
docker run hello-world
```

Os conteneur : windows
```
docker inspect --format='{{.Os}}' hello-world
```

Docker Desktop->Switch vers Linux docker/ windows

```
docker run hello-world
```
* Pull image **linux** de [Docker hub](https://hub.docker.com/search?q=hello-world&type=image) 
* Run image


Os conteneur : linux.

```
docker inspect --format='{{.Os}}' hello-world
```
Comment un conteneur tourne sur une machine host Windows? => VM Linux sur Windows

### Docker Desktop configurations 
* Shared drive 
* Advanced seulement disponible pour la vm linux


## Lancer des commandes dans le conteneur
Alpine : version légère de linux
```
docker container run alpine ls -l
```
Commande bash dans le conteneur linux
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

## Isolation des conteneurs  
Il est important de faire la différence entre une image et un container. 

L'image permet de construire et lancer un conteneur.

Deux lancements de conteneur sont bien isolés et n'ont pas d'interaction.

```
docker container run -it alpine /bin/ash
```

Ecrire dans le conteneur 1
```
 echo "hello world" > hello.txt
 ls
```
Lister les fichiers dans le conteneur 2
```
docker container run alpine ls
```
Le conteneur 2 ne contient pas hello.txt

## Kitematic (UI pour Docker)


Download : [Kitematic](https://kitematic.com/)

* Liste des conteneurs qui tournent 
* Lance un nouveau conteneur
* Configuration des conteneurs
* Liens de documentations des conteneurs 
* Start/stop des conteneurs

Guide : [lien](https://docs.docker.com/kitematic/userguide/)
 
 ## Mon conteneur custom
 
 ### Faire un commit après les changements  
 Création d'un conteneur ubuntu et lancement d'un bash dans le conteneur
 ```
 docker container run -ti ubuntu bash
```
Exit ubuntu 
```
docker images
```
Size : 64MB vs ISO 2GB
 ```
 docker container run -ti ubuntu bash
```

Ajout d'une librairie dans mon conteneur Ubuntu

[Figlet](http://www.figlet.org/)
```
apt-get update
apt-get install -y figlet
figlet "hello docker"
```

Exit ubuntu

Recupère l'id du conteneur 
```
docker container ls -a
```
Commit les changements
```
docker container commit b6
```
Nouvelle image crée
```
docker image ls
```
Ajoute un tag 
```
docker image tag 268 ourfiglet
```

Run commande figlet 
```
docker container run ourfiglet figlet hello
```

 ### Docker file
 
Dockerfile 
 ```
FROM ubuntu
RUN apt-get update && apt-get install -y figlet
```
Build l'image
 ```
docker image build -t figlet:v0.1 .
 ```
  Liste les images
  ```
 docker images
  ```
  Run le conteneur
  ```
  docker container run figlet:v0.1 figlet hello
  ```
  Installation de Python et appel de figlet hello
   ```
  FROM figlet:v0.1
RUN apt-get update && apt-get install -y python
CMD ["figlet","hello"]
 ```
 Build image
```
docker image build -t figlet:v0.1 .
```
Liste les images
 ```
 docker images
 ```
  
  V0.1 continue à fonctionner 
   ```
    docker container run figlet:v0.1 figlet hello
 ```
  Print hello et contient Python 
  ```
  docker container run figlet:v0.2 figlet hello
 ```
 
 Run le conteneur
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

Utilise la cache quand on build des nouvelles images  

  
  
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


## Docker Compose 

docker-compose.yml

Permet de lancer les différents conteneurs avec leurs paramètres

Voir exercices

## Push image 
**Docker Id**
* **Login** chwapiexo1 
* **Password** chwapiexo1
 ```
  docker login
  ```
  * Nécessite un Docker Id 
  * Docker Desktop->repo 
  
 Build conteneur et Push sur [Docker hub](https://hub.docker.com/) 
 ```
docker image build --tag chwapiexo1/figlet:2.0 .
docker image push chwapiexo1/figlet:2.0
 ```
[Prix pour un repository privé](https://hub.docker.com/pricing)

Supprime l'image et pull de Docker Hub
 ```
docker rmi 582 -f
docker image pull chwapiexo1/figlet:2.0
 ```
 
## Exercices

* [Lab](https://labs.play-with-docker.com/) permet de ne pas devoir installer Docker

* [Exercice ](https://training.play-with-docker.com/microservice-orchestration/)

## Démonstrations   
### Azure 
Run le conteneur en local
 ```
docker run -p 8000:80 mcr.microsoft.com/azuredocs/aci-helloworld
```
Lien
 ```
 http://localhost:8000/
 ```
[Azure Portal]( https://portal.azure.com/#home)

Documentation : [Quickstart](https://docs.microsoft.com/en-us/azure/container-instances/container-instances-quickstart-portal) 

Pseudo : hofbauer92@gmail.com
Configuration
* Resource groups 
* Create resource
* Image docker : mcr.microsoft.com/azuredocs/aci-helloworld
* Network : Dns name => DemoContainer (liens application = dnsdemochwapi.westus.azurecontainer.io)

Voir les logging de connexion :  /Containers/logs

### Swarm  
[Lab](https://labs.play-with-docker.com/)  dans Edge

**Docker Id**
* **Login** chwapiexo1 
* **Password** chwapiexo1

Créer deux instances de machine Host Docker

Initialisation de la machine principale
```
docker swarm init --advertise-addr $(hostname -i)
```
Joindre la machine principale 
```
 docker swarm join --token SWMTKN-1-5wn8f8r8klcvqrl6ruordimf06hl3h48loo9szo11mpa34dsjn-e33ynvtrbsan70c8tiat7fs6q 192.168.0.48:2377
```
Liste les noeuds
```
docker node ls
```
Installe les services
```
docker service create -p 80:80 --name web nginx:latest
```
Curl ou click sur le lien du port dans lab
```
curl http://localhost:80
```
Lance 15 services
```
docker service scale web=15
```
Liste l'état des services 

```
docker service ps web
```

Stop le noeud 2
```
docker node update --availability drain node2
```

Liste l'état des services 
```
docker service ps web
```
Liste les noeuds
```
docker node ls
```
Active le noeud 2
```
docker node update --availability active node2
```

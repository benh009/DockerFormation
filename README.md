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

Os container
```
docker inspect --format='{{.Os}}' hello-world
```


??? helloworld container
```
 docker run -it mcr.microsoft.com/windows/servercore powershell
 ```

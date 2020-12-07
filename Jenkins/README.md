# Jenkins

## Introduction

Jenkins n'est pas disponible sur plate-forme ppc64le. Ce Dockerfile permet de créer la version ppc64le.

>Cette image est basée sur la version lts 2.249.2

Pour construire l'image : 

```bash
docker image build -t asten/jenkins:ppc64le-2.249.2 .
```

## Lancement 

```bash
docker container run -d --name jenkins -p 8080:8080 -v /Data/Apps/Jenkins:/home/jenkins  --restart always --privileged asten/jenkins:ppc64le-2.249.2
```






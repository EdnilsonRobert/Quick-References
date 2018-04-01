# Docker | Referência Rápida

- DOCs: [https://docs.docker.com/](https://docs.docker.com/)
- Hub: [https://hub.docker.com/](https://hub.docker.com/)


## Status de execução do Docker

``` bash
# Verifica se o Docker está em execução
service docker status

# Inicia a execução do Docker
service docker start
```

## Hello world

``` bash
docker run hello-world
```

## Visualizando containers

``` bash
# Visualiza todas as imagens disponíveis para execução
docker images

# Visualiza todos os containers em execução
docker ps

# Visualiza todos os containers: parados e em execução
docker ps -a
```

## Interagindo com containers

``` bash
# Cria um container mas não o inicia
docker create ubuntu

# Inicia um container de forma interativa
docker run -ti ubuntu /bin/bash
# Útil para containers que precisam de ajustes

# Inicia um container de forma daemonizada
docker run -d centos:7
# Útil quando o container não precisa de ajustes, serve apenas para consumo
```

Deixa o modo interativo mas mantém o container em execução: `CTRL+P+Q`

``` bash
# Acessa novamente um container em execução
docker attach <CONTAINER_ID>

# Encerra a execução de um container
docker stop <CONTAINER_ID>

# Inicia a execução de um container
docker start <CONTAINER_ID>

# Reinicia a execução de um container
docker restart <CONTAINER_ID>

# Pausa a execução de um container
docker pause <CONTAINER_ID>

# Despausa a execução de um container
docker unpause <CONTAINER_ID>

# Remove um container
docker rm <CONTAINER_ID>
# O container é removido mas imagem permanece no disco

# Remove uma imagem de container do disco
docker rmi <CONTAINER_ID>

# Renomeia um container
docker rename <CONTAINER_NAME> <NEW_NAME>

# Etiqueta um container
# Padrão de nome: username/image_name:version
docker tag <CONTAINER_ID> <username>/<image_name>:1.0
```

## Examinando consumo de um container

``` bash
# Examina recursos utilizados pelo container
docker stats <CONTAINER_ID>

# Examina processos em execução em um container
docker top <CONTAINER_ID>

# Recebe logs de um container
docker logs <CONTAINER_ID>
```

## Configurando memória e CPU

``` bash
# Executa um container sem configuração de memória ou CPU
docker run -ti --name teste debian
# Executa um container com configuração de memória
docker run -ti -m 512M --name teste_memo debian
# Executa um container com configuração de CPU
docker run -ti --cpu-shares 1024 --name teste_cpu debian

# Checa a quantidade de memória configurada para um container
docker inspect teste | grep -i mem
docker inspect teste | grep -i cpu
docker inspect teste_memo | grep -i mem
docker inspect teste_cpu ! grep -i cpu

# Altera configuração de memória e CPU de um container em execução
docker update -m 256M --cpu-shares 512 teste
```

## Dockerfile

``` bash
# Cria um arquivo dockerfile vazio (usar maiúscula)
> Dockerfile
```

Dockerfile
``` Dockerfile
FROM debian
MAINTAINER EdnilsonRobert
```

``` bash
# Constrói a imagem a partir do dockerfile
docker build .
```

## Docker Hub

``` bash
# Efetua login no hub.docker.com
docker login

# Envia uma imagem para o Hub
docker push <username>/<image_name>:1.0

# Busca todos os container de um usuário
docker search <username>

# Baixa uma imagem do repositório
docker pull <username>/<image_name>:1.0
```

<!--
UPDATE:
- docker load
- docker commit
-->

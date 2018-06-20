# Docker Swarm Mastery: DevOps Style Cluster Orchestration

> Build, compose, deploy, and manage Docker containers from development to DevOps based Swarm clusters

Curso en udemy.

## Section 3 - Swarm Intro y creando un swarm de 3 nodos

Utilizando play with docker creamos un swarm de 5 nodos porque podemos.

Nuestro primer servicio en swarm

```bash
# Creando un servicio alpine que haga ping al 8.8.8.8
docker service create alpine ping 8.8.8.8
# Actualizando un servicio swarm que tenga 3 replicas
docker service update <nombre del servicio> --replicas 3
# Listando los servicios
docker service ls
# Detalles del servicio
docker service ps <nombre del servicio>
# Eliminando un contenedor del servicio
docker container rm -f <nombre contenedor>
# Eliminando el servicio
docker service rm <nombre del servicio>
```

Agregar un nodo como worker o manager

```bash
# Iniciar swarm
docker swarm init
# Iniciar swarm con una ip especifica
docker swarm init --advertise-addr <ip>
# Agregar un worker al swarm
docker swarm join --token <token> <ip>
# Crear un token manager para agregar un manager al swarm
docker swarm join-token manager
# Listar nodos
docker swarm node ls
```

## Section 4 - Swarm funciones basicas y como usarlas en tu flujo de trabajo

### Overlay Network

```bash
# Crear red overlay
docker network create --driver overlay mydrupal
docker network ls
# Crear un servicio psql con la red mydrupal con password mypass de un contenedor postgres
docker service create --name psql --network mydrupal -e POSTGRES_PASSWORD=mypass postgres
docker service ls
docker service ps psql
# Crear un servicio drupal con la red mydrupal en el puerto 80:80 de un contendor drupal
docker service create --name drupal --network mydrupal -p 80:80 drupal
docker service ls
docker service ps drupal
```

### Routing Mesh

```bash
docker service create --name search --replicas 3 -p 9200:9200 elasticsearch
curl search:9200
```

### Crear una Webapp multi servicio y multi nodo

```bash
# Crear red overlay frontend y backend
docker network create --driver overlay frontend
docker network create --driver overlay backend
# Servicio redis
docker service create --name redis --network frontend redis:3.2
# Servicio db
docker service create --name db --mount type=volume,source=db-data,target=/var/lib/postgresql/data --network backend postgres:9.4
# Servicio vote
docker service create --name vote --network frontend -p 80:80 --replicas 2 dockersamples/examplevotingapp_vote:before
# Servicio worker
docker service create --name worker --network frontend --network backend dockersamples/examplevotingapp_worker
# Servicio result
docker service create --name result -p 4444:80 --network backend dockersamples/examplevotingapp_result:before
```

## Section 5 - Ciclo de vida de una Swarm App

## Section 6 - Controlando la ubicacion dentro de un swarm

## Section 7 - Operando Swarm en produccion
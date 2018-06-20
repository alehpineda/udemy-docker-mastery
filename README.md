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
docker service ps <nombre contenedor>
# Eliminando un contenedor del servicio
docker container rm -f <nombre contenedor>
# Eliminando el servicio
docker service rm <nombre del servicio>
```

## Section 4 - Swarm funciones basicas y como usarlas en tu flujo de trabajo

## Section 5 - Ciclo de vida de una Swarm App

## Section 6 - Controlando la ubicacion dentro de un swarm

## Section 7 - Operando Swarm en produccion
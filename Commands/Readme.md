# Docker Commands Reference

This repository provides a comprehensive guide to commonly used Docker commands for managing images, containers, volumes, networks, and multi-container applications.

## Table of Contents
1. [Image Management](#1-image-management)
2. [Container Management](#2-container-management)
3. [Volume Management](#3-volume-management)
4. [Network Management](#4-network-management)
5. [Dockerfile and Build](#5-dockerfile-and-build)
6. [Docker Compose](#6-docker-compose)
7. [System Cleanup](#7-system-cleanup)

---

## 1. Image Management

- `docker build -t <image-name> .`  
  Build an image from a Dockerfile in the current directory.

- `docker images`  
  List all locally stored Docker images.

- `docker pull <image-name>`  
  Download an image from a registry.

- `docker rmi <image-name>`  
  Remove a Docker image.

- `docker inspect <image-name>`  
  View detailed information about an image.

---

## 2. Container Management

- `docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>`  
  Run a container in detached mode and publish ports.

- `docker ps`  
  List running containers.

- `docker ps -a`  
  List all containers, including stopped ones.

- `docker stop <container-name>`  
  Stop a running container.

- `docker start <container-name>`  
  Start a stopped container.

- `docker restart <container-name>`  
  Restart a container.

- `docker exec -it <container-name> /bin/bash`  
  Open an interactive shell inside a running container.

- `docker logs <container-name>`  
  View logs from a container.

- `docker rm <container-name>`  
  Remove a stopped container.

- `docker inspect <container-name>`  
  View detailed information about a container.

---

## 3. Volume Management

- `docker volume create <volume-name>`  
  Create a new volume.

- `docker volume ls`  
  List all volumes.

- `docker volume inspect <volume-name>`  
  View details of a volume.

- `docker volume rm <volume-name>`  
  Remove a volume.

- `docker run -v <volume-name>:<container-path> <image-name>`  
  Mount a volume inside a container.

---

## 4. Network Management

- `docker network ls`  
  List all Docker networks.

- `docker network create <network-name>`  
  Create a custom network.

- `docker network inspect <network-name>`  
  View details of a network.

- `docker network connect <network-name> <container-name>`  
  Connect a container to a network.

- `docker network disconnect <network-name> <container-name>`  
  Disconnect a container from a network.

---

## 5. Dockerfile and Build

- `docker build -f <Dockerfile> -t <image-name> .`  
  Build an image using a specific Dockerfile.

- `docker history <image-name>`  
  Show the history of an image’s layers.

- `docker tag <image-name> <repository>:<tag>`  
  Tag an image for pushing to a registry.

- `docker push <repository>:<tag>`  
  Push an image to a registry.

---

## 6. Docker Compose

- `docker-compose up`  
  Start all services defined in `docker-compose.yml`.

- `docker-compose down`  
  Stop and remove containers, networks, and volumes.

- `docker-compose ps`  
  List containers managed by Compose.

- `docker-compose logs`  
  View logs from Compose services.

- `docker-compose build`  
  Build or rebuild services.

- `docker-compose exec <service-name> <command>`  
  Run a command inside a running service container.

---

## 7. System Cleanup

- `docker system prune`  
  Remove unused data (containers, networks, images, and build cache).

- `docker image prune`  
  Remove unused images.

- `docker container prune`  
  Remove stopped containers.

- `docker volume prune`  
  Remove unused volumes.

---


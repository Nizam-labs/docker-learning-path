# Docker Learning Repository

A hands-on repository for learning Docker and containerization. This project contains examples and explanations covering fundamental and advanced Docker concepts.

## Table of Contents
1.  [Introduction to Docker and Containerization](#introduction-to-docker-and-containerization)
2.  [Docker Architecture](#docker-architecture)
3.  [Docker Images and Containers](#docker-images-and-containers)
4.  [Docker Commands](#docker-commands)
5.  [The Dockerfile](#the-dockerfile)
6.  [Multi-Stage Builds](#multi-stage-builds)
7.  [Docker Volumes](#docker-volumes)
8.  [Docker Networking](#docker-networking)
9.  [Docker Compose for Multi-Container Applications](#docker-compose-for-multi-container-applications)

## 1. Introduction to Docker and Containerization

### What is Containerization?
Containerization is a lightweight form of virtualization that bundles an application with all its dependencies—such as code, runtime, system tools, and libraries—into a single, portable, and self-sufficient package. This allows the application to run consistently across different computing environments, from a developer's laptop to a production server.

### What is Docker?
Docker is an open-source platform that uses OS-level virtualization to develop, ship, and run applications inside containers. It provides an ecosystem of tools to manage and orchestrate containers.

## 2. Docker Architecture

Docker operates on a client-server architecture.
*   **Docker Daemon (`dockerd`):** A persistent background process that manages Docker objects like images, containers, volumes, and networks.
*   **Docker Client (`docker`):** The primary command-line tool for users to interact with Docker. The client sends commands (e.g., `docker run`) to the Docker daemon.
*   **Docker Registries:** Stores Docker images. **Docker Hub** is a public registry that is the default for Docker, but you can also host your own private registry.

*A visual diagram could be added here to illustrate the flow.*

## 3. Docker Images and Containers

### Docker Images
A Docker image is a read-only template with instructions for creating a Docker container.
*   Images are built from a `Dockerfile` and are composed of multiple layers, which improves efficiency.
*   Images are immutable, meaning they cannot be changed after they are created.

### Docker Containers
A Docker container is a runnable instance of a Docker image.
*   When a container is run from an image, a thin, writable layer is added on top of the image's read-only layers.
*   This writable layer stores any changes made to the running container. It is not persistent and is deleted when the container is removed.

## 4. Docker Commands

This section provides a quick reference for common Docker commands.

### Image Management
*   **`docker build -t <image-name> .`**: Builds an image from a `Dockerfile` in the current directory.
*   **`docker images`**: Lists all locally stored Docker images.
*   **`docker pull <image-name>`**: Downloads an image from a registry.
*   **`docker rmi <image-name>`**: Removes a Docker image.

### Container Management
*   **`docker run -d -p <host-port>:<container-port> --name <container-name> <image-name>`**: Runs a container from an image in detached mode (`-d`) and publishes ports.
*   **`docker ps`**: Lists running containers. Add `-a` to see all containers (including stopped ones).
*   **`docker stop <container-name>`**: Stops a running container.
*   **`docker start <container-name>`**: Starts a stopped container.
*   **`docker exec -it <container-name> /bin/bash`**: Opens an interactive terminal inside a running container.
*   **`docker logs <container-name>`**: Displays the logs of a container.
*   **`docker rm <container-name>`**: Removes a stopped container.

## 5. The Dockerfile

A `Dockerfile` is a text file that contains a set of instructions for building a Docker image.

**Example `Dockerfile` for a simple web application:**
```dockerfile
# Use an official Node.js runtime as the parent image
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the workdir
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Make the application's port available to the host
EXPOSE 3000

# Define the command to run the app
CMD [ "npm", "start" ]```











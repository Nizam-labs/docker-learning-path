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

<img src="https://github.com/Nizam-labs/docker-learning-path/blob/main/images/docker-arch.png" width=50% height=50% />

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
CMD [ "npm", "start" ]
```


## 6. Multi-Stage Builds

Multi-stage builds are a powerful feature in Docker that allow you to use multiple FROM statements in a single Dockerfile. This helps optimize the final image by separating the build environment from the runtime environment.

Benefits

- Reduces image size by excluding build tools and intermediate files.
- Improves security and performance.
- Enables reuse of build artifacts across stages.

**Example `Multi stage build` with sample asp.net core web application:**
```dockerfile
# Stage 1: Build the application
# Use the full .NET SDK image for building.
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy the project file first for caching.
COPY WebApp.csproj .
RUN dotnet restore

# Copy the rest of the application code.
COPY . .

# Publish the application.
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Create the final, smaller runtime image
# Use the ASP.NET Core runtime image.
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy the published application from the 'build' stage.
COPY --from=build /app/publish .

# Expose port 80.
EXPOSE 80

# Define the command to run the application.
ENTRYPOINT ["dotnet", "WebApp.dll"]
```

## 7. Docker Volumes

Docker volumes are used to persist data generated by and used by Docker containers.

**Key Features**

- Volumes are stored outside the container filesystem.
- They survive container restarts and removals.
- Ideal for databases, logs, and user-generated content.

## 8. Docker Networking

Docker provides several networking drivers to connect containers:

**Types of Networks**

- **Bridge**: Default network for containers on a single host.
- **Host**: Shares the host's network stack.
- **Overlay**: Enables communication between containers across multiple Docker hosts.
- **None**: Disables networking.

**Useful Commands**

- docker network ls: List available networks.
- docker network create &lt;network-name&gt;: Create a custom network.
- docker network inspect &lt;network-name&gt;: View network details.
- docker network connect &lt;network-name&gt; &lt;container-name&gt;: Connect a container to a network.

## 9. Docker Compose for Multi-Container Applications

Docker Compose is a tool for defining and running multi-container Docker applications using a docker-compose.yml file.

**Benefits**

- Simplifies container orchestration.
- Supports service dependencies.
- Easy to scale and manage.








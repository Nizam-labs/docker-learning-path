# Docker Networking

Docker networking facilitates communication between Docker containers, the Docker host, and the external world. It provides isolated network environments for each container, enabling them to have their own IP addresses and network interfaces.

## Key Concepts and Network Types

### Default Bridge Network (docker0)

- - Automatically created upon Docker installation.
    - New containers are attached to this network by default unless specified otherwise.
    - Containers within the same bridge network can communicate with each other via their IP addresses.

### User-defined Bridge Networks

- - Created explicitly by users for specific applications or groups of containers.
    - Offer automatic service discovery, allowing containers to communicate by service names instead of IP addresses.
    - Provide better isolation and organization for multi-container applications.

### Host Network

- - Removes network isolation between the container and the host.
    - Containers on the host network share the host's network stack, including its IP address and routing table.
    - Eliminates the need for port mapping, as containers directly use the host's ports.

### None Network

- - Containers attached to this network have no network interfaces, effectively isolating them from all network communication.
    - Suitable for containers that do not require any network access.

### Overlay Networks

- - Used in Docker Swarm mode for communication between containers running on different Docker hosts in a cluster.
    - Enables distributed applications to communicate seamlessly across multiple machines.

### Macvlan Networks

- - Allow containers to be assigned a MAC address, making them appear as physical devices on the network.
    - Provides direct network connectivity to the underlying physical network.

## Communication and Port Publishing

- Containers within the same user-defined network can communicate by service name.
- To allow external access to a container's services, ports must be "published" or "exposed" from the container to the host using the -p or --publish flag during container creation or in a docker-compose.yml file.

**Example of Creating a User-Defined Bridge Network:**

```Code
docker network create my_custom_network
```
**Example of Running a Container on a User-Defined Network:**

```Code
docker run -d --name my_app --network my_custom_network my_image
```

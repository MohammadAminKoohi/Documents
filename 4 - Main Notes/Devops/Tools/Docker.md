
2024-08-18 15:01

Status:

Tags: #Backend #Devops 

# Docker


Docker is a platform designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all parts it needs, such as libraries and other dependencies, and ship it all out as one package.

---

## Basic Docker Commands

### Running Containers
```bash
docker run [OPTIONS] [container]:[tag]
```
- **-d** : Run in detached mode (background)
- **-i** : Interactive mode (keeps STDIN open)
- **-t** : Allocate a pseudo-TTY (terminal)
- **-p** : Map container port to the host (e.g., `-p 8080:80`)
- **-v** : Bind mount a volume (e.g., `-v /host_dir:/container_dir`)
- **-e** : Set environment variable (e.g., `-e ENV_VAR=value`)
- **-f**  :  
- **--mount** : Mount storage with more control (e.g., `--mount type=bind, source="/host_dir", target="/container_dir"`)
- **--link** : Link to another container (e.g., `--link container_name:alias`)

### Managing Containers
- **docker ps** : List running containers
  - **-a** : Show all containers (including stopped ones)
- **docker stop [container]** : Stop a running container
- **docker rm [container]** : Remove a stopped container
- **docker commit [container id]  [name] :[version]** : create a new image from the container mentioned


### Managing Images
- **docker images** : List all images
- **docker rmi [image]** : Remove an image
- **docker pull [image]** : Download an image from Docker Hub

### Executing Commands in Containers
- **docker exec [container]  [command]** : Run a command inside a running container
- **docker attach [container]** : Attach to a running container (connect your terminal to it)

### Inspecting and Viewing Logs
- **docker inspect [container]** : Return detailed information about a container in JSON format
  - Includes environment variables, network settings, and more
- **docker logs [container]** : View the logs of a container

---

## Entrypoint and CMD

### ENTRYPOINT
```Dockerfile
ENTRYPOINT ["program"]
```
- **ENTRYPOINT** defines a command that will always run when the container starts.
- Anything specified in the command line will be appended to the ENTRYPOINT.
- Use ENTRYPOINT when you want your container to run as an executable.

### CMD
```Dockerfile
CMD ["command", "arg1", "arg2"]
```
- **CMD** provides default arguments for the ENTRYPOINT if none are provided in the command line.
- If ENTRYPOINT is not specified, CMD is the primary command run by the container.

---

## Docker Networks

When a Docker container is created, Docker automatically creates three default networks:
1. **bridge** (default)
2. **none**
3. **host**

### Bridge Network
- A private internal network created by Docker on the host.
- Containers attached to this network are assigned an IP address in the `172.17.x.x` range.
- To access these containers externally, you need to map their ports to the host using the `-p` flag.
- Example:
  ```bash
  docker run -d -p 8080:80 nginx
  ```

### Host Network
- Removes the network isolation between the container and the Docker host.
- The container will share the host’s network stack, meaning it will use the host’s IP address.
- **Note:** You cannot run multiple containers that listen on the same port with this network mode.

### None Network
- The container is completely isolated with no network access.
- Used for specialized tasks where network isolation is required.

---

## Docker Compose

Docker Compose allows you to define and manage multi-container Docker applications. It uses a YAML file to configure your application's services.

### Basic Docker Compose Format

```yaml
version: '3'
services:
  service_name:
    image: [image_name]
    build: [build_context]
    ports:
      - "5000:5000"
    links:
      - [other_service]
    networks:
      - [network_name]

networks:
  [network_name]:
```

### Common Docker Compose Commands
- **docker-compose up** : Start all services defined in `docker-compose.yml`.
- **docker-compose down** : Stop and remove containers, networks, images, and volumes created by `docker-compose up`.

---

## Example Commands

### Running a Local Docker Registry
```bash
docker run -d -p 5000:5000 --name registry registry:2
```

### Tagging an Image for the Local Registry
```bash
docker image tag my-image localhost:5000/my-image
```

---

## Docker Engine Architecture

Docker Engine consists of three main components:
1. **Docker CLI**: Command-line interface to interact with Docker.
2. **REST API**: API that allows programs to communicate with the Docker daemon.
3. **Docker Daemon**: Background process that manages Docker containers, images, networks, and storage.

### Namespaces
Docker uses Linux namespaces to provide the isolation that containers need. There are several types of namespaces Docker uses:
- **PID Namespace**: Provides process isolation.
- **Network Namespace**: Provides network isolation.

### Docker Engine Workflow
1. **Docker CLI** sends commands to the Docker daemon.
2. **Docker Daemon** interacts with the OS kernel and manages containers.
3. **REST API** allows other programs to communicate with Docker to automate tasks.





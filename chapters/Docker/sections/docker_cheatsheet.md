# Docker Cheatsheet

## General

Start the docker daemon
```bash
docker -d
```

Get help with Docker. Can also use –help on all subcommands
```bash
docker --help
```

Display system-wide information
```bash
docker info
```

## Docker Hub

https://hub.docker.com

Login into Docker
```bash
docker login -u <username>
```

Publish an image to Docker Hub
```bash
docker push <username>/<image_name>
```

Search Hub for an image
```bash
docker search <image_name>
```

Pull an image from a Docker Hub
```bash
docker pull <image_name>
```

## Images

Build an Image from a Dockerfile
```bash
docker build -t <image_name> 
```

Build an Image from a Dockerfile without the cache
```bash
docker build -t <image_name> . –no-cache 
```

List local images
```bash
docker images 
```

Delete an Image
```bash
docker rmi <image_name> 
```

Remove all unused images
```bash
docker image prune
```

## Containers

Create and run a container from an image, with a custom name:
```
docker run --name <container_name> <image_name>
```

Run a container with and publish a container’s port(s) to the host.
```
docker run -p <host_port>:<container_port> <image_name>
```

Run a container in the background
```
docker run -d <image_name>
```

Start or stop an existing container:
```
docker start|stop <container_name> (or <container-id>)
```

Remove a stopped container:
```
docker rm <container_name>
```

Open a shell inside a running container:
```
docker exec -it <container_name> sh
```

Fetch and follow the logs of a container:
```
docker logs -f <container_name>
```

To inspect a running container:
```
docker inspect <container_name> (or <container_id>)
```

To list currently running containers:
```
docker ps
```

List all docker containers (running and stopped):
```
docker ps --all
```

View resource usage stats
```
docker container stats
```

### Docker Notes

#### Docker Engine
- Docker CLI
- Docker Daeomon
- REST API

REST API is used to interact with the docker daemon.
Docker CLI need not be on the same host

```
docker -H=remote-docker-engine:2375
docker -H=10.123.15.14:2375 run nginx
```

#### Namespaces

Docker uses namespaces to isolate workspaces.
Isolation in containers achieved via, namespaces for,

- Process ID
- Network
- Interprocess comm
- Mount
- Unix Time sharing

#### Cgroups

Docker uses cgroups to control resources allocated to each container.

``` 
# 50 percent sharing
docker run --cpus=.5 ubuntu
docker run --memory=100m
```

Run container in background

```
docker run -d --rm -p 8888:8080 tomcat:8.0
docker ps
# Run command inside container
# List all processes in that container
docker exec DOCKERID ps -eaf 
```

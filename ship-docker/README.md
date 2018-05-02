
#### Docker notes

- We have a docker daemon running in the background that provides REST API
and ability to control lifecycle of containers.

#### Docker Compose

- Starting, stopping containers
- Container communication
- Shared volumes

#### Docker Machine

- Used to spin up servers in a cloud of your choice or locally on vagrant
virtual machines (makes those cloud interactions as if they were taking place
locally)

#### Docker Commands

```
docker ps
docker ps -a -> shows stopped containers as well
```

We can start a container from an image.

```
docker images
```

##### Run a new container

Get Ubuntu image and run a container of it - also run a command

```
docker run ubuntu:16.04 ls -lah
```

##### Inspecting Docker Containers

```
docker inspect <CONTAINER_ID>
docker inspect 793728d13f76
```

Formatting Inspection data

```
docker inspect --format="{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" <CONTAINER_NAME/CONTAINER_ID>
docker inspect --format="{{range .NetworkSettings.Networks}}{{.NetworkID}}{{end}}"
```

##### Inspection via jq

```
docker inspect <CONTAINER_ID/CONTAINER_NAME> | jq -r '.[0].NetworkSettings.SandboxKey'
```

```
Note: Every time you run the container, a new container is created, using the same image
```

##### Remove Container

```
docker rm <CONTAINER_NAME/CONTAINER_ID>
```

##### Docker Container IDs

```
docker ps -aq
```

Now remove all of them,

```
docker rm $(docker ps -aq)
```


##### Remove the container when its done with the action

```
docker run --rm ubuntu:16:04 echo "hello world"
```

##### Remove Docker images

```
docker images
# Show Image ids
docker images -q

docker rmi $(docker images -q)
```

##### Interacting with a spun up Container

```
# This will exit immediately
docker run ubuntu:16.04 bash

# Run interactive mode
docker run -it ubuntu:16.04 bash

# Start a container
docker start <CONTAINER_ID>
# Interactive mode start
docker start -i <CONTAINER_ID>
# Stop a container
docker stop <CONTAINER_ID>
```

##### Make a useful Docker Container

```
# Spin up container
docker run -it ubuntu:16:04 bash

# Update
apt-get update

# Install nginx
apt-get install -y nginx
which nginx
nginx
OR
service nginx start
```

Try curl <Network_IP_OF_CONTAINER>

Open up local computer to speak to this container

```
# Port 80 on host should go to port 80 on container
docker run -it -p 80:80 ubuntu:16.04 bash
apt-get install -y nginx


curl localhost
or go to browser and type localhost to see nginx welcome page
```

##### Make nginx server our files

```
mkdir dockertest
cd dockertest
touch index.html

# v flag is for volumes
# Share contents of current dir - to where in container
docker run -it -p 80:80 -v .:/var/www/html ubuntu:16:04 bash
# Sharing can also use complete path
docker run -it -p 80:80 -v ~/dockertest:/var/www/html ubuntu:16:04 bash
# Inside container
apt-get update && update-get install -y nginx
```

```
cat /etc/nginx/sites-available/default

cd /var/www/html
cat index.html
```


##### Create a reusable container

```
docker run -it ubuntu:16:04 bash
apt-get update && apt-get -y nginx
```

```
docker ps -a
```

##### Docker diff of a container

Show changes to container in relation to base image used.

```
docker diff <CONTAINER_NAME>
```

##### Docker commit changes for a new image

So,
- You take an image
- Build a container off of it
- Make changes to container
- Get a diff of changes, `docker diff CONTAINER_NAME`
- Commit changes so we can built a new Image

```
docker commit -h
```

```
docker ps -a
docker commit -a "Mani" -m "Installed nginx" <CONTAINER_NAME>
docker commit -a "Mani" -m "Installed nginx" manitestcontainer/nginx:0.1.0

# Get images
docker images
```

##### Use above container

```
cd dcker
echo "Hello mani" > index.html
# Share current directory with html container, use the image we just made
# and run nginx command
docker run -it -p 80:80 -v $(pwd):/var/www/html manitestcontainer/nginx:0.1.0 nginx

However this container will make a change and exit because docker uses daemon to
run processes in background
```

```
docker run -it -p 80:80 -v $(pwd):/var/www/html manitestcontainer/nginx:0.1.0 bash
# Tell nginx to run in the foreground
echo "daemon off;" >> /etc/nginx/nginx.conf
```

Now lets save the config,
```
docker diff <CONTAINER_NAME>
docker commit -a "Mani" -m "nginx runs in foreground" <CONTAINER_NAME> manitestcontainer/nginx:0.2.0
```

##### Run container and serve content

```
docker run -it -p 80:80 -v $(pwd):/var/www/html manitestcontainer/nginx:0.2.0 nginx
```

##### Run container and server content in detached mode
```
# Detach so it doesnt hang on spinning it up
docker run -d -it -p 80:80 -v $(pwd):/var/www/html manitestcontainer/nginx:0.2.0 nginx
docker ps
```

##### Docker history

```
docker history manitestcontainer/nginx:0.2.0
```

#---------------------------------------------------------------------------------------

##### Dockerfile

```
mkdir nginx
cd nginx
vim Dockerfile
```

```
FROM ubuntu:16:04

MAINTAINER Mani

RUN apt-get update && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

CMD ["nginx"]
```

Note:
- Dockerfile commits just like the commit command

```
# Look for dockerfile in current directory
docker build -t manitestdocker/nginx:0.1.0 .
# Run in detached mode
docker run -d -p 80:80 -v $(pwd)/../:/var/www/html manitestcontainer/nginx:0.1.0
# If you want to retag
docker run -d -p 80:80 -v $(pwd)/../:/var/www/html manitestcontainer/nginx:0.2.0
```

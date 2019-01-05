# Docker commands

### Show Commands

#### Docker version
```sh
$ docker version
```

#### Show info like number of containers, etc
```sh
$ docker info
```

## Working with containers
##### About Containers
Docker containers are often compared to virtual machines but they are actually just processes running on your host os. In Windows/Mac, Docker runs in a mini-VM so to see the processes you will need to connect directly to that. On Linux run "ps aux" and see the processes directly.
#### Create and run a container in foreground
```sh
$ docker container run -it -p 80:80 nginx
```
#### Create and run a container in background
```sh
$ docker container run -d -p 80:80 nginx
```
#### Naming Containers
```sh
$ docker container run -d -p 80:80 --name nginx-server nginx
```
- Looked for image called nginx in image cache
- If not found in cache, it looks to the default image repo on Dockerhub
- Pulled it down (latest version), stored in the image cache
- Started it in a new container
- We specified to take port 80- on the host and forward to port 80 on the container
- We can specify versions like "nginx:1.09"

#### List running Containers
```sh
$ docker container ls
```
#### List all Containers (includes not running)
```sh
$ docker container ls -a
```
#### Stop Container
```sh
$ docker container stop <ID>
```
#### Stop all running Containers
```sh
$ docker stop $(docker ps -aq)
```
#### Remove Container
###### can't remove running containers, must stop first
```sh
$ docker container rm <ID>
```
#### Remove running Container forcefully
```sh
$ docker container rm -f <ID>
```
#### Remove multiple Containers
```sh
$ docker container rm <ID> <ID> <ID>
```
#### Remove all Container
```sh
$ docker rm $(docker ps -aq)
```
#### Get logs
##### use name or ID
```sh
$ docker container logs <NAME>
```
#### List processes running in Container
```sh
$ docker container top <NAME>
```
## Image Commands
##### About Images
- Images are app bianaries and dependencies with meta data about the image data and how to run the image
- Images are no a complete OS. No kernel, kernel modules (drivers)
- Host provides the kernel, big difference between VM
#### List images pulled
```sh
$ docker image ls
```
#### Pull an image
```sh
$ docker pull <image>
```
#### Remove an image
```sh
$ docker image rm <image>
```
#### Remove all images
```sh
$ docker rmi $(docker images -a -q)
```
## Sample container creation
NGINX:
```sh
$ docker container run -d -p 80:80 --name nginx nginx (-p 80:80 is optional as it runs on 80 by default)
```
APACHE:
```sh
$ docker container run -d -p 8080:80 --name apache httpd
```
MONGODB:
```sh
$ docker container run -d -p 27017:27017 --name mongo mongo
```
MYSQL:
```sh
$ docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql
```
## Container info

### View info on container
```sh
$ docker container inspect <NAME>
```
### View Specific property (--format)
```sh
$ docker container inspect --format '{{ .NetworkSettings.IPAddress }}' <NAME>
```
### View Performance stats (cpu, mem, network, disk, etc)
```sh
$ docker container stats <NAME>
```

## Accessing Container
### Create new nginx container and bash into
```sh
$ docker container run -it --name <NAME> nginx bash
```
- i = interactive Keep STDIN open if not attached
- t = tty - Open prompt

### Run/Create Ubuntu container
```sh
$ docker container run -it --name ubuntu ubuntu
```
(no bash because ubuntu uses bash by default)
### You can also make it so when you exit the container does not stay by using the -rm flag
```sh
$ docker container run --rm -it --name <NAME> ubuntu
```
### Access an already created container, start with -ai
```sh
$ docker container start -ai ubuntu
```
### Use exec to edit config, etc
```sh
$ docker container exec -it mysql bash
```

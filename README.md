# Docker commands

### Show Commands
#### show Docker version
```sh
$ docker version
```

#### Show info like number of containers, etc
```sh
$ docker info
```

### Working with containers
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
#### List processes running in container
```sh
$ docker container top <NAME>
```

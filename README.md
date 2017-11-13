# Docker Setup
## Installation
1. Download docker toolbox
2. Copy `images/boot2docker.iso` to `c:/users/[user]/.docker/machine/cache`

## Add Console for ConEMU
1. Go to "Settings" menu.
2. Select "Startup > Tasks"
3. Click on "+" button to add new task.
4. Provide name as "Docker"
5. Set value text area with:

```
"-new_console:d:C:\Program Files\Docker Toolbox" "%ConEmuDrive%\Program Files\Git\bin\bash.exe" --login -i "C:\Program Files\Docker Toolbox\start.sh"
```

## Test Setup
Run `docker run hello-world`.  After a while, you should see a message "Hello from Docker!".  There is a delay because it needs to download the **hello-world** package from the remote location.  Subsequent invocations will display the response immediately.

## Build and run test package
1. build the image: `docker build -t friendlyhello .`
2. run the container: `docker run -p 4000:80 friendlyhello`

### Detached Mode
`docker run -d -p 4000:80 friendlyhello`

### Commands
Command                                                   | Description                             |
----------------------------------------------------------|-----------------------------------------|
`docker ps`                                               | List containers                         |
`docker ps -a`                                            | List all containers                     |
`docker container ls`                                     | List containers                         |
`docker images`                                           | List images                             |
`docker stop <containerName>`                             | stop container                          |
`docker login`                                            | login to docker cloud                   |
`docker <tag> <image> <username>/<repository>:<tag>`      | tag repository                          |
`docker image rm <imageID>`                               | remove image                            |
`docker image rm <imageID> --force`                       | remove image (forced)                   |
`docker update --restart=no $(docker container ls -a -q)` | Remove auto-restart from all containers |

Command                                            | Description                                           |
---------------------------------------------------|-------------------------------------------------------|
`docker build -t <friendlyname> .`                 | Create image using this directory's Dockerfile        |
`docker run -p 4000:80 <friendlyname>`             | Run "friendlyname" mapping port 4000 to 80            |
`docker run -d -p 4000:80 <friendlyname>`          | Same thing, but in detached mode                      |
`docker container ls`                              | List all running containers                           |
`docker container ls -a`                           | List all containers, even those not running           |
`docker container stop <hash>`                     | Gracefully stop the specified container               |
`docker container kill <hash>`                     | Force shutdown of the specified container             |
`docker container rm <hash>`                       | Remove specified container from this machine          |
`docker container rm $(docker container ls -a -q)` | Remove all containers                                 |
`docker image ls -a`                               | List all images on this machine                       |
`docker image rm <image id>`                       | Remove specified image from this machine              |
`docker image rm $(docker image ls -a -q)`         | Remove all images from this machine                   |
`docker login`                                     | Log in this CLI session using your Docker credentials |
`docker tag <image> username/repository:tag`       | Tag <image> for upload to registry                    |
`docker push username/repository:tag`              | Upload tagged image to registry                       |
`docker run username/repository:tag`               | Run image from a registry                             |

### Determine local machine IP
`docker-machine ip default`

## Docker Swarm
`docker swarm init --advertise-addr $(docker-machine ip default)`

### deploy compose
`docker stack deploy -c docker-compose.yml getstartedlab`

### netcat
`docker run --net=host -ti ubuntu:14.04 bash`

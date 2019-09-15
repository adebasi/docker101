# Docker commands

## Images

Working with Docker, normally everything starts with an image which is required to start a container. This is where [Docker-Hub](hub.docker.com) comes into play. Docker-Hub provides lots of images to download. Some images are official like `nginx` and some are user generated like `adebasi/pingpong`.

Go ahead and download `nginx`:

`$ docker pull nginx`

All downloaded images can be listed by:

`$ docker images`

## Container

Images are immutable and readonly. When starting a container, Docker adds a read/write layer on top of these immutable layers, so processes in the container can write files.

Let's start a container:

`$ docker run -d nginx`

`-d` starts the container in the background

To see all running containers execute:

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
7401b15512dd        nginx               "nginx -g 'daemon of…"   3 seconds ago       Up 1 second         80/tcp              funny_hopper
```

You can see that the nginx is running and it is listening on Port 80, but `curl localhost:80` won't work. You have to forward the containers port in order to access it locally.

`$ docker run -d -p 8080:80 nginx`

Now you can `curl localhost:8080` to see the nginx welcome site.
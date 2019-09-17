# Container composition with `docker-compose`

We used only single containers so far. But most web applications require for example a frontend, a backend, and a database. And they also need some configuration. This can make docker commands very long and unhandy. This is what `docker-compose` is for. You can specify multiple services and their configuration in a file and then start containers with a single command: `docker-compose up`


## Give it a try
Use the docker-compose example from the docker website to start wordpress locally:
https://docs.docker.com/compose/wordpress/

Start wordpress using docker-commands and make yourself comfortable with the following docker-compose commands:

```bash
docker-compose up [-d] #starts (and creates if necessary) containers based on a compose file
docker-compose ps #list all containers belonging to the compose file
docker-compose stop [<continerId>] #stop all or a specific container belonging to the compose file
docker-compose start [<continerId>] #start all or a specific container belonging to the compose file. This does not create containers, if they do not exist
```

## What does docker-compose do for you?
The docker compose file specifies two services, their configuration and which images to use to start theses containers. There is no portforwarding of the database. This is not necessary, because docker compose creates a network in which the containers can communicate with eachother. 

Commands that docker-compose do for you, when executing `docker-compose up`:

```bash
$ docker network create example
$ docker volume create db_data
$ docker run \
    -e MYSQL_ROOT_PASSWORD=somewordpress \
    -e MYSQL_DATABASE=wordpress \
    -e MYSQL_USER=wordpress \
    -e MYSQL_PASSWORD=wordpress \
    --restart=always \
    --mount source=db_data,target=/var/lib/mysql \
    --name db \
    --network example \
    mysql:5.7
$ docker run \
    -e WORDPRESS_DB_HOST=db:3306 \
    -e WORDPRESS_DB_USER=wordpress \
    -e WORDPRESS_DB_PASSWORD=wordpress \
    -e WORDPRESS_DB_NAME=wordpress \
    --restart=always \
    -p 8000:80 \
    --network example \
    wordpress:latest       
```

`depends_on` from the example will start services in dependency order, therefore it is not part of the commands.

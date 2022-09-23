
### Database Migration
- When to use ```.yml``` and ```.json``` file?
    - ```.yml```: for configuration file
    - ```.json```: for exchanging data between multiple computers e.g. a client or server (much faster to parse due to no need for judging the datatype) (All datatype are being specified such as str using " ", but ```.yml``` file have to view all data as str)
 
 
### Docker Compose
[Docker compose tutorial](https://www.youtube.com/watch?v=HG6yIjZapSA)
```bash=
# some are in running or stop contianer
# so get all containers id
# -a bring stopped containers as well (clean the workspace)
$ docker container rm $(docker contianer ls -aq)

$ cd <directory>
# build the image first and run the service
$ docker-compose build 
# run docker compose to start your multiple containers (run in the background (detach))
$ docker-compose up -d 
# or use a single command
$ docker-compose up --build -d

# stop the services
$  docker-compose down
```

```yml=
# docker-compose.yml
---
version: "3.8"
services:
  web:
    build: ./frontend
    ports: # port mapping
      - 3000:3000 # map for port 3000 of the host to port 3000 of the container
  api:
    build: ./backend
    ports:
      - 3001:3001
    environment: # need to tell where the database is "=mongodb": to mongodb
      DB_URL: mongodb://db/vidly  
      # db: connect to ```db``` services we define
      # db/<database name> 
  db:
    image: mongo:4.0-xenial
    ports:
      - 27017:27017
    # don't want the data stored in the temporary containers, so define volumes
    volumes:
      - vidly:/data/db # map ````vidly``` this volume to a directory inside the container)

# the syntax we have to follow (default stored in /var/lib/docker/volumes) (local filesystem)
volumes:
  vidly: # with no value   
```
- volumes: default stored in the ```/var/lib/docker/volumes```
- Or we can directly define a local folder to mount the data in the container 
```yml=
---
version: "3"
services:
  db:
    image: mongo:4.0-xenial
    ports:
      - 27017:27017
    volumes:
      - D:/project1_datastorage:/data/db 
```
![](https://i.imgur.com/0zwj6wl.png)

- Each service will have one Dockerfile (```frontend``` & ```backend```)

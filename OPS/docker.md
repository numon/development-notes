## Docker comands

- `docker run nginx:version`
- `docker run -d nginx` - detach mode (run in background) 
- `docker attach nginx` - check output of image
- `docker run -it nginx bash`
- `docker run -p 80:5000 container_name`
- `docker run -v /opt/datadir:/var/lib/mysql mysql` - map data to local dir
- docker ps 
- docker ps -a
- docker stop container_name
- docker rm container_name
- docker images
- docker rmi container_name
- docker rm
- docker run --name webapp nginx:1.14-alpine
- docker inspect

- `docker exec container_name cat /etc/hosts` - execute command in container

- `docker build .` - build container from Docker file
- `docker build -t ./ image_name` - build with specific name
- `docker login`
- `docker push image_name` - push to docker hub

- docker run -e ENV_VARIABLE=production images_name
- docker run --mount type=bind,source=/data/mysql,target=/var/lib/mysql mysql
- docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
- docker run -v /opt/data:/var/lib/mysql -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql.

 - docker stop $(docker ps -q)
 - docker rm $(docker ps -a -q)
 - docker rmi $(docker images -q) 
 
- docker network ls
-  docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network


## Docker file
```dockerfile
FROM node:12

RUN apt-get update

COPY file/path /to/path
ENTRYPOINT yarn start

```
## Docker compose 
```yaml
redis:
  image: redis
db:
  image: postgres:latest
front:
  build: ./path/to/frontend
  ports:
    - 5000:80
  links:
    - db
```
- docker-compose up

```yaml
version: 2
services:
  redis:
    image: redis
    networks:
      - frontend
      - backend
  db:
    image: postgres:latest
    networks:
      - backend
  front:
    build: ./path/to/frontend
    networks:
      - backend

networks:
  - frontend
  - backend
```

## Docker swarm
- docker swarm init
- docker service create --replicas=3 image_name

## Kubernetes
 Cluster -> Nodes

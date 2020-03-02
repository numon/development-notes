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

- docker exec container_name cat /etc/hosts

- docker build .
- `docker build -t ./ image_name` - build with specific name
- `docker login`
- `docker push image_name` - push to docker hub

- docker run -e ENV_VARIABLE=production images_name


## docker file
```dockerfile
FROM node:12

RUN apt-get update

COPY file/path /to/path
ENTRYPOINT yarn start

```

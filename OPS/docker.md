## Docker comands

- docker run nginx:version
- docker run -d nginx - detach  mode 
- docker run -it nginx bash
- docker run -p 80:5000 container_name
- `docker run -v /opt/datadir:/var/lib/mysql mysql` - map data to local dir
- docker ps 
- docker ps -a
- docker stop container_name
- docker rm container_name
- docker images
- docker rmi container_name
- docker rm
- docker run --name webapp nginx:1.14-alpine

- docker exec container_name cat /etc/hosts

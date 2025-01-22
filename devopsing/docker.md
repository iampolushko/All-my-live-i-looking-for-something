### Commands

Docker-compose logs “container name” – check container logs
docker container prune - delete all stopped containers
docker rmi IMAGE_ID - remove docker image
docker rm CONTAINER_ID - remove docker container
docker volume ls - list of the all volumes

### Idea stuff

In idea you can open the run configuration add in vm-option this thing

```
-DMYSQL_USER=root -DMYSQL_PASSWORD=root -DMYSQL_PORT=3308
```

```.properties
spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:${MYSQL_PORT:3308}/diplom
spring.datasource.username=${MYSQL_USER:root}
spring.datasource.password=${MYSQL_PASSWORD:root}
```

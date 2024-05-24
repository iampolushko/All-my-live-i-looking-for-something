### Commands

Docker-compose logs “container name” – check container logs

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

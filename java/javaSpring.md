# Spring

[Spring project template builder](https://start.spring.io/). You can also use build in inteliga pro functional but you doesn't have money for inteliga pro or just make the intliga project and follow the instruction in the docs.
[Best guide](https://www.youtube.com/watch?v=fL5NDw0rDOI)

#### App layers

- API Layer (GET, POST, PUT, DELETE)
- Servide layer
- Data access layer
- Data base(another app)

#### Functional

[Spring boot](https://spring.io/projects/spring-boot/) is a base on what you can install the applications to make you own configuration. Is it a builder.

#### Structure

pom - project object manager. It is control the project

parent - обозначает наследование. If we delete the parent, we will need to add parent link in every dependency.

plugins have usage mostly in microservices or docker images

What is controller in spring? Is a components what calculate the user requests and generate answers. Controller is a java class what have any realisation of controller annotation. Controller take information from http request param, heeder or body and use this info for make any buisness logic. Then buisnes logic is done, controller make http answer what will send to user.

After spring read all project it starts read application file. Can have an extensions:
.properties(Y need to write full path for every param but it is the esiest to lern)

```properties
    some.test.number=32
    some.test.text=Some text
```

.yml()

```yml
some:
  test: number:32
    text:Some text
```

## Lombok

https://youtu.be/QmsMWCIf3nc?si=JqLH9IEQRdCITMGm

#### Annotations

bean - is any class what controlle by container spring.
Whet Spring starts it load all components in them context.
Components is any object what have any annotation(configuration, component, bean, controller, service, repository)

###### Annotation what you real will use.

- @Controller - manage the incoming http requests
- @ResponseBody - дает фреймворку понять, что объект, который вы вернули из метода надо прогнать через HttpMessageConverter, чтобы получить готовое к отправке на клиент представление.
- @RestController - is @Controller + @ResponseBody. It is mark class as Spring MVC controller and automaticly convert returned data to json or xml
  - @GetMapping - mark method
- @Component - it is marks means as Spring componets
- @Service - meta assosiated with @Component(It is just a special case for @Component). It is indicate what the class holding the buisness logic.
- @Repository - meta assosiated with @Component. For cath specific exeptions and retrow them to Spring unifiend and uncheck exeptions

## Angular

Big framework
[All facts](https://habr.com/ru/companies/otus/articles/746076/)

## Data base connection

Dont forget add to pom mysql(for working with db) adn jpa(for automise table instanse making) dependensys
Application.yml(.properties) file:

```yml
spring:
  datasource:
    url: jdbc:mysql://localhost:3307/test
    username: user
    password: user
  jpa:
    show-sql: true
    generate-ddl: true
    hibernate:
      ddl-auto: update
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect
```

[JPA Entity](https://www.youtube.com/watch?v=_mDKqZO9FzI) - u can make class(entity) from sql table

##Post and Get

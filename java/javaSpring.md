# Spring:

[Spring project template builder](https://start.spring.io/). You can also use build in inteliga pro functional but you doesn't have money for inteliga pro or just make the intliga project and follow the instruction in the docs.
[Best guide](https://www.youtube.com/watch?v=fL5NDw0rDOI)

#### App layers

- API Layer (GET, POST, PUT, DELETE)
- Serviсe layer
- Data access layer
- Data base(another app)

#### Functional

[Spring boot](https://spring.io/projects/spring-boot/) is a base on what you can install the applications to make you own configuration. Is it a builder.

#### Structure

#### Spring mvc

Схема проектирования
model - view - controller
controller - works for listening the url. Working with user.
model - work with data base.

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

Spring have a lot of included frameworks(like Security, JPA, MVC)

@Service - is a local case of @Component

### Get and Post

- #### Get
  We have 2 way to get arguments from get request. Difficult and complex or easy and accurate:
- Difficult
  This method is geting access to all request info
  If u dont add params it print null null

```java
    @GetMapping("/test")
    public String returnName(HttpServletRequest request) {
        //Taking params from request
        String name = request.getParameter("name");
        String surname = request.getParameter("surname");
        //just test output
        System.out.println(name + " "+ surname);
        //U need to return html page frome where get the request params
        return "src/main/resources/static/product.html";
    }
```

- Easy
  This method doesnt take all request. It takes only parameters.
  <text style="color: rgba(255, 0, 0, 1);">If u dont add the params it dont find the page</text>
  if u wanna make possible print null null just add the "required=false" as @RequestParam argument

```java
    @GetMapping("/test")
    public String returnName(@RequestParam("name") String name,
                              @RequestParam("surname") String surname) {
        System.out.println(name + " "+ surname);
        return "src/main/resources/static/product.html";
    }
```

Request text

```URL
http://localhost:8080/test?name=oleg&surname=danov
```

Console normal output

```
oleg danov
```

# Important dependencies (frameworks?):

## 1 - Spring web

Restful API
Для создания контроллеров запросов
Tomcat

## 2 - Thymeleaf

Tichicaly it is a interlayer betwen java backand and html (way to connect backend and frontend). Шаблонизатор.
It is make a logic inside the html documents
https://www.youtube.com/watch?v=nyQx6jqnsZg

##### Different types of vars

${param} - take on or paste in data in page
@{/path/style.css} - link type(any files, photo too). HTML engine can not see the files inside the "static", becouse it's have self orient file system.
\*{param.lengh} - util var. Ucan use normal java String methods in html

##### How to use vars?

When you opening the html tag put this link inside of it

```html
<html xmlns:th="http://www.thymeleaf.org"></html>
```

If u need to show java ref in html

```java
  @GetMapping("/catalog") // just part of the link
  public String pageForAll(Model model) {
      String penis = "pe pe pe penis";
      model.addAttribute("penis", penis);
      return "pages/catalog"; // html adres from repository
  }
```

```html
<h1 th:text="penis"></h1>
```

if you need the cycle:

```java
  @GetMapping("/catalog")
  public String pageForAll(Model model) {
      ArrayList<String> numbers = new ArrayList<>();
      numbers.add("1");
      numbers.add("2");
      model.addAttribute("numbers", numbers);
      return "pages/catalog";
  }
```

```html
<div th:each="number : ${numbers}">
  <h1 th:text="${number}"></h1>
</div>
```

For insert the html blocks:
Put the 'part' block inside of 'div' with "th:fragment" tag

```html
<div th:fragment="header"><div></div></div>
```

and add the link in th:insert

```html
<div th:insert="blocks/header :: header"></div>
<!--blocks - repository name, header - file name, header after :: - is a th:fragment = "header"-->
```

## 2 - springframework.security

### unmarked info

- ### important tip!

if u have problem with access to resourses from **static** folder firstly check the links in html.
It is should be looks like that:

```html
<link th:href="@{/css/style.css}" rel="stylesheet" />
<img th:src="@{/images/user.svg}" alt="user" />
```

After that in class **SecurityConfig** create this method:

```java
    @Bean
    WebSecurityCustomizer configureWebSecurity() throws Exception{
        return (web) -> web.ignoring().requestMatchers("/images/**", "/css/**");
    }
```

Holy moly! It is would bee works.
BUT!
The indial comrat from [this video ](https://www.youtube.com/watch?v=6gswFeWXvF8&) that this way is not to great and we should use the:

```java
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http.authorizeHttpRequests(auth -> auth.requestMatchers("/images/**", "/css/**").permitAll());
    }
```

## 3 - Lombok

https://youtu.be/QmsMWCIf3nc?si=JqLH9IEQRdCITMGm

#### Annotations

bean - is any class what controlle by container spring.
Whet Spring starts it load all components in them context.
Components is any object what have any annotation(configuration, component, bean, controller, service, repository)

#### Annotation what you real will use(fundamental spring annotations).

- @Controller - manage the incoming http requests
- @ResponseBody - дает фреймворку понять, что объект, который вы вернули из метода надо прогнать через HttpMessageConverter, чтобы получить готовое к отправке на клиент представление.
- @RestController - is @Controller + @ResponseBody. It is mark class as Spring MVC controller and automaticly convert returned data to json or xml
  - @GetMapping - mark method
- @Bean -
- @Component - it is marks means as Spring componets. @Bean variation
- @Service - meta assosiated with @Component(It is just a special case for @Component). It is indicate what the class holding the buisness logic.
- @Repository - meta assosiated with @Component. For cath specific exeptions and retrow them to Spring unifiend and uncheck exeptions

## 4 - spring-boot-devtools

making the local server

# Build and depoloing

- ### Second properties file
  U can create copy of **application.properties** what called the **application-dev.properties** and edit the configuration in u IDE.
  In **edit configuration** page in field **program arguments** put this:

```
--spring.profiles.active=dev
```

# Unmarked info:

## Angular

Big framework
[All facts](https://habr.com/ru/companies/otus/articles/746076/)

## Data base connection

It id from jpa or mysql-connector-j or spring-boot-starter-data-jpa dependencies
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

## Unmarked info and questions

In class controller you should use the annotation @Controller if u wann return page. For what @RestController exists?

### Interesting facts:

Spring boot по умолчанию использует web server appache tomcat
https://ru.stackoverflow.com/questions/1211649/thymeleaf-%D0%BD%D0%B5-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B0%D0%B5%D1%82-css-%D1%84%D0%B0%D0%B9%D0%BB

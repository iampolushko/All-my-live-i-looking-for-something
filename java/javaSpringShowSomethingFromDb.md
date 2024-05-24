# Show Something From DB in Spring

### Make some preferences

- ### pom.xml
  we add all version dependencies and plugins info for build here

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.1.7</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.example</groupId>
	<artifactId>buysell</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>buysell</name>
	<description>shop</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-freemarker</artifactId>
		</dependency>

		<dependency>
        <!-- for create the comfortable annotations like getters and setters and lot more -->
			<groupId>org.projectlombok</groupId>
			<artifactId>lombok</artifactId>
			<version>1.18.24</version>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-mail</artifactId>
		</dependency>
		<dependency>
         <!-- for restfuul api -->
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
        <!-- makes possible the mysql connection -->
			<groupId>com.mysql</groupId>
			<artifactId>mysql-connector-j</artifactId>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-test</artifactId>
			<scope>test</scope>
		</dependency>

	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
				<configuration>
					<image>
						<builder>paketobuildpacks/builder-jammy-base:latest</builder>
					</image>
				</configuration>
			</plugin>
		</plugins>
	</build>

</project>
```

- Starter-security and security-test - is not the same. If you call the Starter-security you got the aothorisation page.

* ### application.yml or .properties
  the only differense betwen those 2 types is writing style. IN .properties u need to write full path to every setting.

```yml
spring:
  datasource: # make sql connection for datasource
    url: jdbc:mysql://localhost:3307/test
    username: user
    password: user
  jpa:
    show-sql: true # for show sql in console
    generate-ddl: true # return bool what mean either shema initialise or not
    hibernate:
      ddl-auto: update
    properties:
      hibernate:
        dialect: org.hibernate.dialect.MySQL8Dialect #mysql dialect
```

### Make java classes

##### Create Repositories in java.com.projectName

- entity
- repository
- service
- controller

- ### Entity

```java
package com.example.buysell.Entity;

import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity //Main annotation what referensing spring boot what this class corresponds to sql table
@Data //Add getters and setters  (thx lombok :3 )
@Table(name = "Student")
@NoArgsConstructor //Class constructor whithout arguments (thx lombok :3 )
@AllArgsConstructor //Class constructor with arguments  (thx lombok :3 )
public class StudentEntity {
    @Id
    @Column(name = "id")
    @GeneratedValue
    private int id;

    @Column(name = "mark")
    private int mark;

    @Column(name = "name")
    private String name;
}

// If i understood right, this entity create table student in database if it don't exist and just connect to existing table
```

- ### Repository

```java
package com.example.buysell.Repository;

import com.example.buysell.Entity.StudentEntity;
import org.springframework.data.jpa.repository.JpaRepository;

//able to perform all the operation to our database or entity
public interface StudentRepo extends JpaRepository<StudentEntity, Integer> { //in <> we add the entity class and type of entity(table) primary key
}
```

- ### Service

```java
package com.example.buysell.Service;

import com.example.buysell.Entity.StudentEntity;
import com.example.buysell.Repository.StudentRepo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class StudentService { //here we make all operations with entity. We get entity through the repository
    @Autowired // u just need this annotation to not geta an error
    private StudentRepo studentRepo;

    public StudentEntity saveDetails(StudentEntity studentEntity) {
        return studentRepo.save(studentEntity);
    }

    public List<StudentEntity> getAllDetails() {

        return studentRepo.findAll();
    }
}
```

- ### Controller

```java
package com.example.buysell.Controller;

import com.example.buysell.Entity.StudentEntity;
import com.example.buysell.Service.StudentService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class StudentController {
    @Autowired
    private StudentService studentService;

    @PostMapping("/addStudent") //make post request
    public StudentEntity postDetails(@RequestBody StudentEntity studentEntity) {
        return studentService.saveDetails(studentEntity);
    }

    @GetMapping("/getStudents") //make get request
    public List<StudentEntity> getDetails() {
        return studentService.getAllDetails();
    }
}
```

Don't forget what you have the Application class(here no user moves. I add this just to explain hows it's works)

```java
package com.example.elembase;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@SpringBootApplication //contains 3 annotations insid
//1 - @SpringBootConfiguration - just a special form of @Configuration but without any configuration parameters(you can add just a few)
//2 - @EnableAutoConfiguration - spring auto confugurate all components
//3 - @ComponentScan - add possability to add annotations for all classes
public class ElemBaseApplication{
    public static void main(String[] args) {
        SpringApplication.run(ElemBaseApplication.class, args);
    }
}
```

### Testing

after all of that u can open the postman style program and make the post request "http://localhost:8080/addStudent" with json:

```json
{
  "name": "Student name",
  "mark": 100
}
```

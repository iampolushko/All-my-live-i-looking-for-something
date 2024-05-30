#### Folder structure

- ##### entitiy
  сущность объекта из базы данных
- ##### repository
  интерфейс, связывающий таблицу из базы данных и класс entity
- ##### service
  содержит в себе логику операция над entity
- ##### dto
  dto - объект, который используется для передачи данных между подсистемами приложения. Он содержит только поля и getter/setter методы для доступа к ним. DTO не содержит бизнес-логики и используется только для передачи данных
- ##### controller
  через него проходят rest операции

#### Test app

- ##### pom

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.3.0</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example</groupId>
    <artifactId>restTest</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>restTest</name>
    <description>restTest</description>
    <properties>
        <java.version>17</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>

```

- ##### properties

```properties
spring.application.name=restTest

spring.datasource.driver-class-name=org.postgresql.Driver
spring.datasource.url=jdbc:postgresql://localhost:5432/test
spring.datasource.username=postgres
spring.datasource.password=root
spring.jpa.generate-ddl=true

server.port=8081


```

- ##### entitiy

```java
package com.example.resttest.entity;

import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE)
    private Long id;
    private String name;
    private Short amount;
}
```

- ##### repository

```java
package com.example.resttest.repository;

import com.example.resttest.entity.Product;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

- ##### service

```java
package com.example.resttest.service;

import com.example.resttest.dto.ProductDTO;
import com.example.resttest.entity.Product;
import com.example.resttest.repository.ProductRepository;
import lombok.AllArgsConstructor;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
@AllArgsConstructor
public class ProductService {
    private final ProductRepository productRepository;

    public Product create(ProductDTO dto) {
        Product product = Product.builder()
                .name(dto.getName())
                .amount(dto.getAmount())
                .build();

        return productRepository.save(product);
    }

    public List<Product> readAll() {
        return productRepository.findAll();
    }

    public Product update(Product product) {
        return productRepository.save(product);
    }

    public void delete(Long id) {
        productRepository.deleteById(id);
    }
}
```

- ##### dto

```java
package com.example.resttest.dto;

import lombok.Data;

@Data
public class ProductDTO {
    private String name;
    private Short amount;
}
```

- ##### controller

```java
package com.example.resttest.controller;

import com.example.resttest.dto.ProductDTO;
import com.example.resttest.entity.Product;
import com.example.resttest.service.ProductService;
import lombok.AllArgsConstructor;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@AllArgsConstructor
public class ProductController {

    private final ProductService productService;

    @PostMapping
    public ResponseEntity<Product> create(@RequestBody ProductDTO dto){
        return new ResponseEntity<>(productService.create(dto), HttpStatus.OK);
    }

    @GetMapping
    public ResponseEntity<List<Product>> readAll(){
        return new ResponseEntity<>(productService.readAll(), HttpStatus.OK);
    }

    @PutMapping
    public ResponseEntity<Product> update(@RequestBody Product product){
        return new ResponseEntity<>(productService.update(product), HttpStatus.OK);
    }

    @DeleteMapping("/{id}")
    public HttpStatus delete(@PathVariable Long id) {
        productService.delete(id);
        return HttpStatus.OK;
    }
}
```

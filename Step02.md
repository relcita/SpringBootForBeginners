##What You Will Learn during this Step:
- Lets add dependencies and see if they are autowired in
- Lets make Spring Boot log the content from Spring Framework in Debug mode

## Useful Snippets and References

First Snippet

```
    @Component
    class SomeBean {

        @Autowired
        private SomeDependency someDependency;

        public String calculateSomething() {
            // I'm a lazy bugger. Skipping calculation
            return someDependency.getSomething();
        }
    }

    @Component
    class SomeDependency {

        public String getSomething() {
            return "something";
        }

    }
```

Second Snippet
```
System.out.println(ctx.getBean(SomeBean.class).calculateSomething());
```
Third Snippet
```
/src/main/resources/application.properties
logging.level.org.springframework=DEBUG
```

## Exercises

## Files List
### /pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.in28minutes</groupId>
    <artifactId>springboot-for-beginners-example</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>Your First Spring Boot Example</name>
    <packaging>war</packaging>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.4.0.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```
### /src/main/java/com/in28minutes/springboot/Application.java
```
package com.in28minutes.springboot;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;
import org.springframework.stereotype.Component;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        ApplicationContext ctx = SpringApplication.run(Application.class, args);
        System.out.println(ctx.getBean(SomeBean.class).calculateSomething());

    }

    @Component
    class SomeBean {

        @Autowired
        private SomeDependency someDependency;

        public String calculateSomething() {
            // I'm a lazy bugger. Skipping calculation
            return someDependency.getSomething();
        }
    }

    @Component
    class SomeDependency {

        public String getSomething() {
            return "something";
        }

    }

}
```
### /src/main/resources/application.properties
```
logging.level.org.springframework=DEBUG
```
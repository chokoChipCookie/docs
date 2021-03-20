# 2stWeekSummary by Tori

## 0. Java SE8 버전, 이전 버전과의 차이 및 주요 변경사항 정리
- 람다 표현식
   - `함수형 인터페이스` (추상 메서드를 하나만 가지는 인터페이스)의 인스턴스를 만드는 방법으로 쓰일 수 있음
   - 메소드의 매개변수, 리턴 타입, 변수로도 사용이 가능
   
   ````JAVA
    new Thread(new Runnable() { //스레드 생성 및 실행
        @Override
        public void run() {
            System.out.println("기존의 Runnable 인스턴스 생성 방법");
        }
    }).start();
   ````

    ````JAVA
    new Thread(() -> System.out.println("람다 표현식")).start();
   ````
<br />

------------

## 1. 기존의 스프링 MVC와 스프링 부트의 차이점
- 기존에는 프로젝트를 셋팅하는 데에 많은 시간이 걸림 (서로 호환되는 버전의 jar 등)
- spring-boot-starter로 자주 사용되는 편리한 의존성 조합을 간단하게 설정할 수 있음

<br />

------------

## 2. IDE 에서 제공하는 스프링 이니셜라이저로 프로젝트 세팅하며 과정 정리

> IntelliJ IDEA를 사용하였습니다. 

- Maven 프로젝트 생성

- pom.xml에 Dependency 추가 및 플러그인 다운로드

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>
        <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>2.4.3</version>
            <relativePath/> <!-- lookup parent from repository -->
        </parent>
        <groupId>com.example</groupId>
        <artifactId>rest-service</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <name>rest-service</name>
        <description>Demo project for Spring Boot</description>
        <properties>
            <java.version>1.8</java.version>
        </properties>
        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
            </dependency>

            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-test</artifactId>
                <scope>test</scope>
            </dependency>
        </dependencies>

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

- Controller 및 View를 위한 DTO 클래스를 생성
    ```JAVA
    package com.example.restservice;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication
    public class MainApplication { //내장 WAS를 실행하는 Main 클래스
        public static void main(String arg[]){
            SpringApplication.run(MainApplication.class, arg);
        }
    }

    ```

    ```JAVA
    package com.example.restservice;

    import java.util.concurrent.atomic.AtomicLong;

    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class GreetingController {

        private static final String template = "Hello, %s!";
        private final AtomicLong counter = new AtomicLong();

        @GetMapping("/greeting")
        public Greeting greeting(@RequestParam(value = "name", defaultValue = "World") String name) {
            return new Greeting(counter.incrementAndGet(), String.format(template, name));
        }
    }
    ```

    ```JAVA
    package com.example.restservice;

    public class Greeting {

        private final long id;
        private final String content;

        public Greeting(long id, String content) {
            this.id = id;
            this.content = content;
        }

        public long getId() {
            return id;
        }

        public String getContent() {
            return content;
        }
    }
    ```



- Configuration에 Maven Goal을 추가
   ```
   spring-boot:run
   ```

- 서버 구동하여 `http://127.0.0.1:8080/greeting` 페이지 확인
    ```json
    {"id":1,"content":"Hello, World!"}
    ```

<br />

------------

## 3. ORM과 JPA에 관련하여 정리(Spring Data JPA, MyBatis에 대해 함께 정리)
- ORM(Object Relational Mapping) : 객체와 RDB간 데이터를 자동으로 매핑해주는 프레임워크
   - SQL에 의존적인 코딩에서 벗어나 `비즈니스 로직`에 집중
   - 객체 간의 관계를 바탕으로 SQL을 자동으로 생성
 
- JPA(Java Persistence API) : 자바 ORM 기술에 대한 표준 명세로 자바에서 제공하는 API
   - RDB의 관계를 Object에 반영하는 것이 목적으로, `객체`를 통해 DB 데이터를 다룸
   - Mapper는 필드 변경 시 SQL을 수정해야 하지만, JPA는 `필드`만 변경하면 되어 유지보수가 쉬움

- myBatis : SQL 매핑 프레임워프중 하나로, JDBC 코드의 복잡함을 해결
   - `Connection` 과 `close()`가 자동으로 가능
   - 내부적으로 `preparedStatement` 처리
   - Mapper는 SQL과 그에 대한 처리를 지정하는 역할을 하는데, myBatis와 Spring을 연동하는 경우 `Mapper XML`과 `Mapper 인터페이스` 구조가 필요함
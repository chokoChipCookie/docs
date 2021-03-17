# 2stWeekSummary.md By YMK

## 0. Java SE8 버전, 이전 버전과의 차이 및 주요 변경사항 정리
- JAVA 8 : `Oracle` 로 인수된 후 첫번째 버전
- 람다식 지원
	- 람다식 : `익명함수` (메소드역할을 대신 함)
	- 장점 : 간결하다.
	- 단점 : 가독성이 떨어질 수 있다.

------------

## 1. 기존의 스프링 MVC와 스프링 부트의 차이점
- 프로젝트의 전반적인 설정방법이 다르다.
	- `스프링` 에서는 xml 파일로 bean을 생성하여 프로젝트 설정
	- `스프링부트` 에서는 java 코드와 yml 파일로 프로젝트 설정이 가능하여 가독성이 좋고, 관리하기 편하다.

	> 프로젝트 예시 보여주며 설명

------------

## 2. IDE 에서 제공하는 스프링 이니셜라이저로 프로젝트 세팅하며 과정 정리
> 본인은 IntelliJ Community 버전을 설치했습니다. (설치과정 생략)
> Commuity 버전은 Spring Boot 프로젝트 생성기능이 제공되지 않으므로 별도로 의존성을 주입해줘야 한다.
- Gradle 사용 시
	- bundle.gradle 파일의 내용을 수정해준다.

	```
	수정 전
	plugins {
		id 'java'
	}
	```

	```
	수정 후
	buildscript {
		ext{
			springBootVersion='2.2.11.RELEASE'
		}
		repositories {
			mavenCentral()
		}
		dependencies {
			classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
		}
	}
	```

- Maven 사용 시
	- pom.xml 파일에 내용을 추가해준다.

	```xml
	<properties>
		<java.version>1.8</java.version>
		<maven-jar-plugin.version>3.1.1</maven-jar-plugin.version>
	</properties>

	<!-- Inherit defaults from Spring Boot -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.2.11.RELEASE</version>
	</parent>

	<!-- Override inherited settings -->
	<description/>
	<developers>
		<developer/>
	</developers>
	<licenses>
		<license/>
	</licenses>
	<scm>
		<url/>
	</scm>
	<url/>

	<!-- Add typical dependencies for a web application -->
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>

	<!-- Package as an executable jar -->
	<build>
		<pluginManagement>
			<plugins>
				<plugin>
					<groupId>org.springframework.boot</groupId>
					<artifactId>spring-boot-maven-plugin</artifactId>
				</plugin>
			</plugins>
		</pluginManagement>
	</build>
	```

- 서버 구동
	- 테스트를 위해 Application 과 Controller 클래스를 생성한다.
	```java
	Application.java 
	@SpringBootApplication
	public class Application {
		public static void main(String arg[]){
			SpringApplication.run(Application.class, arg);
		}
	}
	```
	
	```java
	HomeController.java
	@RestController
	public class HomeController {

		@RequestMapping("/")
		public String index() {
			return "확인";
		}
	}
	```
	
	- IntelliJ 의 터미널을 열어 서버를 run 해주자.
		- Gradle 사용시
		```js
		grandlew build 
		gradlew bootRun
		```
		- Maven 사용시
		```js
		mvn package -X
		mvn spring-boot:run
		(Application.java 파일을 run 해도 정상작동)
		```

------------

## 3. ORM과 JAP에 관련하여 정리(Spring Data JPA, MyBatis에 대해 함께 정리)
- ORM 프레임워크는 데이터베이스 객체를 자바 객체로 매핑 함으로써 객체간의 관계를 바탕으로 SQL을 자동으로 생성해주지만 myBatis 는 SQL을 명시해줘야 한다.
	- `ORM(Object Relational Mapping)` : 객체 관계 매핑(연결)
	- `JPA(Java Persistence API)` : Java ORM 기술에 대한 API 표준 명세(Java 에서 제공하는 API)

- SQL Mapper : 직접 SQL문을 작성해 DB에 접근하는 것을 의미
	- `myBatis` : 개발자가 지정한 SQL, 저장프로시저 그리고 몇가지 고급 매핑을 지원하는 퍼시스턴스 프레임워크이다. 

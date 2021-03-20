# 두번째 주 내용 정리

## 1. Java SE 8 주요 변경사항

- 람다 표현식(`Lambda Expression`)

  - 익명 클래스의 한 개의 메소드를 식으로 표현한 것.
  - 식별자 없이 실행할 수 있는 함수 표현식을 의미하며 익명 함수로 부르기도 함.

  ```java
  // 기존
  int max(int a, int b) {
    return a > b ? a : b;
  }

  // 람다식
  (int a, int b) -> {
    return a > b ? a : b;
  }
  ```

  - 장점
    1. 불필요한 루프문의 삭제, 함수의 재활용에 용이함.
    2. 코드가 간결해져 코드 가독성 향상에 크게 기여함.
  - 단점
    1. 불필요하게 남발할 경우 코드의 이해도가 떨어지고 코드가 지저분해짐.
    2. 람다 표현식을 통해 만든 익명 함수는 재사용이 불가능함.

- 스트림 API(`Stream API`)

  - Java에서 많은 양의 데이터를 저장하기 위해 배열/컬렉션을 사용함. 이렇게 저장된 데이터에 접근하기 위해 반복문이나 반복자를 사용해 매번 새로운 코드를 작성하는데, 코드가 길어지고 코드 가독성이 떨어지며 코드의 재사용이 불가능해짐.
  - 이런 문제점을 해결하기 위해 Java SE 8부터 `Stream API`가 제공됨. `Stream API`는 데이터를 추상화하여 관리하며 배열/컬렉션, 파일에 저장된 데이터도 같은 방법으로 관리할 수 있음.
  - `Stream API`의 동작 흐름
    ```
    비정제 데이터 > 중개 연산 > 최종 연산
    ```
  - 연산 단계에서는 사용할 수 있는 연산이 정해져있으므로 신중히 선택하여 사용해야함.

- `java.time`
  - Java SE 8 이전 버전에서는 `Date` 클래스를 이용하여 날짜 연산을 수행했음.
  - 이후 `Calendar` 클래스도 있어지만 불변성, 윤초, 월 표현에 대한 문제가 있어 `java.time` 패키지가 제공됨.
  - `java.time` 패키지에 속하는 모든 클래스의 인스턴스는 불변 객체로 생성됩니다.

## 2. Spring MVC와 Spring boot의 차이점

- 기존의 `Spring MVC`는 최소한의 기능을 탑재한 기본 프로젝트를 설정하는데 너무 많은 시간이 소요됨.
- `Spring boot`는 내장 `Tomcat`이 들어있어 별도의 서버 설치 없이 자동으로 실행됨.
- `Spring boot`는 `Spring boot starter` 패키지를 제공함으로서 빠른 프로젝트 생성과 설정을 도와줌.
- ✨ 프로젝트 관리의 용이성, 빠른 프로젝트 구성을 위해 나온 `Spring boot`

## 3. `Spring boot` 설정 과정

- `Project SDK`와 `Starter Service URL` 설정

  - `JDK 1.8`과 `https://start.spring.io`로 설정함.

- `Spring Initializr Project Settings` 설정

  ```js
  {
    Group: 'com.example.bolam',
    Artifact: 'test',
    Type: 'Gradle',
    Language: 'Java',
    Packaging: 'Jar',
    Java Version: 11,
    Version: '0.0.1-SNAPSHOT',
    Name: 'test',
    Description: 'Test project for Spring Boot',
    Package: 'com.example.bolam.test',
  }
  ```

  - 예제 프로젝트는 `Gradle`과 `Java 8` 버전을 사용하기로 결정함.

- 의존성 추가

  - 최소한의 웹 프로젝트 구성을 위한 `Spring Web`과 `Lombok`을 추가함.
  - 이후 IDE에서 지원하는 기능을 사용하기 위해 `Lombok` 플러그인을 추가해야 함.

    ```gradle
    // build.gradle

    plugins {
      id 'org.springframework.boot' version '2.4.4'
      id 'io.spring.dependency-management' version '1.0.11.RELEASE'
      id 'java'
    }

    group = 'com.example.bolam'
    version = '0.0.1-SNAPSHOT'
    sourceCompatibility = '1.8'

    configurations {
        compileOnly {
            extendsFrom annotationProcessor
        }
    }

    repositories {
        mavenCentral()
    }

    dependencies {
        implementation 'org.springframework.boot:spring-boot-starter-web'
        compileOnly 'org.projectlombok:lombok'
        developmentOnly 'org.springframework.boot:spring-boot-devtools'
        annotationProcessor 'org.projectlombok:lombok'
        testImplementation 'org.springframework.boot:spring-boot-starter-test'
    }

    test {
        useJUnitPlatform()
    }
    ```

## 4. ORM과 JPA, MyBatis에 대하여

- ORM(`Object Relational Mapping`)
  - 객체와 관계형 데이터베이스의 데이터를 매핑함.
    - 객체 모델과 관계형 모델 간에 패러다임의 불일치가 존재함.
    - ORM을 통해 생성된 SQL 구문을 통해 패러다임의 불일치를 해결할 수 있음.
  - 장점
    1. 객체 지향적인 코드로 인해 직관적이고 개발자는 비즈니스 로직에 집중할 수 있게 됨.
    2. 데이터베이스에 대한 종속성이 줄어들고 재사용성과 유지보수의 편리성이 증가함.(그러나 로우 쿼리를 작성하는 경우 종속성이 증가하고 재사용성과 유지보수의 대한 편리성이 감소함.)
  - 단점
    - 완벽하게 ORM을 통해 서비스를 구현이 어려움.

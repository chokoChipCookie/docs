# 2주차_스프링부트



## 1. JAVA8
### (1). Optional Class
- 자바를 다루면서 가장 자주보던 NullPointerException! 피할수 없을까?
- 널체크를 클래스에게 맞기고 우린 생각하지 말자


```java
//자바8 이전 널체크
String str = getText();
int length;
if (str != null) {
	length = str.length();
} else {
	length = 0;
}


//자바8 
//널체크와 동시에 널이 아니면 String클래스를 람다식으로
//length메소드 호출, 널이면 0 반환
int length = Optional.ofNullable(
        getText()
    ).map(String::length)
     .orElse(0);
```


## 2. Rombok
- 기존 스프링 DTO,VO의 getter setter 등등 세팅을 대신해준다.
  - 어노테이션을 사용하여 대신 만들수있다. 작성이 훠얼씬 쉬워진다. 

\
  ```java
  // 기존
  package test.vo;
    private Integer idx;

    public int getIdx() {
        return idx;
    }

    public void setIdx(int idx) {
        this.idx = idx;
    }

    @Override
    public String toString() {
        return "idx :" + idx;
    }


  // Rombok 사용
@Getter @Setter
@RequiredArgsConstructor
@ToString
  private test.vo;
    public Integer idx;

  ```


## 3. MyBatis빠이 웰컴 JPA 
빠른장단점
- MyBatis
  - 그냥 SQL 매퍼, 공부안해도 SQL문 바로 작성해서 쓸수있다는 장?점이 있다.
  - 그외엔 없다 쓸데없는 DAO작성해서 연결해줘야 하며 쿼리도 XML로 작성해서 따로 빼둔다... 그럴바엔 프로시저 쓰고말지..
- JPA
  - ORM으로 엔터티클래스 작성해서 객제지향적으로 데이터를 가져올수 있다.
  - 러닝커브가 있다. ORM에 대한 기준같은게 딱히 없기때문에 ORM마다 쓰는방법이 다르다.

```java
//MyBatis
//XML 매핑
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
     PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
     "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
 //여기는 매핑할 MemberMapper.java의 풀패키지명을 적어준다
<mapper namespace="com.test.mybatis.PostsMapper">
 
    <resultMap type="Posts" id="PostsResultMap">
        <result property="_title" column="title" />
        <result property="_content" column="content" />
        <result property="_author" column="author" />
    </resultMap>
 
    <insert id="insertPost" parameterType="com.test.mybatis.Posts" >
        INSERT INTO posts values(#{_title},#{_content},#{_author})
    </insert>

//DAO
public interface PostsDAO {
    public void insertPost(Posts Posts);
}

//DAO_Service
@Repository
public class PostsDAOService implements PostsDAO {
 
    @Autowired
    private SqlSession sqlSession;

    @Override
    public void insertPost(Posts Posts) {
        PostsMapper postsMapper = sqlSession.getMapper(postsMapper.class);
        postsMapper.postsMapper(Posts);
    }


}


//JPA INSERT
@Getter
@NoArgsConstructor
@Entity
public class Posts {

    @Id // pk Field
    @GeneratedValue(strategy = GenerationType.IDENTITY) // for auto increment
    private Long id; //bigint

    @Column(length = 500, nullable = false)
    private String title;

    @Column(columnDefinition = "TEXT", nullable = false)
    private String content;
    private String author;

    @Builder
    public Posts(String title, String content, String author){
        this.title = title;
        this.content = content;
        this.author = author;
    }

//JPA 레포 연결
public interface PostsRepository extends JpaRepository<Posts, Long> {
    //EntityClass, Pk type
}
```
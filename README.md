# Spring-SelfStudy
  
   
      2022-04-05 start 
      Spring Self-Study 
      🧑‍🎓 Ref: Inflearn / Narp 
  

## **2022-04-06**
### Spring WEB MVC 프로젝트 만들기

▪️ Maven : 프로젝트 관리도구로 스프링은 Maven Tool에 의해서 만들어진다. <br>
  　　　　  **생성 -> 빌드 -> 배포**
        
        
<img width="14" alt="image" src="https://user-images.githubusercontent.com/100359222/161929783-366a9ca1-f9f8-4afc-ba95-f68ffcb88bd5.png"> : M은 maven, S는 Spring <br> 아이콘에서도 확인할 수 있다. <br>
▪️ pom(Project Object Model) 기술된 파일을 보고 maven Tool이 동작하게 된다. <br> 
<br> Pom이 하는것은? Library관리 == API 관리 <br><br>
▪️ MVC ➡️ Spring 변경된 점은? 1. POJO 2. DB설정

## **2022-04-07**
### Spring과 DB연결
1. root-context.xml에 database연결
- api파일 추가 
  -  Spring DB API 
  -  mybatis
  -  mybatis spring 
  -  spring jdbc
2. db.properties 연결 <br>
한 클래스를 생성한다고 했을때, A a = new A(); 처럼 **직접적인 생성**도 가능하겠지만 <br> spring에서는 **root-context.xml**파일 내에 ```<bean>태그``` 안에 클래스를 설정해줄 수 도 있다. <br>
  ```
  <bean id="소문자 시작" class="연결할 객체"> 
  <property name="locations" value="/WEB-INF/mybatis/db.properties"/>
  <property>의 태그는 class의 setter메소드에 의해서 value에 들어가있는 값을 넘겨주면 class의 파일을 읽어서 리턴해준다.
  ```
  
## **2022-04-08**
### Spring Web mvc에서 DataBase연결하기
- 자바에서 JDBC연결부분은 -> **DataSource**로 연결 -> bean생성 필요 <br>
```
  org.springFramework.jdbc.datasource -> simpleDriverDataSource.class 소스 활용
  <bean id="dataSource" class="simpleDriverDataSource.class 소스">
    <property name="driverClass" value="${driver}"/>
  🌟여기서 driver은 db.properties 즉, properties파일에 있는 driver을 의미한다.🌟
    <property name="url" value="${url}"/>
    <property name="username" value="${username}"/>
    <property name="pasword" value="${password}"/>
  <bean>
```

이외에도 스프링에서 jdbc방법이 여러가지가 있다. 하지만 표준 가이드라인은 상단의 내용이다. 먼저 공부하고, 깊은 내용을 추후에 공부하자! 😄

- jdbc를 활용해서 mybatis에서 sqlsessionfactory를 만들어내는게 가장 중요했다. 
```
  mybatis와 연관된 api
  <bean id="sqlSessionFactory" class="SqlSessionFactoryBean경로">
    - database연결정보 작성 -
    <property name="dataSource" ref="dataSource"/>
    <property name="configlocation" value="/WEB-INF/mybatis/config.xml(경로)"/> --> config.xml에 해당하기에 `typeAlias만` 필요하고 나머지는 필요없음.
    <property name="mapperlocation" value="classpath:kr/bit/mybatis/*.xml" /> -->
   - ✔️ mapper파일 참조시, mapper파일을 찾아가려면 ':' 콜론이 있어야한다.
  </bean>
```

## **2022-04-09**
### Spring web mvc 동작원리
- 🌟스프링은 모든 객체를 '스프링 컨테이너'가 관리한다 
  - 여기서 스프링컨테이너란 객체를 관리하는 '메모리공간'
- 🌟스프링에서 등장하는 가장 중요한 개념이 '`DI(Dependency Injection)`'이다. <br>
    의존관계를 싫어하는 스프링이기 때문에 등장! 외부로부터 주입을 받는것이 '의존성 주입(DI)'
- @ 어노테이션 (전처리) -> Spring Contatiner에서 관리를 해준다. -> <br>
-> class를 객체로 만들어준다 == 메모리에 new 하고 객체를 생성해준다는 의미다. <br>
annotation이 붙여져있으면 spring에서 발견해서 '객체'를 만들어준다. == POJO가 하나 만들어진다.

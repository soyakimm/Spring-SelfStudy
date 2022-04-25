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

## **2022-04-10**
### Spring web mvc 동작원리(2) 
DI(dependecy Injection)을 하는 방법
1. `@Autowired`
- 스프링컨테이너에 가서 MemberDAO 객체를 찾는다. 
- 찾은 객체를 해당 변수에 가져와서 쓸 수 있게 한다. 
- ⭐ 여기서 @ 어노테이션은 위에 말했던 '전처리' 즉, 행동에 옮겨진다는 의미다 ⭐
2. `@Inject`

객체 바인딩을 하기 위해서 스프링이 제공해주는 클래스가 있다 -> `'Model'`  <br>
`HttpServletRequest == Model`

## **2022-04-12**
### Spring WEB MVC를 이용한 회원관리

😙 파일뜯어보기
`root-context.xml` : 데이터베이스 연결하는 파일
`servlet-context.xml` : frontController 참조 파일
- `<context:component-scan base-package=...>` : controller을 메모리에 자동으로 올릴 수 있도록 도와줌
  - 어떻게 도와줄까? @어노테이션이 붙여있는 클래스를 Spring Container에서 관리를 해준다. <- 이를 MVC에서는 POJO라고 말했다.
-----------------------------
- `@RequestMapping` : HandlerMapping에 의해서 관리되는 매핑 | 클라이언트에게 요청이 오면 핸들러매핑이 @RequestMapping이라는 요청을 보고 각각의 메소드와 매핑을 시켜서 처리를 해준다.
### 이렇게 Spring에서 가장 큰 차이점은 POJO의 개수의 차이다. 하나에 적은 코드로 구현 가능하기 때문이다. 

`@RequestParam` : 클라이언트에서 넘어온 변수 이름을 다르게 설정

## **2022-04-14**
### Spring WEB MVC 프로젝트 만들기

메소드의 이름과 SQL의 ID를 최대한 일치시켜준다.
1. interface에 메소드를 정의
2. interface의 메소드하고 Sql Mapper의 id들의 이름과 연결시켜서 sql을 실행하게 만든다 ---> DAO가 필요없다. <br>
---- 이때 interface가 MapperInterface라고 부르는데, 이 인터페이스와 xml의 id와 자동으로 연결해서 DB프로그래밍을 한다 --- ✴️ 여기서 포인트 ! DAO를 없어지게함. <br>
### 근데 XML Mapper도 쓰지 않고, 메소드 위에다가 어노테이션을 이용해서 여기에 SQL을 쓰는 방법이 있다.

## **2022-04-15**
### Mapper 인터페이스와 XML mapper 파일 이용 CRUD하기
1. interface에 DAO에서 정의해놓은 메소드를 interface로 가져와 '정의'만 해놓는다.<br>
🌟 메소드의 이름이 sql의 id와 동일하게 설정되어있어, dao가 없어도 spring framework 내부에서 인터페이스만 가지고도 sql을 실행할 수 있도록 돕는다 ⭐ <br>
2. ✅ interface로 만든 **인터페이스명과** Mapper.xml파일의 `namespace`가 동일해야, spring framework에서 인터페이스만을 가지고도 sql을 실행할 수 있도록 하는 것이므로, 🕶️ 매우매우 주의해야한다!!!! -> 프레임워크가 알아서 매핑해준다 <br> 
<img width="551" alt="image" src="https://user-images.githubusercontent.com/100359222/163715259-5fd695ae-6422-47ac-9b25-702117778f22.png">

### 단! 이렇게 자동으로 매핑하기 위해서 조건을 걸어주어야 한다 ###
1. @Mapper 어노테이션 : Mybatis(SqlSessionFactory + SqlSession) 동격
2. root-context에 mybatis-spring:scan 이 있어야 한다. <br>
   -> mapper을 메모리에 올려서 작업할 수 있게 하는 것
<img width="557" alt="image" src="https://user-images.githubusercontent.com/100359222/163715493-44af698e-2e4e-4f54-8711-ce72b66ebd47.png">
<br>
3. 컨트롤러에서는 DAO가 아닌 Interface에 정의한 메소드를 가져온다
4. 3번에 정의한 interface메소드는 @Autowired로 의존성주입을 한 후, 빈등록을 한다.

## **2022-04-18** ##
### Mapper인터페이스와 @(Annotation)이용 CRUD
XML파일이 터무니없이 길어질 경우, Annotation을 사용한 crud가 더욱 효과적이다. <br>

## 2022-04-19 ##
### Spring WEB MVC와 Ajax 통신하기 (@ResponseBody)
Javascript를 통해서 데이터를 불러와 화면단에 뿌려줄 수 있다. <br>
이때, <script>태그를 이용해, $ajax를 통하여 서버와 연결한다. <br>
1. url : 요청하는 경로
2. type : 요청방식 (get, post)
3. dataType : 서버로부터 내려온 데이터 타입(json 등)
4. success : callback함수 (예: resultHtml)
5. error : error가 나면 실행할 것
------------------------------------
 ** success, 즉 받아올 펑션**
 1. function result(data) { <br>
  console.log(data); <br>
  alert(data); 등등 
}
  
### $.ajax() -> callback 함수로 응답 -> JSON로 Controller에서 응답필요 ###
<img width="434" alt="image" src="https://user-images.githubusercontent.com/100359222/163884105-55897779-2fa8-4f79-95aa-5665191d66c1.png">

## 2022-04-20 ##
### Spring WEB MVC 다중 파일 업로드 구현하기(UI) ###
🧑‍🎨 API 설치 필요: 1. Apache Commons-fileupload 2. commons-io  

업로드를 하기 위한 Bean 설정
  ■ servlet-context.xml
   ```
 <beans:bean id="multipartReslover" class="CommonsMultipartResolver의 경로">
   <bean:property name="maxuploadSize" value="52428800"/> : 업로드 가능한 최대 파일 크기
   <bean:prpoerty name="maxInMemoerySize" value="1000000*/> : 업로드 전 메모리 보관가능한 최대 바이트 크기     
   </bean:bean>
   ```
  ■ .jsp 파일의 <form>에서 파일업로드 할때 설정 <br>
`<form class = "" action="<c:url value='/upload.do(넘어갈 화면)" enctype="multipart/form-data" method="post">`
   
  ■ '추가'누를때마다 동적으로 파일이 추가로 업로드 되는 모습 확인 <br>
    ```
   var cnt=1;
 .append("<br>"+<input type='file' name='file"+cnt+"'/>");
   cnt++;
    ```

 ## 2022-04-25 ##
### Spring WEB MVC 다중 파일 업로드 구현하기1(서버) ###

file은 바이너리 데이터로 저장되어 서버에 넘어간다. <br>
enctype = multipart/form-data  == 여기서 multi의 의미는 서버로 넘어갈때 body에 구분이 되어서 한쪽은 파일정보 한쪽은 파라미터정보로 나누어서, form으로 쌓아서 넘어간다는 식으로 이해하면 된다. <br>

 - Spring에서 제공해주는 파일업로드 API가 존재 <BR>
 `MultipartHttpServletRequest multipartRequest` <br>
 🍎 `HttpServletRequest`는 name, id와 같은 파라미터만 받을 수 있다!

 - 업로드쪽으로 파라미터 정보가 넘어와서, `multipartReuqest`에 담긴다. 
   - 그때 사용할 수 있는 file 함수(기능)이 있다. 
    - `multipartRequest.getParameterNames()` // 예를 들어, id, name이라는 파라미터가 넘어온다.
     - 단, getParameterNames는 `Enumeration`라는 클래스로 받아주어야 한다.
       - `Enumeration` : 나열, 열거형 <-> **배열(X)** <BR>
           좋은점: 나열된 데이터가 몇개인지 알 필요가 없기때문에, (size,length) 커서를 옮겨다니면서 '**데이터의 유무**'만 판별해서 데이터를 처리한다.
         - `Enumeration`의 `hasMoreElements`: 엘리먼트를 가지고 있니? 가지고 있으면 ture, 없으면 false를 리턴한다.
  - multipartRequest로 가져온 파라미터들( file1, file2...)을 `getFileNames();` 라는 메소드를 통해서 가져와야한다. ⚠️이때 Names는 파일이름이 아닌, '파라메터의 이름'이다!
      - `getFileNames()`는 Iterator에 속해져있는 메소드이다.
- `MultipartFile` : spring에서 제공, 파일을 담을 수 있는 클래스 (파일이름, 파일타입, 파일크기 등)
   - `getOriginalFilename()` : 실제 업로드 된 파일 이름 뽑는 메소드
   
![image](https://user-images.githubusercontent.com/100359222/165184812-437f1e49-9d72-4baf-8071-22b6841c7306.png)

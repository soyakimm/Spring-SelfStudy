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
  

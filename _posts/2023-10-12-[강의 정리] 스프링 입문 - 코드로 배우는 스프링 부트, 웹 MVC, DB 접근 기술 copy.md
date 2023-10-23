---
title: "[강의 정리] 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술"
search: true
categories: 
  - 백엔드 공부
last_modified_at: 2023-10-23 14:26:00 +0900
---

#### 섹션 0. 강의 소개

https://start.spring.io/  
예전에는 스프링 프로젝트를 밑바닥부터 만들었지만 요즘에는 다 스프링부트라는 것을 가지고 스프링 프로젝트를 만듦

Maven
Gradle
필요한 라이브러리를 가져오고 빌드 라이프사이클까지 다 관리해주는 툴

과거에는 maven을 많이 썼으나 최근에는 gradle을 많이 씀

버전 선택  
snapshot은 아직 만들고 있는 버전  
M1은 아직 정식 릴리즈된 버전이 아님  

group 기업명   
artifact 빌드에 나올 때 결과물

file -> settings -> gradle 검색  
build and run using, run tests using  
둘 다 IntelliJ IDEA로 변경  
Gradle로 되어있으면 느림  
위처럼 해주면 gradle을 통하지 않고  
intelliJ에서 자바를 바로 띄워서 돌림

#### 섹션 1. 프로젝트 환경설정

https://www.thymeleaf.org/  
springboot-dev-tools 라이브러리 설치하면 서버 재시작 없이 recompile로 html 변경 사항 반영 가능

#### 섹션 2. 스프링 웹 개발 기초

정적컨텐츠
파일 그대로 전달
웹브라우저 -> 내장톰캣서버 -> 스프링 컨테이너 -> 우선 컨트롤러에서 찾음 -> 없으면 static

MVC와 템플릿 엔진
MVC 모델, 템플릿 엔진, 화면

API
JSON 데이터 포맷으로 전달

변수는 private  
getter, setter는 public

javaBean 표준 방식

@ResponseBody
return 문자 or 객체
문자는 문자 그대로 http body에
객체는 JSON 형태로(default)

웹브라우저 -> 내장톰캣서버 -> 스프링 컨테이너  
@ResponseBody가 없다 -> viewResolver  
있다 -> HttpMessageConverter  
  있는데 문자 -> StringConverter  
  있는데 객체 -> JsonConverter

객체를 JSON으로 바꿔주는 라이브러리 대표 2가지  
잭슨, Gson  
스프링은 잭슨

#### 섹션 3. 회원 관리 예제 - 백엔드 개발

비즈니스 요구사항 정리  
데이터: 회원ID, 이름  
기능: 회원 등록, 조회  
아직 데이터 저장소가 선정되지 않음(가상의 시나리오)  

Assertions.assertEquals(member, result);
expected = member
같으면 초록 다르면 빨강

shift + F6 rename

@AfterEach  
각 테스트 함수가 실행되고나서 매번 실행  
ex) 멤버리스트 삭제하는 로직 넣어서 매번 clear  

각 테스트 함수는 서로 연관성이 없어야한다.  

TDD 테스트 주도 개발  
테스트 케이스를 먼저 만들고 로직을 구현  

코드가 몇만 몇십만이 되면 테스트 코드 없이 구현하는 것은 불가능  
테스트 관련 깊게 공부 필요  

ctrl + shift + T
테스트 케이스 작성

private static Map<Long, Member> store = new HashMap<>();
각각 다른 class에서 new로 새로운 인스턴스를 만들어도 static일 때는 변수가 동일?
static - 여러 객체가 해당 메모리를 공유

DI(dependency injection)

#### 섹션 4. 스프링 빈과 의존관계

AutoWired
스프링 컨테이너에서 멤버 서비스를 가져온다.
컨트롤러에 AutoWired와 서비스의 @Service를 연결

component scan

@Component 애노테이션이 있으면 스프링 빈으로 자동 등록된다.

메인 함수가 있는 파일이 속한 패키지 하위만 빈 등록

싱글톤
컨트롤러 서비스 레포지토리 1개씩

주로 싱글톤 사용

DI
생성자 주입 - 권장  
필드 주입 - 변수에 autowired -> 안좋음(테스트 코드에서 사용) 
setter 주입 - set함수가 public으로 되어있어야되기때문에 다른 소스에서 변경 가능


#### 섹션 5. 회원 관리 예제 - 웹 MVC 개발

#### 섹션 6. 스프링 DB 접근 기술

다형성
하나의 인터페이스를 두고 구현체를 변경

@SpringBootTest
스프링 컨테이너를 띄워서 테스트 진행

@Transactional
트랜잭션 후 커밋 전에 롤백

단위 테스트
순수 자바

통합 테스트
스프링을 띄우고 하는 테스트

단위 테스트로만 가능한 환경이 좋음  
통합 테스트만 가능하다면 테스트 설계가 잘못됐을 확률이 높음

 JDBC API로 직접 코딩 -> 스프링 JdbcTemplate -> JPA

 JPA를 사용하면 SQL 보다는 객체 중심으로 고민을 할 수 있음  
 SQL과 데이터 중심 설계에서 객체 중심의 설계로 패러다임 전환

#### 섹션 7. AOP

AOP  
Aspect Oriented Programming
관점지향 프로그래밍
공통 관심사항과 핵심 관심사항을 분리
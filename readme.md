## 1차 요구사항 구현
- [x] 유저가 루트 url로 접속시에 게시글 리스트 페이지(http://주소:포트/article/list)가 나온다.
- [x] 리스트 페이지에서는 등록 버튼이 있고 버튼을 누르면 http://주소:포트/article/create 경로로 이동하고 등록 폼이 나온다.
- [x] 게시글 등록을 하면 http://주소:포트/article/create로 POST 요청을 보내어 DB에 해당 내용을 저장한다.
- [x] 게시글 등록이 되면 해당 게시글 리스트 페이지로 리다이렉트 된다. 페이지 URL 은 http://주소:포트/article/list 이다.
- [x] 리스트 페이지에서 해당 게시글을 클릭하면 상세페이지로 이동한다. 해당 경로는 http://주소:포트/article/detail/{id} 가 된다.
- [x] 게시글 상세 페이지에는 id에 맞는 게시글 데이터와 목록 버튼이 있다. 목록 버튼을 누르면 게시글 리스트 페이지로 이동하게 된다.

- (추가 기능이나 구현기능설명이 필요한 경우 서술)
- layout 기능을 추가하여 html을 꾸며줌
- create 페이지에서 취소 버튼을 만들어서 취소를 누르면 list 페이지로 이동하게 설계
- ![list페이지.JPG](..%2F..%2FUsers%2FSBS%2FDesktop%2Flist%ED%8E%98%EC%9D%B4%EC%A7%80.JPG)
list 페이지
- 
- ![create 페이지.JPG](..%2F..%2FUsers%2FSBS%2FDesktop%2Fcreate%20%ED%8E%98%EC%9D%B4%EC%A7%80.JPG)

create 페이지

![detail페이지.JPG](..%2F..%2FUsers%2FSBS%2FDesktop%2Fdetail%ED%8E%98%EC%9D%B4%EC%A7%80.JPG)

detail 페이지
## 미비사항 or 막힌 부분
- ...

## MVC 패턴
### MVC 패턴이란?
-> MVC는 Model, View, Controller의 약자
하나의 애플리케이션,프로젝트를 구성할 때 그 구성요소를 세가지 역할로 구분하는 패턴

### 모델(Model)
-> 소프트웨어나 애플리케이션에서 정보 및 데이터 부분을 의미
Controller에게 받은 데이터를 조작(가공)하는 역할을 수행
즉, 데이터와 관련된 부분을 담당하며 값과 기능을 가지는 객체

Model이 가지는 규칙

`1. 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 함`

` 2. View나 Controller에 대해서 어떤 정보도 알지 말아야 함`

` 3. 변경이 일어나면, 변경 통지에 대한 처리 방법을 구현해야만 한다.`

### 뷰(View)
-> View는 입력 값이나 체크 박스 등과 같은 사용자 인터페이스 요소를 나타냄
Controller에게 받은 Model의 데이터를 사용자에게 시각적으로 보여주기 위한 역할을 수행
즉, 사용자에게 보여지는 화면이라고 볼 수 있다.

View가 가지는 규칙

`1. Model이 가지고 있는 정보를 따로 저장해서는 안된다.`

`2. Model이나 Controller를 알고 있을 필요가 없다.`

`3. 변경이 일어나면 변경통지에 대한 처리방법을 구현해야만 한다.`

### 컨트롤러(Controller)
-> Controller는 Model과 View 사이에서 데이터 흐름을 제어 함
사용자가 접근한 URL에 따라 요청을 파악하고 URL에 적절한 Method를 호출하여
Service에서 비즈니스 로직을 처리한다. 이후 결과를 Model에 저장하여 View에게 전달하는 역할을 수행한다.
Controller는 Model과 View의 역할을 분리하는 중요한 요소이다.

Controller가 가지는 규칙

`1. Model이나 View에 대해서 알고 있어야 한다.`

`2. Model이나 View의 변경을 모니터링 해야 한다.`

## 스프링에서 의존성 주입(DI) 방법 3가지 방법
의존 관계가 변경되지 않을 경우 : 생성자 주입
의존 관계가 선택적이거나 변경 가능한 경우 : 수정자 주입(setter 주입)

### 1. 생성자 주입
-> 생성자 주입은 생성자를 통해서 의존 관계를 주입받는 방식
생성자에 @Autowired를 하면 스프링 컨테이너에 @Component로 등록된
빈 생성자에 필드요한 빈들을 주입한다.

#### 특징
- 생성자 호출 시점에 1번만 호출 되는것을 보장
- 불변과 필수 의존 관계에 사용
- 생성자가 1개만 존재하는 경우 @Autowired를 생략해도 자동 주입
- 주입받을 필드를 final로 선언 가능

### 2. 수정자 주입(setter주입)
-> setter라 불리는 필드의 값을 변경하는 수정자 메서드를 통해서
의존 관계를 주입하는 방식
@Component를 통해 실행하는 클래스를 스프링 빈으로 등록하고 의존관계를 주입하게 된다. @Autowired가 있는 수정자들을 자동으로 의존관계 주입한다.

#### 특징
- 선택과 변경 가능성이 있는 의존 관계에서 사용
- 자바 빈 프로퍼티 규약의 수정자 메서드 방식을 사용하는 방법
- set필드명 메서드를 생성하여 의존관계를 주입
- @Autowired를 입력하지 않으면 실행이 되지 않는다.


### 3. 필드 주입
->필드에 @Autowired를 붙여서 바로 주입하는 방법

#### 특징
- 코드가 간결해진다
- 대신 외부에서 변경이 불가능하여 테스트하기 어려운 단점이 존재
- DI 프레임워크가 없으면 아무것도 할수 없음.
- 애플리에키션의 실제 코드와 상관없는 특정 테스트를 하고 싶을때 사용
- 정상적으로 작동되게 하려면 결국 setter가 필요
- 만약, 의존관계를 필수적으로 넣지 않으려면 @Autowired(required-false) 옵션 처리를 통해 필수가 아님을 명시할수 있다.

## JPA의 장점과 단점
- JPA 개념
  -> Java Persistence API 는 자바의 ORM 기술의 표준
-
-> 구현체가 따로 없으며 ORM 프레임 워크를 선택하여 사용

### 장점
1. 생산성
   -메서드 호출만으로 쿼리를 수행
   ->SQL 반복 작업을 하지 않으므로 생산성 향상

2. 유지보수
- 테이블 칼럼 변경 시 이전에는 SQL을 모두 확인 후 수정 필요
- JPA는 JPA가 대신 작업을 수행 하므로 유지 보수 측면에서 장점이 있음

3. 특정 벤더에 종속적이지 않음
- 여러 DB벤더(MySQL,Oracle 등)마다 다른 SQL을 사용하기 때문에
  DB변경이 어려움
- JPA는 추상화된 데이터 접근 계층을 제공하여 특정 벤더에 종속적이지 않음
  -> 어떤 DB를 사용하고 있는지만 설정하면 얼마든지 DB 변경 가능

### 단점
1. 성능
   -메서드 호출로 쿼리를 실행하는 건 내부적인 동작이 많다는 의미
   -직접 SQL을 호출하는 것보다 성능이 낮을 수 있음

2. 런닝커브
   -JPA를 사용하기 위해서는 학습해야 할 것들이 많음
   -JPA를 사용해도 SQL을 알아야 Hibernate가 수행한 쿼리 확인 및 성능
   모니터링이 가능함


## HTTP GET 요청과 POST 요청의 차이
### GET 방식
-> GET방식은 HTTP Method 중 하나로 주로 서버에 데이터를 조회할때(리소스를 조회) 사용합니다.
-> URL을 통해 모든 파라미터를 전달하기 때문에 주소창에 전달 값이 노출되고,
URL길이가 제한이 있기 때문에 전송 데이터 양이 한정 되어있으며,
형식에 맞지 않으면 인코딩해서 전달해야함, URL에 파라미터가 노출되기 때문에
GET방식은 중요한 정보를 다루면 안됨(보안)

### 특징
- GET 방식의 요청은 캐시가 가능함
- GET 방식의 요청은 브라우저 히스토리에 남음
- GET은 SELECT 성향이 있어 서버에서 어떠한 데이터를 가져와서 보여주는 용도로 활용
- GET은 CRUD기능 중에 R-Read(조회) 역할

### POST 방식
-> POST방식은 HTTP Method 중 하나로 주로 서버에 데이터(리소스)를 생성할때 사용 합니다.

### 특징
- POST 방식의 요청은 캐시 되지않음.
- POST 방식의 요청은 히스토리에 남지 않음.
- POST 방식은 서버의 값이나 상태를 바꾸기 위해 활용
- GET은 CRUD 기능 중에 C-Create(생성)의 역할

### 결론
- GET은 서버에서 데이터를 조회할때, POST는 서버에 데이터를 생성 혹은 수정 할때 사용
- CRUD 기능으로 비유하면 GET은 Read(조회), POST는 Create(생성)에 가까움
- GET은 URL 파라미터에 요청하는 데이터를 담아 보내기에 HTTP 메시지에 대한 Body가 없음
- POST는 Body에 데이터를 담아 보내기에 HTTP 메시지에 Body가 존재

- [멱등성]
  -GET 방식의 요청은 멱등성이 보장된다 (POST를 제외한 나머지 HTTP Method는 멱등성이 보장 된다)
  -POST 방식의 요청은 멱등성이 보장되지않는다 (HTTP Method중 하나인 PATCH 또한 멱등성이 보장 되지 않음)

### 멱등성(idempotent) 이란?
- 멱등의 사전적 정의는 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질을 의미
  GET은 리소스를 조회한다는 점에서 여러 번 요청 하더라도 응답이 똑같을 것
  반대로 POST는 리소스를 새로 생성하거나 업데이트할 때 사용 되기 때문에 멱등이 아니라고 볼 수 있다. (POST 요청이 발생하면 서버가 변경될 수 있다,)
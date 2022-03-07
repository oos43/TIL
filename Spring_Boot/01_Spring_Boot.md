> [실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1/dashboard) 강의를 들으며 궁금한 부분을 공부하고 정리하는 페이지입니다.

<br>

## 프로젝트 환경설정

### Thymeleaf
- view template의 하나
- 웹과 독립 실행형 환경을 위한 최신의 서버 사이드 자바 템플릿 엔진이다.  
- 현대 HTML5 JVM 웹 개발에 이상적이다.

### Lombok
- 자바 라이브러리
- 반복되는 코드 작성을 어노테이션으로 대신할 수 있게 해준다.  
  ex. @Setter, @Getter
- 컴파일 과정에서 어노테이션으로 작성된 부분을 코드로 생성해준다.

### 서버 사이드 렌더링
- [서버사이드 렌더링 (개발자라면 상식으로 알고 있어야 하는 개념 정리)](https://www.youtube.com/watch?v=iZ9csAfU5Os)
- __CSR (클라이언트 사이드 렌더링)__  
  서버에서 (body 안에 아이디와 어플리케이션에서 필요한 자바스크립트 링크만 들어 있는) 인덱스 HTML파일을 클라이언트에 보내면 처음에는 빈 화면만 보이게 됨  
  링크된 자바스크립트 파일과 필요한 데이터를 서버로부터 받아 동적으로 HTML을 생성해 최종적인 어플리케이션을 보여줌
- __SSR (서버 사이드 렌더링)__  
  웹사이트에 접속하면 서버에서 필요한 데이터를 모두 가져와 HTML파일을 만들어서 동적으로 제어할 수 있는 소스코드와 함께 클라이언트에 보냄

### HikariCP
- Database Connection Pool을 관리해주는 역할을 한다.
- 미리 정해놓은 만큼의 connection을 pool에 담아 놓고 요청이 들어오면 thread가 connection을 요청하고 HikariCP가 pool 내에 있는 connection을 연결해준다.

### given-when-then 패턴
- 테스트 코드를 작성하는 표현 방식
- 준비 - 실행 - 검증

### Unit Test (단위 테스트)
- 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차  
  모든 함수와 메소드에 대한 테스트 케이스를 작성하는 절차

### JUnit
- 자바용 단위 테스트 프레임워크

### AssertJ
- 테스트 코드를 작성할 때 유용한 라이브러리

### 메모리 모드로 테스트 하기
- test - resources - application.yml 추가
- url을 __jdbc:h2:mem:test__ 로 변경
- h2 데이터베이스와 연결하지 않고도 테스트 가능
- 별도의 설정이 없으면 스프링 부트가 메모리 모드로 테스트 하기 때문에 application.yml이 없어도 가능함

## 명령어

### cmd 명령어
- __dir__  
  특정 디렉토리에 포함된 모든 파일과 하위 디렉토리를 나열하는 명령어
- __cd__  
  change directory  
  폴더를 이동하는 명령어
- __gradlew build__  
  jar 빌드 만드는 명령어

### IntelliJ 단축키
- 검색 : Ctrl + Shift + F
- Alt + Enter
- Test : Shift + Ctrl + T
- Preference : Ctrl + Alt + S
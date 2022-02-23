> [실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1/dashboard) 강의를 들으며 궁금한 부분을 공부하고 정리하는 페이지입니다.

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

### EntityManager & @Transactional
- 엔티티 매니저에서 수행되는 모든 로직은 트랜잭션 안에서 수행되어야 한다.
- 트랜잭션 : 하나의 작업 단위
## 테스트

### Unit Test (단위 테스트)
- 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차  
  모든 함수와 메소드에 대한 테스트 케이스를 작성하는 절차

### given-when-then 패턴
- 테스트 코드를 작성하는 표현 방식
- 준비 - 실행 - 검증

### JUnit
- 자바용 단위 테스트 프레임워크
- @RunWith(SpringRunner.class) : JUnit 실행시 Spring과 엮어서 실행하기 위해 필요한 어노테이션

### AssertJ
- 테스트 코드를 작성할 때 유용한 라이브러리

### 메모리 모드로 테스트 하기
- test - resources - application.yml 추가
- url을 __jdbc:h2:mem:test__ 로 변경
- h2 데이터베이스와 연결하지 않고도 테스트 가능
- 별도의 설정이 없으면 스프링 부트가 메모리 모드로 테스트 하기 때문에 application.yml이 없어도 가능함

### Assert 클래스 메소드
- assertEquals(String message, Object expected, Object actual) : expected와 actual이 같은지 확인하는 메소드
- fail(String message) : fail 코드에 도달하면 테스트 실패

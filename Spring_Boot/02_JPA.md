> [실전! 스프링 부트와 JPA 활용1 - 웹 애플리케이션 개발](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1/dashboard) 강의를 들으며 궁금한 부분을 공부하고 정리하는 페이지입니다.

<br>

## 도메인 분석 설계

### 요구사항 분석
- 실무에서는 다대다 관계를 일대다, 다대일 관계로 풀어 쓰는 것이 좋다.
- 양방향 연관 관계보다는 단방향 연관 관계를 쓰는 것이 좋다.
  
### 엔티티 타입 / 값 타입
- __엔티티 타입__
  - @Entity로 정의하는 객체
  - 식별자를 통해 추적 가능
- __값 타입__
  - 단순히 값으로 사용하는 자바 기본 타입 또는 객체
  - 추적 불가 (식별자 X)
  - 기본 값 타입, 임베디드 타입이 있음

### 상속 관계 매핑
- 객체의 상속 구조와 DB의 슈퍼타입, 서브타입 관계를 매핑하는 것
  #### 1. 싱글 테이블 전략 (SINGLE_TABLE)
  - 하나의 테이블만 사용하고, 구분 컬럼(DTYPE)으로 어떤 자식 데이터가 저장되었는지 구분함
  - 자식 엔티티가 매핑한 컬럼에 모두 null을 허용해야 함
  #### 2. 조인 테이블 전략 (JOINED)
  #### 3. TABLE_PER_CLASS 전략

### 연관관계 매핑 분석
- 일대다, 다대일의 양방향 관계일 경우 연관관계의 주인을 정해야 하는데, 외래키가 있는 쪽을 연관관계의 주인으로 정하는 것이 좋다.
- 연관관계의 주인 쪽에 값을 세팅해야 값이 변경된다.
#### 연관관계의 주인
- 두 객체 연관관계 중 하나를 정해서 테이블의 외래키를 관리해야 하는데 이를 연관관게의 주인이라 함

### 연관관계 편의 메서드
- 객체에 양방향 연관관계를 한 번에 설정하는 메서드
- 예를 들어, Member와 Order가 양방향 연관관계일 때
```JAVA
public void setMember(Member member) {
  this.member = member;
  member.getOrders().add(this);
}
```

### @Id, @GeneratedValue
- 기본키 매핑 시 사용하는 어노테이션
- 직접 할당 시에는 @Id만 사용하고,  
  자동 생성 시에는 @Id, @GeneratedValue를 같이 사용함

### 즉시로딩 (FetchType.EAGER) / 지연로딩 (FetchType.LAZY)
- 즉시로딩
  - 데이터를 조회할 때 연관된 정보를 join을 통해 모두 가져옴
- 지연로딩
  - __프록시__ 를 사용해 데이터를 조회할 때 연관된 객체를 필요할 때 가져올 수 있음
  - 프록시 객체는 실제 엔티티를 참조하고 있음

### EntityManager 사용
- persist : 영속성 컨텍스트에 객체를 넣고, 트랜잭션이 커밋되는 시점에 insert 쿼리가 날아가 DB에 반영됨
- find(타입, PK) : 단건 조회
- createQuery(JPQL, 반환 타입)
- getResultList : 결과가 하나 이상일 때 리스트를 반환
- setParameter : 파라미터 바인딩

### JPQL
- Java Persistence Query Language
- sql은 테이블을 대상으로 하는 쿼리
- jpql은 엔티티 객체를 대상으로 하는 쿼리

### EntityManager & @Transactional
- JPA의 엔티티 매니저에서 수행되는 모든 데이터 변경, 로직은 트랜잭션 안에서 수행되어야 한다.
  - 트랜잭션 : 하나의 작업 단위
- 클래스 레벨에서 @Transactional 어노테이션을 쓰면 public 메소드들에 적용됨
  - @Transactional(readOnly = true) 를 추가하면 조회 성능을 최적화함

### 테스트
- @Transactional : 테스트에서는 트랜잭션을 commit 하지 않고 rollback 하기 때문에 insert 쿼리가 날아가지 않음
- insert 쿼리를 확인하고 싶으면 EntityManager를 만들고 flush 메소드 사용
  - flush : 영속성 컨텍스트에 있는 변경이나 등록 내용을 데이터베이스에 반영
- assertEquals(member, memberRepository.findOne(saveId));
  - member와 memberRepository.findOne(saveId)가 같으면 성공
  - 이렇게 확인하는 게 가능한 이유는 JPA에서 같은 트랜잭션 안에서 PK 값이 같은 엔티티는 같은 영속성 컨텍스트 안에서 하나로 관리되기 때문

### 어노테이션
- @PersistenceContext : Spring이 생성한 EntityManager를 주입하는 어노테이션
- @PersistenceUnit : EntityManagerFactory를 직접 주입하고자 할 때 쓰는 어노테이션

### casecade = CasecadeType.ALL
```JAVA
@Entity
public class Order {

  @OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
  private List<OrderItem> orderItems = new ArrayList<>();
}

persist(orderItem);
persist(order);
```
- 기본적으로 모든 엔티티는 저장하고 싶으면 각자 persist 해줘야 함
- cascade = CascadeType.ALL 옵션을 추가하면 persist(order)라고만 써도 orderItem도 저장됨  
  (cascade는 persist를 전파함)
- private owner인 경우에만 사용해야 함 (OrderItem을 Order만 참조해서 씀, 다른 데서 OrderItem을 참조하는 경우에는 cascade를 사용하면 안 됨)

### 변경 감지와 병합
#### 1. 변경 감지 (Dirty Checking)
- 트랜잭션 안에서 엔티티에 변화가 생기면, 그 변경 사항을 자동으로 DB에 반영하는 것
#### 2. 병합 (Merge)
- 준영속 상태의 엔티티를 영속 상태로 변경할 때 사용하는 기능
- *주의!* 병합은 모든 필드를 다 변경하기 때문에 값이 없으면 null로 업데이트를 할 위험이 있음

__병합보다는 변경 감지__ 를 사용하도록 하자

### 준영속 엔티티

### Querydsl
- 동적 쿼리 작성에 유용한 라이브러리
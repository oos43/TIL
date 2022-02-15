# 07. OOP 관점에서 모델링이란 무엇일까요?

### 6. JPA는 OOP의 관점에서 모델링을 할 수 있게 해준다
- 콤포지션 (결합)   
  Car와 Engine 클래스가 있을 때 Car 클래스가 Engine 클래스를 사용하고 싶으면 상속이 아닌 콤포지션을 해야 함   
  (상속은 Engine이 Car의 부모 클래스가 되는 것이기 때문에 X)


  ```JAVA
    Class Engine {
        int id;
        int power;
    }

    Class Car {
        int id;
        String name;
        Engine engine;
    }
  ```
  JPA를 이용하면 이러한 클래스를 기반으로 데이터베이스를 자동 생성함   
  - Car 테이블의 컬럼 : id, name, engineId
  - Engine 테이블의 컬럼 : id, power
- 상속   
  ```JAVA
    Class EntityDate {
        Timestamp createDate;
        Timestamp updateDate;
    }

    Class Car extends EntityDate {
       (생략)
    }
  ```
  - JPA를 이용해서 테이블을 생성했을 때   
    Car 테이블의 컬럼 : id, name, engineId, createDate, updateDate
- 연관 관계

### 7. 방언 처리가 용이하여 Migration하기 좋고, 유지보수 하기도 좋다
- JPA는 다양한 방언(dialect)을 지원함 - Oracle, MariaDB, MySQL 등
- JPA는 추상화 객체와 연결되어 있고, 이 추상화 객체와 DB가 연결되어 있음   

<br>

> ▶ 방언 (Dialect)   
> Dialect는 JPA에서 제공하는 추상 클래스   
> JPA에서 원하는 Dialect를 설정하면 이에 맞게 쿼리를 생성함
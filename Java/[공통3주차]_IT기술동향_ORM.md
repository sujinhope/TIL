# 공통 3주차_기술동향

[TOC]

##### 출처

```
https://gmlwjd9405.github.io/2018/12/25/difference-jdbc-jpa-mybatis.html
```



### ORM

- Object Relational Mapping



##### 영속성(Persistence)

- 데이터를 생성한 프로그램이 종료되더라도 사라지지 않는 데이터의 특성

- 일반적으로는 메모리에 저장되어 있다가 프로그램이 종료되면 모두 사라진다.

- 데이터를 보존하기 위해 **파일 시스템, 관계형 DB, 객체 DB** 등을 활용하여 영구적으로 저장하여 영속성을 부여한다.

  

##### 데이터를 데이터베이스에 저장하는 방법 3가지

- JDBC
- Spring JDBC
- Persistence Framework(Hibernate, Mybatis)



##### Persistence Layer

- 프로그램 아키텍처에서 데이터에 영속성을 부여해주는 계층
- JDBC를 이용해서 직접 구현도 가능하지만 주로 Persistence Framework(Hibernate, Mybatis)를 이용하여 이루어진다.



##### Persistence Framework

- JDBC 프로그래밍의 복잡함이나 번거로움을 없애고 간단하게 DB와 연동되는 시스템을 빠르게 개발할 수 있으며 안정적인 구동ㅇ르 보장

- 구분

  - SQL Mapper - Mybatis

    - SQL <---- 매핑 ----> Object 필드

    - SQL 문장으로 직접 데이터베이스 데이터를 다룬다.

  - ORM - JPA, Hibernate

    - 데이터베이스 데이터 <---- 매핑 ----> Object 필드
    - 객체를 통해 간접적으로 DB 데이터를 다룬다.



##### JDBC(Java Database Connectivity)

- DB에 접근할 수 있도록 Java에서 제공하는 API

- 모든 Persistence Framework는 내부적으로 JDBC API를 이용

- DB에서 자료를 쿼리하거나 업데이트 하는 방법을 제공한다.

  ![image](https://user-images.githubusercontent.com/33229855/88633534-1a49e400-d0f0-11ea-8f92-d54df26094b9.png)







##### ORM이란?

- 객체 - 관계 매핑

- 객체와 관계형 데이터베이스의 데이터를 자동으로 매핑해주는 것

  객체지향 프로그래밍(클래스) - 관계형 데이터베이스(테이블)

- 이 때 객체모델과 관계형 모델 간의 불일치는 ORM을 통해 SQL을 자동으로 생성하여 해결한다.

- 객체를 통해 간접적으로 데이터베이스 데이터를 다룰 수 있음

- Persistence API라고도 한다.

  - ex - JPA, Hibernate

- ##### 장점

  - 객체지향적인 코드로 인해 더 직관적이고 비즈니스 로직에 더 집중할 수 있다.

    => SQL query가 아닌 직관적 코드(메서드)로 데이터를 조작할 수 있어서 개발자가 객체 모델로 프로그래밍하는데 더 집중할 수 있도록 도와준다.

    => SQL의 절차적, 순차적 접근이 아닌 객체지향적 접근으로 인해 생산성이 증가

  - 재사용 및 유지보수의 편리성 증가
  - DBMS에 대한 종속성이 줄어든다.
    - 자바에서 가공할 경우 equals, hashCode의 오버라이드같은 자바의 기능을 이용할 수 있고 간결하고 빠른 가공이 가능하다.
    - 프로그래머가 Object에 집중함으로써 DBMS를 교체하는 대규모 작업에도 비교적 적은 리스크와 시간이 소요된다.

  

- ##### 단점

  - 완벽한 ORM으로만은 서비스를 구현하기가 어렵다.
    - 프로젝트의 복잡성이 커질수록 난이도도 올라갈 수 있음
    - 잘못구현 시 속도 저하 및 일관성이 무너지는 심각한 문제가 발생할 수 있음
    - DBMS의 고유 기능을 이용하기 어려움(단점으로만 작용하는 것은 아님)
  - 프로시저가 많은 시스템에선 ORM의 객체지향적 장점을 활용하기 어려움





### MyBatis & JPA & Hibernate

##### Mybatis

- 개발자가 지정한 SQL, 저장 프로시저, 고급 매핑을 지원하는 SQL Mapper
- 원래 Apache Foundation의 iBatis였으나 생산성, 개발프로세스, 커뮤니티 등의 이유로 Google Code로 이전되면서 MyBatis로 바뀜
  - iBatis와 차이점 - JDK 1.5, Annotation, Dynatic SQL, XML Element
- **장점**
  - SQL에 대한 모든 컨트롤을 하고자 할 때 매우 적합
  - SQL쿼리들이 최적화되어있을 때 유용
- **단점**
  - 애플리케이션과 데이터베이스 간 설계에 대한 모든 조작을 하고자 할 때는 적합하지 않음
  - ==DAO와 의존성이 강함==(테이블에 컬럼이 하나 추가될 경우 관련된 모든 SQL문을 수정해야 함.)



##### JPA(Java Persistent API)

- 자바 ORM기술에 대한 API 표준 명세. Java에서 제공하는 API
  - ==ORM을 사용하기 위한 표준 인터페이스를 모아둔 것==
  - 기존 EJB에서 제공되던 Entity Bean을 대체하는 기술
- JPA 구성요소
  - javax.persistance 패키지로 정의된 API
  - JPQL(Java Persistence Query Language)
  - 객체/관계 메타데이터
- 사용자가 원하는 JPA 구현체를 선택해서 사용할 수 있다.
  - Hibernate, EclipseLink, DataNucleus, OpenJPA, TopLink Essentials 등
  - 위 구현체들을 ORM Framework라고 부른다.



##### Hibernate

- JPA의 구현체 중 하나
- 개발자가 직접 SQL을 작성하지 않을 뿐 Hibernate가 지원하는 메서드 내부에서 JDBC API가 동작하고 있다.
- HQL(hibernate Query Language)라 불리는 SQL과 매우 비슷한 쿼리 언어를 포함하고 있음.
  - 객체 지향적이며 상속, 다형성, 관계 등의 객체지향 강점을 누릴 수 있다.
  - 자바 클래스와 프로퍼티 이름을 제외하고 **대소문자를 구분**한다.
  - SQL에서 지원하지 않는 **페이지네이션**이나 동적 프로파일링과 같은 향상된 기능을 제공
  - 쿼리결과로 **객체를 반환**하며 프로그래머에 의해 생성되고 직접적으로 접근할 수 있다.
  - **장점**
    - 객체지향적으로 데이터를 관리할 수 있기 때문에 비즈니스 로직에 집중할 수 있으며 객체지향 개발이 가능하다.
    - 테이블 생성, 변경, 관리가 쉬움
    - 로직을 쿼리에 집중하기보다는 객체 자체에 집중할 수 있음.
  - **단점**
    - 어려움 + 잘 이해하지 않고 사용하면 데이터 손실이 있을 수 있음
    - 성능상 문제가 있을 수 있음




















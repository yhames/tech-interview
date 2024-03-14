# Tech Interview - JPA

JPA란?

Spring JDBC란?

JDBC, Spring JDBC, MyBatis, ORM, JPA, Hibernate, Spring Data JPA에 대해 각각 설명해주세요.

MyBatis란?

Mybatis 사용해본 경험이 있는지? JPA와 Mybatis는 무엇이 다른지?

DataSource는 무엇인가요?

DB Connection Pool 이란?

영속성 컨텍스트는 무엇인가요?

Springboot에서의 커넥션 풀로는 어떤 것을 사용하는지 설명해주세요.

Connection Pool을 쓰는 이유는? 단순히 커넥션을 새로 만드는 것과 차이는?

ORM이 무엇인지 설명해주세요.

ORM이 편하고 좋은데, SQL을 알아야만 할까요?

객체간의 상속관계를 DB에 적용시키기 위해서는 어떻게 해야 할까요?

JPA FetchType - LAZY와 EAGER 각각 어떤 기준으로 사용하나요?

JPA N+1 문제가 무엇인가요?

JPA와 같은 ORM을 사용하면서 쿼리가 복잡해지는 경우에는 어떻게 해결하는게 좋을까요?

동적 쿼리란 무엇이고 언제 동적 쿼리를 사용하나요?

트랜잭션을 추상화해서 사용하는 이유를 알고 계시나요?

트랜잭션 동기화 매니저의 역할에 대해 안다면, 아는대로 설명해주세요.

Spring을 사용해 트랜잭션을 적용하는 방법 2가지에 대해 설명해주세요.

@Transactional 사용해본 적 있는지? 어떻게 사용했는지 설명해주세요.

@Transactional을 사용한 메서드 내부에 FileIOException이 발생했을 때 어떻게 동작하는지 알려주세요.

@Transactional를 스프링 Bean의 메소드 A에 적용하였고, 해당 Bean의 메소드 B가 호출되었을 때, B 메소드 내부에서 A 메소드를 호출하면 어떤 요청 흐름이 발생하는지 설명해주세요.

A 라는 Service 객체의 메소드가 존재하고, 그 메소드 내부에서 로컬 트랜잭션 3개(다른 Service 객체의 트랜잭션 메소드를 호출했다는 의미)가 존재한다고 할 때, @Transactional을 A 메소드에 적용하면 어떤 요청 흐름이 발생하는지 설명해주세요.

@Transactional에 readOnly 속성을 사용하는 이유에 대해서 설명해주세요.

# TransactionManager

## 필요성
DB 접근 기술마다 트랜잭션 처리를 하는 방법이 다 다르다

jdbc 트랜잭션의 경우
```java
try{
    con.setAutoCommit(false); // 트랜잭션 시작
    biz.logic();
    con.commit();
} catch (Exception e) {
        con.rollback();
} finally {
    release(con);
}
```

jpa의 경우
```java
EntityTransaction tx = em.getTransaction();

try {
    tx.begin();
    biz.logic();
    tx.commit();
} catch (Exception e) {
    tx.rollback();
} finally {
    em.close();
}
```

**추상화가 필요하다**

스프링의 트랜잭션 추상화 클래스 = `PlatformTransactionManager`
그것을 구현한 `JpaTransactionManager` 등이 존재한다. -> 트랜잭션을 시작하는 `doBegin` 메소드에서 `EntityManager`를 생성해서 저장하는 로직이 있다.

## 
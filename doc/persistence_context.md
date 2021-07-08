## 영속성 관리 - 내부 동작 방식
```java
//객체를 생성한 상태(비영속)
Member member = new Member();
member.setId("member1");
member.setUsername(“회원1”);
EntityManager em = emf.createEntityManager();
em.getTransaction().begin();
 //객체를 저장한 상태(영속)
em.persist(member);
 //회원 엔티티를 영속성 컨텍스트에서 분리, 준영속 상태
 em.detach(member);
 //객체를 삭제한 상태(삭제)
  em.remove(member);
```

### 영속성 컨텍스트의 이점
- 엔티티 조회에 대한 1차 캐시
- 동일선(identity) 보장
- 트랜잭션을 지원하는 쓰기 지원
- 변경 감지
- 지연 로딩

### 플러시
> 영속성 컨텍스트의 변경내용을 데이터베이스에 반영
- 변경감지
- 수정된 엔티티 쓰기 지연 SQL 저장소에 등록
- 쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송
- 영속성 컨텍스트를 비우지 않음!!
- 영속성 컨텍스트의 변경내용을 데이터베이스에 동기화
- 트랜잭션이라는 작업 단위가 중요 -> 커밋 직전에만 동기화

#### 영속성 컨텍스트를 플러시하는 방법
- em.flush() > 직접호출
- 트랜잭션 커밋 > 플러시 자동 호출
- JPQL 쿼리 실행 - 플러시 자동 호출


### 준영속 상태
- 영속 > 준영속
- 영속 상태의 엔티티가 영속성 컨텍스트에서 분리(detached)
- 영속성 컨텍스트가 제공하는 기능을 사용 못함

#### 준영속 상태로 만드는 방법
- em.detach(entity)
    - 특정 엔티티만 준영속 상태로 전환
- em.clear()
    - 영속성 컨텍스트를 완전히 초기화
- em.close()
    - 영속성 컨텍스트를 종료
    
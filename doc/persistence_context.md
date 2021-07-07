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
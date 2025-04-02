---
tags:
  - EntityManager
  - TI_back
  - JPA
---
## 엔티티 매니저에 대해 설명해주세요.

---

>JPA(Java Persistence API)의 핵심 인터페이스 중 하나로, 데이터베이스와 애플리케이션 사이에서 엔티티 객체를 관리하는 역할을 합니다. 한마디로 **엔티티의 생명 주기를 관리하고, 데이터베이스와의 모든 상호작용을 처리하는 관리자**이다

### 주요 기능

|기능|설명|
|---|---|
|`persist()`|엔티티를 영속 상태로 만들어 DB에 저장 준비|
|`find()`|기본 키(PK)로 엔티티 조회|
|`remove()`|엔티티 삭제|
|`merge()`|준영속 상태의 엔티티를 영속 상태로 변경|
|`flush()`|영속성 컨텍스트의 변경 내용을 DB에 반영|
|`clear()`|영속성 컨텍스트 초기화 (1차 캐시 비움)|
|`detach()`|특정 엔티티를 영속성 컨텍스트에서 분리 (더 이상 관리하지 않음)|

---

### 예시 코드 (Spring Boot 기준)

```java
@Service
@RequiredArgsConstructor
public class MemberService {

    private final EntityManager em;

    public Member findMember(Long id) {
        return em.find(Member.class, id);
    }

    public void saveMember(Member member) {
        em.persist(member);
    }

    public void deleteMember(Long id) {
        Member member = em.find(Member.class, id);
        if (member != null) {
            em.remove(member);
        }
    }
}
```

---

### 엔티티 생명 주기 (JPA 관점)

1. **비영속(New)**: `new Member()`처럼 단순 객체 생성
2. **영속(Managed)**: `em.persist(member)`로 엔티티 매니저가 관리
3. **준영속(Detached)**: `em.detach(member)`나 `em.clear()` 호출 시 관리 종료
4. **삭제(Removed)**: `em.remove(member)`로 삭제 예약됨
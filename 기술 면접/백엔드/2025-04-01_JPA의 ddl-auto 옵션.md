---
tags:
  - TI_back
  - JPA
  - ddl-auto
---
## JPA의 ddl-auto 옵션은 각각 어떤 동작을 하고 어떤 상황에서 사용해야 할까요?

---

>`spring.jpa.hibernate.ddl-auto` 옵션은 JPA(Hibernate)가 **애플리케이션 실행 시 데이터베이스 스키마(테이블 등)를 어떻게 다룰지를 설정**하는 옵션이야. 개발, 테스트, 운영 환경마다 이 옵션을 다르게 설정해야 하니까 **정확하게 이해하고 써야 한다**

###  `spring.jpa.hibernate.ddl-auto` 값 정리

| 옵션 값          | 동작                             | 설명                         | 사용 추천 환경                |
| ------------- | ------------------------------ | -------------------------- | ----------------------- |
| `none`        | 아무 작업 안 함                      | Hibernate가 DDL에 아무 영향도 안 줌 | ✅ 운영 환경 (프로덕션)          |
| `create`      | 앱 실행 시 기존 테이블 삭제 후 다시 생성       | 데이터 다 날아감                  | 개발/테스트 전용               |
| `create-drop` | 앱 실행 시 테이블 생성, 종료 시 삭제         | 테스트 후 흔적 없이 삭제됨            | 테스트 환경 (JUnit 등)        |
| `update`      | 변경된 엔티티 기준으로 테이블 **자동 수정**     | 컬럼 추가/변경은 가능, 삭제는 안 됨      | 빠른 개발 중 유용하지만 주의        |
| `validate`    | 매핑된 엔티티와 DB 테이블이 **일치하는지 확인만** | 불일치 시 에러, 수정 안 함           | 스키마가 미리 있는 운영/QA 환경     |
| `none`        | 아무 작업도 하지 않음                   | 직접 DB 마이그레이션 툴 사용 시        | Flyway, Liquibase 쓰는 경우 |

---

### 🛠 옵션별 실제 예시 시나리오

#### `create`

- **개발 초기**, 자주 테이블 구조 바뀔 때
- 예: 프로젝트 막 시작해서 엔티티 자주 고칠 때

```yaml
spring.jpa.hibernate.ddl-auto: create
```

→ 실행 시 테이블 싹 밀고 새로 만듦

---

#### `update`

- **개발 중간**, 데이터는 유지하면서 테이블 자동 수정 원할 때
- 단점: 컬럼 삭제 X, 구조 망가질 수도 있음

```yaml
spring.jpa.hibernate.ddl-auto: update
```

→ 가장 편하지만, 신뢰성 낮음

---

#### `validate`

- DB 스키마는 DBA가 설계하고, 앱에서는 일치 여부만 체크
- 운영에 딱 적합한 형태

```yaml
spring.jpa.hibernate.ddl-auto: validate
```

→ DB와 엔티티 안 맞으면 앱 실행 자체가 막힘

---

#### `none`

- 완전 수동 관리, Flyway/Liquibase 사용 시 최적
- DB는 손 안 대고, 마이그레이션 도구가 관리

```yaml
spring.jpa.hibernate.ddl-auto: none
```

---

### 실무에서 주의할 점

- **운영 배포에 `update` 쓰면 큰일** 날 수도 있음 (컬럼이 꼬이거나, 의도치 않게 덮어씀)
- 운영은 대부분 `validate` 또는 `none`을 씀
- CI/CD에서는 `create-drop`으로 테스트 후 데이터 초기화하는 경우 많음

---

### 요약 키워드

- `create` → 처음부터 새로
- `create-drop` → 테스트 후 깨끗하게
- `update` → 편하지만 위험
- `validate` → 실수 방지용
- `none` → 완전 수동 관리
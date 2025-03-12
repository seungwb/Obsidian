## 📌 1. **데이터 정의어 (DDL - Data Definition Language)**

데이터베이스 객체(테이블, 뷰, 인덱스 등)를 생성하고 관리하는 명령어들.

### 1️⃣ **테이블 생성 (`CREATE TABLE`)**

```sql
CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```
### 2️⃣ **테이블 수정 (`ALTER TABLE`)**

- 컬럼 추가

```sql
ALTER TABLE users ADD COLUMN age INT;
```

- 컬럼 수정

```sql
ALTER TABLE users MODIFY COLUMN name VARCHAR(100);
```

- 컬럼 삭제

```sql
ALTER TABLE users DROP COLUMN age;
```


### 3️⃣ **테이블 삭제 (`DROP TABLE`)**


```sql
DROP TABLE users;
```

### 4️⃣ **데이터 초기화 (`TRUNCATE TABLE`)**


```sql
TRUNCATE TABLE users;
```

> ⚠ `TRUNCATE`는 모든 데이터를 삭제하지만 테이블 구조는 유지함.

---

## 📌 2. **데이터 조작어 (DML - Data Manipulation Language)**

데이터를 조회하고 추가, 수정, 삭제하는 명령어들.

### 1️⃣ **데이터 삽입 (`INSERT INTO`)**



```sql
INSERT INTO users (name, email) VALUES ('홍길동', 'hong@example.com');
```

### 2️⃣ **데이터 조회 (`SELECT`)**


```sql
SELECT * FROM users;
```

- 특정 컬럼만 조회

```sql
SELECT name, email FROM users;
```

- 조건 조회 (`WHERE`)

```sql
SELECT * FROM users WHERE email = 'hong@example.com';
```

- 정렬 (`ORDER BY`)
```sql
SELECT * FROM users ORDER BY created_at DESC;
```

- 중복 제거 (`DISTINCT`)
```sql
SELECT DISTINCT email FROM users;
```

- 페이징 (`LIMIT`, `OFFSET`)
```sql
SELECT * FROM users LIMIT 10 OFFSET 20;
```

### 3️⃣ **데이터 수정 (`UPDATE`)**
```sql
UPDATE users SET name = '강감찬' WHERE id = 1;
```

### 4️⃣ **데이터 삭제 (`DELETE`)**

```sql
DELETE FROM users WHERE id = 1;
```

> ⚠ `DELETE` 사용 시 주의! `WHERE` 절을 생략하면 모든 데이터가 삭제됨.

---

## 📌 3. **데이터 제어어 (DCL - Data Control Language)**

사용자 권한을 관리하는 명령어들.

### 1️⃣ **권한 부여 (`GRANT`)**

```sql
GRANT SELECT, INSERT ON users TO 'user1'@'localhost';
```

### 2️⃣ **권한 회수 (`REVOKE`)**
```sql
REVOKE INSERT ON users FROM 'user1'@'localhost';
```

---

## 📌 4. **트랜잭션 제어어 (TCL - Transaction Control Language)**

트랜잭션을 관리하는 명령어들.

### 1️⃣ **트랜잭션 시작 (`START TRANSACTION`)**

```sql
START TRANSACTION;
```

### 2️⃣ **트랜잭션 저장 (`SAVEPOINT`)**

```sql
SAVEPOINT save1;
```

### 3️⃣ **트랜잭션 커밋 (`COMMIT`)**

```sql
COMMIT;
```

### 4️⃣ **롤백 (`ROLLBACK`)**

```sql
ROLLBACK TO save1;
```

---

## 📌 5. **고급 SQL 문법**

### 1️⃣ **JOIN (테이블 조인)**

- `INNER JOIN` (교집합)

```sql
SELECT 
	users.name
	, orders.amount 
FROM users 
INNER JOIN orders 
ON users.id = orders.user_id;
```

- `LEFT JOIN` (왼쪽 테이블 모든 데이터 포함)

```sql
SELECT 
	users.name
	, orders.amount 
FROM users 
LEFT JOIN orders 
ON users.id = orders.user_id;
```

- `RIGHT JOIN` (오른쪽 테이블 모든 데이터 포함)
```sql
SELECT 
	users.name
	, orders.amount 
FROM users 
RIGHT JOIN orders 
ON users.id = orders.user_id;
```

### 2️⃣ **서브쿼리 (Subquery)**

```sql
SELECT 
	name 
FROM users 
WHERE id = 
	(
		SELECT 
			MAX(id) 
		FROM users
	);
```

### 3️⃣ **집계 함수 (Aggregation)**

```sql
SELECT COUNT(*) FROM users;  -- 개수 
SELECT AVG(age) FROM users;   -- 평균 
SELECT SUM(amount) FROM orders; -- 합계 
SELECT MAX(age) FROM users;   -- 최댓값 
SELECT MIN(age) FROM users;   -- 최솟값
```

### 4️⃣ **GROUP BY & HAVING**

```sql
SELECT 
	age, 
	COUNT(*) 
FROM users 
GROUP BY age 
HAVING COUNT(*) > 1;
```

### 5️⃣ **CASE 문 (조건에 따라 값 반환)**

```sql
SELECT name,
CASE 
	WHEN age < 18 THEN '미성년자'
	WHEN age BETWEEN 18 AND 65 THEN '성인'
	ELSE '노년'
END AS category
FROM users;

```

---

## 🚀 **정리**

|SQL 유형|주요 명령어|
|---|---|
|DDL (정의)|`CREATE`, `ALTER`, `DROP`, `TRUNCATE`|
|DML (조작)|`INSERT`, `SELECT`, `UPDATE`, `DELETE`|
|DCL (제어)|`GRANT`, `REVOKE`|
|TCL (트랜잭션)|`COMMIT`, `ROLLBACK`, `SAVEPOINT`|
## 작성 순서

- SELECT - FROM - WHERE - GROUP BY - HAVING - ORDER BY
## 실행 순서

- FROM - WHERE - GROUP BY - HAVING - SELECT - ORDER BY

# Cassandra
## ✅ Cassandra란?

**Apache Cassandra**는 다음과 같은 특징을 가진 **NoSQL 데이터베이스**입니다:

* **분산형** (Distributed): 데이터를 여러 서버(노드)에 분산 저장합니다.
* **컬럼 패밀리형(Column-family)** 구조: RDBMS의 테이블과 비슷하지만, 유연한 스키마를 가짐.
* **높은 쓰기 성능**: 빠르게 데이터를 쓸 수 있음.
* **장애 허용(Fault-tolerant)**: 노드가 일부 죽어도 시스템 전체가 동작함.
* **CAP 이론에서 AP 지향**: 가용성(Availability) + 파티션 허용(Partition tolerance)을 우선시함.

---


## Index
1. [Cassandra & Memory](#1-cassandra--memory)
2. [Cassandra vs RDBMS](#2-cassandra-vs-rdbms)
3. [Cassandra vs Other NoSQL](#3-cassandra-vs-other-nosql)
4. [Cassandra CRUD: CQL (Cassandra Query Language)](#4-cassandra-crud-cql-cassandra-query-language)
5. [Cassandra Write Path vs RDBMS](#5-cassandra-write-path-vs-rdbms)


---

## 1. Cassandra & Memory
### ✅ Cassandra는 메모리 기반인가요?

**아니요. Cassandra는 기본적으로 디스크 기반**입니다.

* Cassandra는 데이터를 디스크에 저장합니다.
* 다만, **쓰기 작업 시에는 먼저 메모리에 쓰고**, 일정 시점에 디스크로 flush 합니다.

🔹 구성 요소로 보면:

| 구성 요소          | 설명                                 |
| -------------- | ---------------------------------- |
| **Memtable**   | 메모리에 저장되는 임시 데이터 (쓰기 시 먼저 여기에 저장됨) |
| **SSTable**    | 디스크에 저장되는 실제 데이터 파일                |
| **Commit log** | 장애 복구를 위한 로그 (디스크에 쓰임)             |

→ 즉, **쓰기 성능을 위해 메모리를 활용하지만, 기본적으로 디스크 기반입니다.**

---

### ✅ 메모리 기반 DB와의 비교

| 항목    | Cassandra                | Redis (예: 메모리 DB)         |
| ----- | ------------------------ | ------------------------- |
| 저장 방식 | 디스크 기반 (with 메모리 버퍼)     | 메모리 기반 (옵션으로 디스크 persist) |
| 주요 목적 | 대용량 분산 저장                | 초고속 읽기/쓰기, 캐시             |
| 용도    | 로그 저장, 센서 데이터, 대규모 트래픽 앱 | 실시간 캐싱, 세션 저장, 랭킹 등       |

---

### ✅ 언제 Cassandra를 쓰나요?

* 매우 **많은 양의 데이터를 빠르게 쓰고 싶을 때**
* **쓰기 지연이 낮고**, 장애가 나도 살아있는 시스템이 필요할 때
* 예: **IoT 데이터, 로그 저장, 타임시리즈 데이터, 추천 시스템 백엔드**

---

### 📌 요약

| 질문                | 답변                                    |
| ----------------- | ------------------------------------- |
| Cassandra는 DB인가요? | 네, NoSQL 분산 데이터베이스입니다.                |
| 메모리 DB인가요?        | 아니요. 디스크 기반입니다. 다만 쓰기 캐시에 메모리를 사용합니다. |
| 언제 쓰나요?           | 대용량 분산 저장, 빠른 쓰기, 장애 허용성이 필요할 때       |

---

## 2. Cassandra vs RDBMS
### ✅ Cassandra vs RDBMS 비교표

| 항목          | RDBMS (예: MySQL, PostgreSQL)    | Cassandra                                       |
| ----------- | ------------------------------- | ----------------------------------------------- |
| **데이터 모델**  | 테이블(행과 열 기반), 고정 스키마            | 컬럼 패밀리 모델, 유연한 스키마                              |
| **쿼리 언어**   | SQL (Structured Query Language) | CQL (Cassandra Query Language) – SQL과 유사하지만 제한적 |
| **스키마 변경**  | 엄격, 변경 시 마이그레이션 필요              | 유연, 컬럼 추가/삭제 자유로움                               |
| **확장성**     | 수직 확장(서버 사양 업그레이드) 위주           | 수평 확장(노드 추가로 성능 향상) 매우 용이                       |
| **데이터 일관성** | 강한 일관성 (ACID 보장)                | 가용성과 속도 우선, eventual consistency (최종 일관성) 기반    |
| **장애 허용**   | 마스터/슬레이브 구조로 장애 발생 시 복잡         | 마스터리스 구조, 노드 중 일부 장애 나도 작동 가능                   |
| **쓰기 성능**   | 낮거나 중간 (트랜잭션 보장으로 인해 속도 저하 가능)  | 매우 빠름 (쓰기 최적화 구조)                               |
| **읽기 성능**   | 빠름 (인덱스 기반 쿼리)                  | 적절함 (복제 및 구조에 따라 다름)                            |
| **적합한 용도**  | 금융, 회계, 사용자 관리 등 정형 데이터         | 로그 저장, IoT, 소셜 피드 등 대용량 실시간 데이터                 |
| **트랜잭션 지원** | 완전 지원 (ACID)                    | 기본적으로 트랜잭션 지원은 약함 (Lightweight transaction은 가능) |
| **복제/백업**   | 마스터-슬레이브 구조, 관리 필요              | 자동 복제 지원, 높은 가용성                                |

---

### ✅ 간단 요약

| 상황                           | 추천 DB            |
| ---------------------------- | ---------------- |
| 복잡한 조인, 정형화된 데이터, 트랜잭션 중요    | 👉 **RDBMS**     |
| 대용량 데이터, 빠른 쓰기, 고가용성, 분산 시스템 | 👉 **Cassandra** |

---

### 💡 예시로 이해하기

* **RDBMS 예시**: 은행 계좌 관리, 주문 관리 시스템, 사용자 인증
* **Cassandra 예시**:

  * 인스타그램 같은 **뉴스 피드**
  * 수백만 개의 **센서 데이터 수집**
  * 실시간 **로그 데이터 저장**



---


## 3. Cassandra vs Other NoSQL
### ✅ Cassandra, Redis, MongoDB 사용 예시

| DB 종류         | 주요 특징                                           | 대표 사용 사례                                                              | 실제 사용 기업/서비스                                                          |
| ------------- | ----------------------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **Cassandra** | - 분산형 NoSQL DB<br>- 쓰기 성능 우수<br>- 고가용성          | - 로그 수집 시스템<br>- IoT 센서 데이터 저장<br>- 뉴스 피드 타임라인 저장<br>- 주문 이벤트 스트리밍 저장 | ▶ Netflix – 영화/시청 기록<br>▶ Instagram – 사용자 피드<br>▶ Uber – 실시간 위치/주문 기록 |
| **Redis**     | - 인메모리 DB<br>- 초고속 응답<br>- 키-값 기반               | - 로그인 세션 저장<br>- 캐시 시스템<br>- 실시간 랭킹(점수 계산)<br>- 메시지 큐 / Pub-Sub       | ▶ Twitter – 타임라인 캐시<br>▶ GitHub – 세션 저장<br>▶ Tinder – 매칭 큐            |
| **MongoDB**   | - 문서형 NoSQL DB<br>- 유연한 스키마<br>- 복잡한 JSON 구조 저장 | - CMS(콘텐츠 관리 시스템)<br>- 사용자 프로필 저장<br>- 제품 카탈로그<br>- 블로그/댓글 시스템        | ▶ Facebook – 메시지/댓글 시스템<br>▶ eBay – 상품 카탈로그<br>▶ Forbes – CMS 콘텐츠 저장  |

---

### ✅ 간단 요약표

| 상황                          | 적합한 DB          |
| --------------------------- | --------------- |
| 빠른 쓰기와 장애 허용이 중요한 **분산 환경** | ✅ **Cassandra** |
| 초고속 응답, **캐시/세션/순위** 관리 필요  | ✅ **Redis**     |
| 유연한 구조의 **JSON/문서형 데이터** 저장 | ✅ **MongoDB**   |

---

### ✅ 예시 조합 (실무에서 같이 쓰이는 경우)

* **Redis + MongoDB**:
  → MongoDB에 저장된 제품 정보를 Redis로 캐싱하여 빠른 응답 제공
* **Cassandra + Kafka**:
  → Kafka로 받은 실시간 이벤트 로그를 Cassandra에 저장

  

---

## 4. Cassandra CRUD: CQL (Cassandra Query Language)
**Apache Cassandra의 CRUD(Create, Read, Update, Delete)** 작업은 \*\*CQL (Cassandra Query Language)\*\*을 사용해서 수행합니다.
SQL과 문법이 비슷하지만, **JOIN, 트랜잭션 등은 제한적**입니다.

### ✅ Cassandra에서의 CRUD 예시

#### 1. **Create (데이터 생성)**

```sql
INSERT INTO users (id, name, email) VALUES (1, 'Alice', 'alice@example.com');
```

* Cassandra는 INSERT = UPSERT 입니다.
  → 이미 존재하는 `id`가 있으면 **Update**처럼 동작합니다.

---

#### 2. **Read (데이터 조회)**

```sql
SELECT * FROM users WHERE id = 1;
```

* **Primary key가 없는 WHERE 조건은 허용되지 않음**
* WHERE 조건에는 **파티션 키 또는 인덱스**가 있어야 함

---

#### 3. **Update (데이터 수정)**

```sql
UPDATE users SET email = 'new_email@example.com' WHERE id = 1;
```

* `WHERE` 절은 **반드시 Primary Key 포함**
* 존재하지 않으면 row가 새로 생성됨 (Upsert 동작)

---

#### 4. **Delete (데이터 삭제)**

```sql
DELETE FROM users WHERE id = 1;
```

* 단일 row 삭제
* 컬럼만 삭제도 가능:

```sql
DELETE email FROM users WHERE id = 1;
```

---

### ✅ 기본 테이블 예시

```sql
CREATE TABLE users (
  id int PRIMARY KEY,
  name text,
  email text
);
```

---

### ✅ 특징 요약

| 작업     | CQL 예시   | 주의할 점                              |
| ------ | -------- | ---------------------------------- |
| Create | `INSERT` | INSERT = UPSERT                    |
| Read   | `SELECT` | WHERE에 반드시 Primary Key 필요          |
| Update | `UPDATE` | WHERE에 Primary Key 필요, 없으면 row 생성됨 |
| Delete | `DELETE` | 컬럼 또는 row 삭제 가능                    |

---

### ✅ Cassandra에서 가능한 SQL 기능 (CQL)

CQL은 SQL 문법과 비슷해서 사용하기 쉽습니다.

| SQL 문법   | Cassandra (CQL) 사용 가능 여부 | 예시                                                  |
| -------- | ------------------------ | --------------------------------------------------- |
| `SELECT` | ✅ 사용 가능                  | `SELECT * FROM users WHERE id = 1;`                 |
| `INSERT` | ✅ 사용 가능                  | `INSERT INTO users (id, name) VALUES (1, 'Alice');` |
| `UPDATE` | ✅ 사용 가능                  | `UPDATE users SET name = 'Bob' WHERE id = 1;`       |
| `DELETE` | ✅ 사용 가능                  | `DELETE FROM users WHERE id = 1;`                   |
| `WHERE`  | ✅ 제한적으로 가능               | 파티션 키나 인덱스가 있어야 조건 사용 가능                            |

---

### ❌ RDBMS처럼 **불가능한** 주요 SQL 기능

| 기능                  | Cassandra에서 지원 여부 | 설명                                                        |
| ------------------- | ----------------- | --------------------------------------------------------- |
| **JOIN**            | ❌ 불가능             | 관계형 조인을 지원하지 않음                                           |
| **GROUP BY**        | ❌ 제한적 또는 불가능      | 집계 함수는 거의 없음                                              |
| **HAVING**          | ❌ 없음              | 그룹 필터링 불가능                                                |
| **서브쿼리 (Subquery)** | ❌ 없음              | `SELECT ... FROM (SELECT ...)` 불가능                        |
| **트랜잭션**            | ❌ 없음              | ACID 트랜잭션 지원 안 됨 (단일 row 수준의 lightweight transaction만 가능) |
| **Foreign Key**     | ❌ 없음              | 관계 제약 조건 없음                                               |
| **Auto Increment**  | ❌ 없음              | 자동 증가 ID 없음, 직접 UUID 또는 타임스탬프 사용                          |

---

### ✅ 요약

| 질문                            | 답변                                                     |
| ----------------------------- | ------------------------------------------------------ |
| Cassandra에서 SQL을 그대로 쓸 수 있나요? | ❌ 완전히는 불가능. SQL과 비슷한 **CQL**을 사용하지만 제한 있음              |
| 어떤 쿼리는 되나요?                   | `SELECT`, `INSERT`, `UPDATE`, `DELETE` 등 기본 DML은 가능    |
| 어떤 쿼리는 안 되나요?                 | `JOIN`, `GROUP BY`, `서브쿼리`, `트랜잭션`, `Foreign Key` 등은 ❌ |

---

#### 💡 Cassandra는 설계 자체가 **"조인을 피하고" 쓰기 성능을 극대화**하는 방향입니다.

→ 그래서 **스키마 설계 시 읽기 패턴을 기준으로 테이블을 만들어야** 합니다.


---

## 5. Cassandra Write Path vs RDBMS

Cassandra와 RDBMS(PostgreSQL 등)는 \*\*쓰기 동작 방식(write path)\*\*이 크게 다릅니다.
Cassandra는 **append-only 모델**이고, RDBMS는 **seek-and-modify 모델**입니다.

---

### ✅ Cassandra Write Path (Append-only)

1. **Write to Commit Log (Disk)**

   * 장애 복구를 위해 디스크에 먼저 기록합니다.
2. **Write to Memtable (Memory)**

   * 메모리에 임시로 데이터를 저장합니다.
3. **Acknowledge the write to client**

   * 이 시점에서 클라이언트는 성공 응답을 받습니다.
4. **Flush to SSTable (Disk) periodically**

   * 메모리가 꽉 차거나 주기적으로 디스크에 flush됩니다.
5. **No overwrite, just append**

   * 항상 새로 추가(append)하는 방식. 기존 데이터를 덮어쓰지 않음.

**📌 특징:**

* 디스크에 **순차적으로 쓰기** 때문에 빠름
* 데이터를 **찾거나 수정하지 않고**, **새로 추가만 함**

---

### ✅ RDBMS (e.g., PostgreSQL) Write Path

1. **Write to WAL (Write-Ahead Log, Disk)**

   * 먼저 로그를 기록하여 복구 가능하게 함
2. **Immediately update the actual DB file (Disk)**

   * 실제 테이블 파일의 **정확한 위치를 찾아서 수정**함
3. **Acknowledge the write to client**

**📌 특징:**

* **랜덤 디스크 접근** 필요 (어디를 수정할지 찾아야 함)
* 데이터 무결성과 **ACID 트랜잭션** 보장을 위해 설계됨
* 상대적으로 느릴 수 있음

---

### ✅ 요약 비교

| 항목     | Cassandra (NoSQL)      | RDBMS (e.g., PostgreSQL) |
| ------ | ---------------------- | ------------------------ |
| 쓰기 구조  | Append-only            | Seek & Modify            |
| 디스크 접근 | 순차적 (빠름)               | 랜덤 접근 (느릴 수 있음)          |
| 트랜잭션   | 제한적 (Lightweight only) | 완전한 ACID 트랜잭션 지원         |
| 쓰기 성능  | 매우 빠름                  | 상대적으로 느림 (정합성 중심 설계)     |
| 주된 목적  | 고속 쓰기, 분산 처리           | 정합성, 관계형 무결성             |
### **MongoDB CLI (`mongosh`) 상세 정리**

`mongosh`는 **MongoDB의 최신 CLI(Command Line Interface)**로, 데이터베이스와 직접 상호작용할 수 있는 도구입니다. 이를 사용해 데이터베이스 관리, 쿼리 실행, 데이터 조작 등을 수행할 수 있습니다.

---

### **1. `mongosh` 설치 및 실행**
#### **설치**
1. **MongoDB Shell 다운로드**:  
   - [공식 다운로드 링크](https://www.mongodb.com/try/download/shell)에서 운영 체제에 맞는 버전을 다운로드합니다.
   - 다운로드한 파일의 압축을 해제하고 `mongosh.exe`를 MongoDB 설치 폴더 (`C:\Program Files\MongoDB\Server\8.0\bin`)에 복사합니다.

2. **환경 변수 설정**:
   - `mongosh`를 어디서든 실행하려면 `mongosh.exe` 경로를 시스템 환경 변수(`Path`)에 추가합니다.
   - 예: `C:\Program Files\MongoDB\Server\8.0\bin`

#### **실행**
MongoDB 서버가 실행된 상태에서 `mongosh`를 입력하면 연결됩니다:
```bash
mongosh
```

---

### **2. 주요 명령어**
#### **1) 데이터베이스 명령어**
| 명령어                       | 설명                                      |
|-----------------------------|-----------------------------------------|
| `show dbs`                  | 모든 데이터베이스 목록 조회                 |
| `use <database>`            | 특정 데이터베이스로 전환 (존재하지 않으면 생성) |
| `db`                        | 현재 사용 중인 데이터베이스 확인             |
| `db.dropDatabase()`         | 현재 데이터베이스 삭제                     |

#### **2) 컬렉션 명령어**
| 명령어                       | 설명                                      |
|-----------------------------|-----------------------------------------|
| `show collections`          | 현재 데이터베이스의 모든 컬렉션(테이블) 조회    |
| `db.createCollection("<name>")` | 새로운 컬렉션 생성                        |
| `db.<collection>.drop()`    | 특정 컬렉션 삭제                          |

#### **3) CRUD 명령어**
| 명령어                                     | 설명                                         |
|------------------------------------------|--------------------------------------------|
| `db.<collection>.insertOne({})`          | 하나의 문서 삽입                             |
| `db.<collection>.insertMany([{}, {}])`   | 여러 문서 삽입                               |
| `db.<collection>.find()`                 | 컬렉션 내 모든 문서 조회                     |
| `db.<collection>.findOne({조건})`         | 조건에 맞는 첫 번째 문서 조회                 |
| `db.<collection>.updateOne({조건}, {수정})` | 조건에 맞는 한 문서를 수정                   |
| `db.<collection>.updateMany({조건}, {수정})`| 조건에 맞는 모든 문서를 수정                 |
| `db.<collection>.deleteOne({조건})`      | 조건에 맞는 한 문서를 삭제                   |
| `db.<collection>.deleteMany({조건})`     | 조건에 맞는 모든 문서를 삭제                 |

---

### **3. MongoDB CLI 활용 예시**
#### **1) 데이터베이스 및 컬렉션 생성**
```bash
> mongosh
test> use mydatabase
switched to db mydatabase

test> db.createCollection("users")
{ "ok": 1 }

test> show collections
users
```

#### **2) 데이터 삽입 및 조회**
```bash
test> db.users.insertOne({ name: "Alice", age: 25 })
{ "acknowledged": true, "insertedId": ObjectId("...") }

test> db.users.find()
[
  { "_id": ObjectId("..."), "name": "Alice", "age": 25 }
]
```

#### **3) 데이터 수정 및 삭제**
```bash
test> db.users.updateOne({ name: "Alice" }, { $set: { age: 26 } })
{ "matchedCount": 1, "modifiedCount": 1 }

test> db.users.deleteOne({ name: "Alice" })
{ "deletedCount": 1 }
```
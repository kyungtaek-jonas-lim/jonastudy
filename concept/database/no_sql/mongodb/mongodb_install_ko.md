## **1. MongoDB 로컬 설치 방법 (간단한 설명)**  
1. **[MongoDB 공식 웹사이트](https://www.mongodb.com/try/download/community)**에서 운영체제에 맞는 MongoDB Community Edition을 다운로드합니다.  
2. 설치 후, MongoDB를 실행하기 위해 터미널에서 `mongod` 명령어를 실행합니다.  
3. 기본적으로 MongoDB는 `localhost:27017`에서 실행됩니다.  

---

## **2. MongoDB CLI: MongoDB Shell (`mongosh`)에 대한 정리**

`mongosh`는 **MongoDB의 최신 CLI (Command-Line Interface)**로, MongoDB 데이터베이스와 상호작용할 수 있는 강력한 도구입니다. 이전 버전의 `mongo.exe`를 대체하며, MongoDB 5.0 이상에서 사용됩니다.

---

### **1. `mongosh`란?**
- MongoDB의 공식 셸로, MongoDB 서버와 통신하며 **데이터베이스 관리, 쿼리 실행, 데이터 조작**을 할 수 있습니다.
- 최신 Node.js 기반으로 만들어졌으며, 이전 CLI(`mongo.exe`)보다 **유연성과 성능**이 향상되었습니다.
- MongoDB의 최신 기능(예: 트랜잭션, 셰이딩 등)과 완벽히 호환됩니다.

---

### **2. `mongosh` 주요 특징**
1. **JSON 기반 입력/출력**:
   - 데이터는 JSON 형식으로 표시되며, 결과를 직관적으로 확인할 수 있습니다.

2. **모던 자바스크립트 지원**:
   - 최신 ECMAScript 표준을 지원하여, 셸에서 복잡한 스크립트 작성 가능.

3. **MongoDB 최신 기능 지원**:
   - 트랜잭션, 애그리게이션, 셰이딩 등 최신 기능을 완벽히 지원.

4. **완벽한 대화형 환경**:
   - 명령어 실행 결과가 포맷팅되어 보기 쉽게 출력.

5. **오픈 소스**:
   - [GitHub에서 공개](https://github.com/mongodb-js/mongosh)된 소스코드.

---

### **3. `mongosh` 설치 및 실행**
#### **1) MongoDB 설치 시 기본 포함 여부 확인**
MongoDB 5.0 이상을 설치했다면 `mongosh`가 기본적으로 설치되었을 가능성이 큽니다.
- 설치된 경로에서 `mongosh.exe` 파일을 확인:
  ```
  C:\Program Files\MongoDB\Server\<버전>\bin
  ```

#### **2) `mongosh`가 없을 경우 설치**
`mongosh`가 없다면 **MongoDB Shell 다운로드 페이지**에서 설치하세요:
- **[mongosh 다운로드 링크](https://www.mongodb.com/try/download/shell)**
  1. 운영 체제를 선택 (Windows, macOS, Linux).
  2. ZIP 파일을 다운로드 후 압축 해제.
  3. `mongosh.exe`를 MongoDB `bin` 디렉터리(`C:\Program Files\MongoDB\Server\8.0\bin`)에 복사.

#### **3) 환경 변수에 추가**
1. **`mongosh.exe` 경로를 환경 변수에 추가**:
   - 경로: `C:\Program Files\MongoDB\Server\8.0\bin`
2. 환경 변수 추가 후, CMD를 다시 열고 실행:
   ```bash
   mongosh
   ```

#### **4) 실행**
MongoDB 서버가 실행된 상태에서 `mongosh`를 입력하면 데이터베이스와 연결됩니다.
```bash
mongosh
```

---

### **4. 주요 명령어**
| 명령어                          | 설명                                 |
|--------------------------------|------------------------------------|
| `show dbs`                     | 모든 데이터베이스 목록 보기             |
| `use <database>`               | 데이터베이스 생성 또는 선택              |
| `show collections`             | 현재 데이터베이스의 모든 컬렉션(테이블) 보기 |
| `db.<collection>.find()`       | 특정 컬렉션의 모든 데이터 조회           |
| `db.<collection>.insertOne({})` | 데이터 추가 (단일 문서)                |
| `db.<collection>.updateOne()`   | 데이터 수정                           |
| `db.<collection>.deleteOne()`   | 데이터 삭제                           |
| `exit`                         | MongoDB 셸 종료                      |

---

### **5. 실행 중 자주 발생하는 문제**
1. **`mongosh` 명령어 인식 불가**:
   - 해결: `mongosh.exe` 경로를 환경 변수에 추가.
2. **MongoDB 서버가 실행되지 않음**:
   - 해결: `mongod` 명령어로 서버 실행.
   ```bash
   mongod --dbpath="C:\data\db"
   ```

---

### **6. MongoDB Shell 사용 예시**
#### **1) 데이터베이스 작업**
```bash
> mongosh
test> show dbs
admin  config  local
test> use mydatabase
switched to db mydatabase
test> db.createCollection("users")
{ "ok": 1 }
```

#### **2) CRUD 작업**
```bash
test> db.users.insertOne({ name: "Alice", age: 25 })
{ "acknowledged": true, "insertedId": ObjectId("...") }

test> db.users.find()
[
  { "_id": ObjectId("..."), "name": "Alice", "age": 25 }
]
```
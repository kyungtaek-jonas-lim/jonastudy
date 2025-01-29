### **1. MongoDBClient vs Mongoose: 어떤 것을 더 많이 사용하나요?**
Node.js에서 MongoDB를 사용할 때 **MongoDBClient**(MongoDB 기본 드라이버)와 **Mongoose**(ODM 라이브러리) 중 하나를 선택할 수 있습니다. 일반적으로 **Mongoose를 더 많이 사용**하지만, 상황에 따라 두 도구의 선택은 다를 수 있습니다.

---

### ✅ **MongoDBClient vs Mongoose 비교**
| 특징                  | **MongoDBClient** (기본 드라이버)   | **Mongoose** (ODM 라이브러리)     |
|----------------------|----------------------------------|---------------------------------|
| **사용 방식**         | MongoDB와 직접 통신 (`findOne`)      | ODM(Object-Document Mapping) 라이브러리 |
| **데이터 모델링**      | JSON 객체를 직접 사용               | Schema(스키마)를 정의하고 데이터 관리 |
| **유효성 검사**        | 없음                               | 내장된 스키마 기반 유효성 검사 지원 |
| **관계형 데이터 처리**   | `$lookup` 등 MongoDB의 기본 기능 사용 | Populate 기능으로 관계형 데이터 처리 |
| **성능**              | 직접 제어 가능 (빠르고 가벼움)        | ODM 사용으로 약간의 오버헤드 존재 |
| **러닝 커브**          | 쉬움 (MongoDB 기본 명령어 활용)       | 스키마 설계 및 추가 설정 필요 |
| **트랜잭션 지원**       | 지원                               | MongoDBClient를 내부적으로 사용하여 지원 |
| **사용 사례**          | 간단한 작업, 성능이 중요한 경우       | CRUD API, 정형화된 데이터 처리 |

✅ **MongoDBClient 사용 장점**
- **가볍고 빠름**: 성능에 민감한 애플리케이션에 적합.
- **유연성**: MongoDB의 모든 기능을 직접 제어 가능.

✅ **Mongoose 사용 장점**
- **스키마 기반 데이터 관리**: 데이터의 일관성을 유지 가능.
- **내장 유효성 검사** 및 **미들웨어 지원**: 데이터 처리 로직을 단순화.

---

### **2. MongoDB 로컬 설치 방법 (간단한 설명)**  
1. **[MongoDB 공식 웹사이트](https://www.mongodb.com/try/download/community)**에서 운영체제에 맞는 MongoDB Community Edition을 다운로드합니다.  
2. 설치 후, MongoDB를 실행하기 위해 터미널에서 `mongod` 명령어를 실행합니다.  
3. 기본적으로 MongoDB는 `localhost:27017`에서 실행됩니다.  

---

### **3. MongoDBClient를 활용한 MongoDB 연결 및 CRUD 예제**

#### **1. 프로젝트 초기 설정**
```bash
mkdir mongodb-client-app
cd mongodb-client-app
npm init -y
npm install typescript ts-node-dev @types/node mongodb dotenv
npx tsc --init
```

#### **2. MongoDB 연결 코드 (`src/app.ts`)**
```typescript
import { MongoClient } from "mongodb";
import dotenv from "dotenv";

dotenv.config();

const uri = process.env.MONGO_URI || "mongodb://localhost:27017";
const client = new MongoClient(uri);

async function run() {
  try {
    // MongoDB 연결
    await client.connect();
    console.log("✅ MongoDB에 연결되었습니다.");

    const db = client.db("testdb");
    const collection = db.collection("users");

    // 데이터 삽입
    const insertResult = await collection.insertOne({ name: "John", age: 30 });
    console.log("📌 삽입된 데이터 ID:", insertResult.insertedId);

    // 데이터 조회
    const user = await collection.findOne({ name: "John" });
    console.log("📌 조회된 데이터:", user);

    // 데이터 수정
    const updateResult = await collection.updateOne(
      { name: "John" },
      { $set: { age: 31 } }
    );
    console.log("📌 수정된 데이터 개수:", updateResult.modifiedCount);

    // 데이터 삭제
    const deleteResult = await collection.deleteOne({ name: "John" });
    console.log("📌 삭제된 데이터 개수:", deleteResult.deletedCount);
  } catch (error) {
    console.error("❌ MongoDB 처리 중 오류 발생:", error);
  } finally {
    await client.close();
    console.log("✅ MongoDB 연결이 종료되었습니다.");
  }
}

run().catch(console.dir);
```

---

#### **3. 실행**
```bash
npx ts-node-dev src/app.ts
```

---

### **4. Mongoose를 활용한 MongoDB 연결 및 CRUD 예제** ([참고](https://github.com/kyungtaek-jonas-lim/jonas-api-master/blob/main/src/services/ItemService.ts))

#### **1. 프로젝트 초기 설정**
```bash
mkdir mongodb-mongoose-app
cd mongodb-mongoose-app
npm init -y
npm install typescript ts-node-dev @types/node mongoose dotenv
npx tsc --init
```

#### **2. MongoDB 연결 코드 (`src/database.ts`)**
```typescript
import mongoose from "mongoose";
import dotenv from "dotenv";

dotenv.config();

const MONGO_URI = process.env.MONGO_URI || "mongodb://localhost:27017/testdb";

export async function connectToDatabase() {
  try {
    await mongoose.connect(MONGO_URI, {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    });
    console.log("✅ Mongoose를 통해 MongoDB에 연결되었습니다!");
  } catch (error) {
    console.error("❌ MongoDB 연결 실패:", error);
    process.exit(1);
  }
}
```

#### **3. MongoDB 모델 정의 (`src/models/User.ts`)**
```typescript
import mongoose, { Schema, Document } from "mongoose";

export interface IUser extends Document {
  name: string;
  age: number;
}

const UserSchema: Schema = new Schema({
  name: { type: String, required: true },
  age: { type: Number, required: true },
});

export const UserModel = mongoose.model<IUser>("User", UserSchema);
```

#### **4. CRUD 연동 코드 (`src/app.ts`)**
```typescript
import express from "express";
import { connectToDatabase } from "./database";
import { UserModel } from "./models/User";

const app = express();
app.use(express.json());

app.post("/users", async (req, res) => {
  try {
    const newUser = new UserModel(req.body);
    const savedUser = await newUser.save();
    res.status(201).json(savedUser);
  } catch (error) {
    res.status(500).json({ error: "사용자 생성 실패" });
  }
});

app.get("/users", async (_, res) => {
  try {
    const users = await UserModel.find();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: "사용자 조회 실패" });
  }
});

app.listen(3000, async () => {
  await connectToDatabase();
  console.log("🚀 서버가 http://localhost:3000에서 실행 중입니다.");
});
```

---

#### **5. 실행**
```bash
npx ts-node-dev src/app.ts
```
### **ODM과 ORM의 차이**
✅ **ORM (Object-Relational Mapping)**
- ORM은 **객체와 관계형 데이터베이스(RDBMS)**를 매핑하는 기술입니다.
- SQL을 직접 작성하지 않고도 객체 지향적으로 데이터를 조작할 수 있습니다.

📌 **ORM 사용 예시 (MySQL + TypeORM)**
```typescript
import { Entity, PrimaryGeneratedColumn, Column } from "typeorm";

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;
}
```
```typescript
import { getRepository } from "typeorm";
import { User } from "./User";

async function createUser() {
  const userRepository = getRepository(User);
  const newUser = userRepository.create({ name: "John Doe" });
  await userRepository.save(newUser);
}
```
- **TypeORM**을 사용하여 `User` 테이블을 자동으로 생성하고, 객체를 SQL 없이 저장할 수 있습니다.

✅ **ODM (Object-Document Mapping)**
- ODM은 **객체와 NoSQL(Document) 데이터베이스(MongoDB)**를 매핑하는 기술입니다.
- NoSQL은 관계형 데이터베이스처럼 고정된 스키마가 없고, JSON 문서 기반으로 데이터를 저장합니다.

📌 **ODM 사용 예시 (MongoDB + Mongoose)**
```typescript
import mongoose, { Schema, Document } from "mongoose";

interface IUser extends Document {
  name: string;
}

const UserSchema = new Schema({
  name: { type: String, required: true },
});

export const UserModel = mongoose.model<IUser>("User", UserSchema);
```
```typescript
import { UserModel } from "./User";

async function createUser() {
  const newUser = new UserModel({ name: "John Doe" });
  await newUser.save();
}
```
- **Mongoose**를 사용하여 MongoDB의 JSON 문서를 객체처럼 다룰 수 있습니다.

### 🚀 **ORM vs ODM 비교**
| 구분       | ORM (TypeORM, Sequelize) | ODM (Mongoose) |
|------------|--------------------------|----------------|
| 대상 DB   | 관계형 데이터베이스 (MySQL, PostgreSQL) | NoSQL (MongoDB) |
| 데이터 구조 | 테이블 (정형 데이터) | JSON 문서 (비정형 데이터) |
| 쿼리 방식 | SQL 기반 | JSON 기반 쿼리 |
| 스키마 변경 | 테이블 구조 변경 필요 | 유동적인 필드 변경 가능 |
| 관계 설정 | `JOIN` 및 외래 키 사용 | 내장 문서(Embedded Document) 또는 참조(Reference) |
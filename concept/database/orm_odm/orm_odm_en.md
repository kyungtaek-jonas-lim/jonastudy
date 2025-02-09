### **Differences between ODM & ORM**
✅ **ORM (Object-Relational Mapping)**
- ORM is a technique that maps **objects to relational databases (RDBMS)**.
- It allows us to work with database records as objects, without writing SQL.

📌 **Example of ORM usage (MySQL + TypeORM)**
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
- **TypeORM** allows us to define entities and work with SQL databases without writing raw SQL queries.

✅ **ODM (Object-Document Mapping)**
- ODM is a technique that maps **objects to NoSQL document databases (MongoDB)**.
- Unlike relational databases, NoSQL databases store data in **JSON-like documents**.

📌 **Example of ODM usage (MongoDB + Mongoose)**
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
- **Mongoose** allows us to model MongoDB documents as JavaScript objects.

### 🚀 **ORM vs ODM Comparison**
| Feature  | ORM (TypeORM, Sequelize) | ODM (Mongoose) |
|----------|--------------------------|----------------|
| Database Type | Relational (MySQL, PostgreSQL) | NoSQL (MongoDB) |
| Data Structure | Tables (Structured Data) | JSON Documents (Unstructured Data) |
| Query Language | SQL-based | JSON-based Queries |
| Schema Changes | Requires table alteration | Flexible schema |
| Relationships | Uses `JOIN` and foreign keys | Uses embedded documents or references |
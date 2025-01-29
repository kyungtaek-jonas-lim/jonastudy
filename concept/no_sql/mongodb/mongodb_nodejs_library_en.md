### **1. MongoDBClient vs Mongoose: Which is used more often?**
When connecting Node.js to MongoDB, you can choose between **MongoDBClient** (official MongoDB driver) and **Mongoose** (ODM library). Generally, **Mongoose** is preferred for most use cases, but each has its pros and cons.

---

### ✅ **Comparison: MongoDBClient vs Mongoose**
| Feature               | **MongoDBClient** (Official Driver) | **Mongoose** (ODM Library)         |
|-----------------------|--------------------------------------|------------------------------------|
| **Usage**             | Directly interacts with MongoDB API | ODM (Object-Document Mapping)     |
| **Data Modeling**     | Uses raw JSON objects (`findOne`)   | Schema-based (with validation)    |
| **Validation**        | None                               | Built-in validation in schemas    |
| **Relationships**     | Manual operations (`$lookup`)       | Populate simplifies relationships |
| **Performance**       | Lightweight (direct control)        | Slight overhead due to ODM        |
| **Learning Curve**    | Easier (uses MongoDB queries)       | Steeper (requires schema knowledge)|
| **Transactions**      | Supported (MongoDB 4.0+)           | Supported via MongoDB transactions|
| **Use Case**          | Lightweight services, high performance | CRUD APIs, structured data        |

✅ **When to use MongoDBClient?**
- When you need **lightweight and fast performance**.
- When you want **fine-grained control** over queries.

✅ **When to use Mongoose?**
- When **schema-based data modeling** is required.
- When you want built-in validation and simplified relationship handling.

---

### **2. MongoDB Local Installation (Quick Guide)**
1. Download the MongoDB Community Edition from the **[official MongoDB website](https://www.mongodb.com/try/download/community)** for your OS.  
2. Use the terminal to start MongoDB with the `mongod` command.  
3. MongoDB will run at `localhost:27017` by default.  

---

### **3. Example using MongoDBClient**

#### **1. Project Setup**
```bash
mkdir mongodb-client-app
cd mongodb-client-app
npm init -y
npm install typescript ts-node-dev @types/node mongodb dotenv
npx tsc --init
```

#### **2. MongoDB Connection Code (`src/app.ts`)**
```typescript
import { MongoClient } from "mongodb";
import dotenv from "dotenv";

dotenv.config();

const uri = process.env.MONGO_URI || "mongodb://localhost:27017";
const client = new MongoClient(uri);

async function run() {
  try {
    await client.connect();
    console.log("✅ Connected to MongoDB!");

    const db = client.db("testdb");
    const collection = db.collection("users");

    // Insert data
    const insertResult = await collection.insertOne({ name: "John", age: 30 });
    console.log("📌 Inserted ID:", insertResult.insertedId);

    // Find data
    const user = await collection.findOne({ name: "John" });
    console.log("📌 Retrieved User:", user);

    // Update data
    const updateResult = await collection.updateOne(
      { name: "John" },
      { $set: { age: 31 } }
    );
    console.log("📌 Modified Count:", updateResult.modifiedCount);

    // Delete data
    const deleteResult = await collection.deleteOne({ name: "John" });
    console.log("📌 Deleted Count:", deleteResult.deletedCount);
  } catch (error) {
    console.error("❌ Error:", error);
  } finally {
    await client.close();
    console.log("✅ Connection closed.");
  }
}

run().catch(console.dir);
```

---

#### **3. Run**
```bash
npx ts-node-dev src/app.ts
```

---

### **4. Example using Mongoose** ([reference](https://github.com/kyungtaek-jonas-lim/jonas-api-master/blob/main/src/services/ItemService.ts))

#### **1. Project Setup**
```bash
mkdir mongodb-mongoose-app
cd mongodb-mongoose-app
npm init -y
npm install typescript ts-node-dev @types/node mongoose dotenv
npx tsc --init
```

#### **2. MongoDB Connection Code (`src/database.ts`)**
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
    console.log("✅ Connected to MongoDB using Mongoose!");
  } catch (error) {
    console.error("❌ MongoDB connection failed:", error);
    process.exit(1);
  }
}
```

#### **3. MongoDB Model (`src/models/User.ts`)**
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

#### **4. CRUD Operations (`src/app.ts`)**
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
    res.status(500).json({ error: "Failed to create user" });
  }
});

app.get("/users", async (_, res) => {
  try {
    const users = await UserModel.find();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: "Failed to fetch users" });


  }
});

app.listen(3000, async () => {
  await connectToDatabase();
  console.log("🚀 Server running at http://localhost:3000");
});
```

---

#### **5. Run**
```bash
npx ts-node-dev src/app.ts
```
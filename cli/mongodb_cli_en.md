### **Detailed Overview of MongoDB CLI (`mongosh`)**

`mongosh` is the **latest Command Line Interface (CLI)** for MongoDB, allowing users to interact directly with databases. It provides tools for database management, executing queries, and manipulating data.

---

### **1. Installing and Running `mongosh`**
#### **Installation**
1. **Download MongoDB Shell**:
   - Download the appropriate version for your OS from the [official download page](https://www.mongodb.com/try/download/shell).
   - Extract the ZIP file and copy `mongosh.exe` to your MongoDB installation folder (e.g., `C:\Program Files\MongoDB\Server\8.0\bin`).

2. **Set Environment Variables**:
   - Add the path to `mongosh.exe` to the system environment variables (`Path`).
   - Example: `C:\Program Files\MongoDB\Server\8.0\bin`.

#### **Execution**
After starting the MongoDB server, connect using:
```bash
mongosh
```

---

### **2. Key Commands**
#### **1) Database Commands**
| Command                     | Description                                |
|-----------------------------|--------------------------------------------|
| `show dbs`                  | Lists all databases                       |
| `use <database>`            | Switches to a database (creates if it doesn't exist) |
| `db`                        | Displays the currently selected database  |
| `db.dropDatabase()`         | Deletes the currently selected database   |

#### **2) Collection Commands**
| Command                     | Description                                |
|-----------------------------|--------------------------------------------|
| `show collections`          | Lists all collections in the current database |
| `db.createCollection("<name>")` | Creates a new collection                  |
| `db.<collection>.drop()`    | Deletes a specific collection              |

#### **3) CRUD Commands**
| Command                                   | Description                                 |
|------------------------------------------|--------------------------------------------|
| `db.<collection>.insertOne({})`          | Inserts a single document                  |
| `db.<collection>.insertMany([{}, {}])`   | Inserts multiple documents                 |
| `db.<collection>.find()`                 | Retrieves all documents in the collection  |
| `db.<collection>.findOne({criteria})`    | Retrieves the first document matching criteria |
| `db.<collection>.updateOne({criteria}, {update})` | Updates a single document                 |
| `db.<collection>.updateMany({criteria}, {update})` | Updates multiple documents               |
| `db.<collection>.deleteOne({criteria})`  | Deletes a single document                  |
| `db.<collection>.deleteMany({criteria})` | Deletes multiple documents                 |

---

### **3. MongoDB CLI Usage Examples**
#### **1) Creating Databases and Collections**
```bash
> mongosh
test> use mydatabase
switched to db mydatabase

test> db.createCollection("users")
{ "ok": 1 }

test> show collections
users
```

#### **2) Inserting and Querying Data**
```bash
test> db.users.insertOne({ name: "Alice", age: 25 })
{ "acknowledged": true, "insertedId": ObjectId("...") }

test> db.users.find()
[
  { "_id": ObjectId("..."), "name": "Alice", "age": 25 }
]
```

#### **3) Updating and Deleting Data**
```bash
test> db.users.updateOne({ name: "Alice" }, { $set: { age: 26 } })
{ "matchedCount": 1, "modifiedCount": 1 }

test> db.users.deleteOne({ name: "Alice" })
{ "deletedCount": 1 }
```
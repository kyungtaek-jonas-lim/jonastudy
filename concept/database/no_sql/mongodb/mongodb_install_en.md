## **1. MongoDB Local Installation (Quick Guide)**
1. Download the MongoDB Community Edition from the **[official MongoDB website](https://www.mongodb.com/try/download/community)** for your OS.  
2. Use the terminal to start MongoDB with the `mongod` command.  
3. MongoDB will run at `localhost:27017` by default.  

---

## **2. MongoDB CLI: MongoDB Shell (`mongosh`) Overview**

`mongosh` is the **official MongoDB command-line interface (CLI)**, designed to interact with MongoDB databases. It replaces the legacy `mongo.exe` and offers enhanced functionality with MongoDB 5.0 and later versions.

---

### **1. What is `mongosh`?**
- `mongosh` is MongoDB's **modern shell** for interacting with databases.
- Built on **Node.js**, it offers better compatibility with modern JavaScript and MongoDB features.
- It supports all the latest MongoDB capabilities, such as **transactions**, **aggregation**, and **sharding**.

---

### **2. Key Features of `mongosh`**
1. **JSON-Based Input/Output**:
   - Displays data in a readable JSON format.

2. **Modern JavaScript Support**:
   - Enables writing scripts with the latest ECMAScript standards.

3. **Full MongoDB Feature Compatibility**:
   - Supports advanced features like transactions and sharding.

4. **Interactive Experience**:
   - Provides formatted output for better readability.

5. **Open Source**:
   - The source code is available on [GitHub](https://github.com/mongodb-js/mongosh).

---

### **3. Installing and Running `mongosh`**
#### **1) Check If `mongosh` Is Installed**
If you have installed MongoDB 5.0 or later, `mongosh` should already be included:
- Look for `mongosh.exe` in the installation path:
  ```
  C:\Program Files\MongoDB\Server\<version>\bin
  ```

#### **2) Download `mongosh`**
If `mongosh` is missing, download it from the **[official MongoDB Shell page](https://www.mongodb.com/try/download/shell)**:
1. Choose your operating system (Windows, macOS, Linux).
2. Download the ZIP file, extract it, and copy `mongosh.exe` to the MongoDB `bin` folder:
   ```
   C:\Program Files\MongoDB\Server\8.0\bin
   ```

#### **3) Add to Environment Variables**
1. Add `mongosh.exe` path to the system environment variables:
   - Path: `C:\Program Files\MongoDB\Server\8.0\bin`
2. Restart the terminal and run:
   ```bash
   mongosh
   ```

#### **4) Run `mongosh`**
To start interacting with MongoDB:
```bash
mongosh
```

---

### **4. Key Commands**
| Command                        | Description                                |
|--------------------------------|--------------------------------------------|
| `show dbs`                     | List all databases                        |
| `use <database>`               | Create or switch to a database            |
| `show collections`             | List all collections in the current database |
| `db.<collection>.find()`       | Retrieve all documents in a collection    |
| `db.<collection>.insertOne({})` | Add a document to a collection            |
| `db.<collection>.updateOne()`   | Update a document in a collection         |
| `db.<collection>.deleteOne()`   | Delete a document from a collection       |
| `exit`                         | Exit the MongoDB shell                    |

---

### **5. Common Issues**
1. **`mongosh` Not Recognized**:
   - Fix: Add the path to `mongosh.exe` in the system environment variables.
2. **MongoDB Server Not Running**:
   - Fix: Start the MongoDB server using `mongod`:
     ```bash
     mongod --dbpath="C:\data\db"
     ```

---

### **6. Example Usage**
#### **1) Database Operations**
```bash
> mongosh
test> show dbs
admin  config  local
test> use mydatabase
switched to db mydatabase
test> db.createCollection("users")
{ "ok": 1 }
```

#### **2) CRUD Operations**
```bash
test> db.users.insertOne({ name: "Alice", age: 25 })
{ "acknowledged": true, "insertedId": ObjectId("...") }

test> db.users.find()
[
  { "_id": ObjectId("..."), "name": "Alice", "age": 25 }
]
```
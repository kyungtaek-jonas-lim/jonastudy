
# Cassandra

## ✅ What is Cassandra?

**Apache Cassandra** is a **NoSQL distributed database** with the following characteristics:

* **Distributed**: Data is distributed across multiple servers (nodes).
* **Column-family model**: Similar to relational tables but with a flexible schema.
* **High write performance**: Optimized for fast, large-scale write operations.
* **Fault-tolerant**: Operates even when some nodes fail.
* **AP-oriented in CAP theorem**: Prioritizes **Availability** and **Partition Tolerance**.

---

## Index

1. [Cassandra & Memory](#1-cassandra--memory)
2. [Cassandra vs RDBMS](#2-cassandra-vs-rdbms)
3. [Cassandra vs Other NoSQL](#3-cassandra-vs-other-nosql)
4. [Cassandra CRUD: CQL (Cassandra Query Language)](#4-cassandra-crud-cql-cassandra-query-language)
5. [Cassandra Write Path vs RDBMS](#5-cassandra-write-path-vs-rdbms)

---

## 1. Cassandra & Memory

### ✅ Is Cassandra an in-memory database?

**No. Cassandra is fundamentally a disk-based database.**

* It stores data on disk.
* However, **write operations first go to memory**, and are later flushed to disk.

🔹 Main components:

| Component      | Description                                                |
| -------------- | ---------------------------------------------------------- |
| **Memtable**   | In-memory structure for temporarily holding write data     |
| **SSTable**    | On-disk data file where flushed data is stored permanently |
| **Commit log** | Write-ahead log stored on disk for crash recovery          |

→ Cassandra uses memory to **optimize write performance**, but **data is persisted to disk**.

---

### ✅ Comparison with in-memory DB

| Feature       | Cassandra (Disk-based)                           | Redis (In-memory DB)                       |
| ------------- | ------------------------------------------------ | ------------------------------------------ |
| Storage       | Disk-based with memory buffering                 | Memory-based (with optional persistence)   |
| Primary use   | Scalable distributed storage                     | Ultra-fast caching, real-time reads/writes |
| Typical usage | Log ingestion, sensor data, high-throughput apps | Session storage, leaderboard, caching      |

---

### ✅ When to use Cassandra

* When you need to handle **large-scale write-heavy workloads**
* When the system must stay available even during **node failures**
* Ideal for: **IoT data ingestion, log storage, time-series data, recommendation backends**

---

### 📌 Summary

| Question                 | Answer                                                                       |
| ------------------------ | ---------------------------------------------------------------------------- |
| Is Cassandra a database? | Yes, it's a NoSQL distributed database.                                      |
| Is it in-memory?         | No. It's disk-based, but uses memory for write buffering.                    |
| When is it useful?       | When you need scalable storage, high write throughput, and high availability |

---

## 2. Cassandra vs RDBMS

### ✅ Comparison Table

| Feature                 | RDBMS (e.g., MySQL, PostgreSQL)            | Cassandra                                                           |
| ----------------------- | ------------------------------------------ | ------------------------------------------------------------------- |
| **Data Model**          | Table-based (rows & columns), fixed schema | Column-family model, flexible schema                                |
| **Query Language**      | SQL (Structured Query Language)            | CQL (similar to SQL, but limited joins)                             |
| **Schema Changes**      | Strict, migration often needed             | Flexible, can add/remove columns easily                             |
| **Scalability**         | Vertical scaling (upgrade server specs)    | Horizontal scaling (add nodes easily)                               |
| **Consistency**         | Strong consistency (ACID compliance)       | Eventual consistency, prioritizes availability                      |
| **Fault Tolerance**     | Master-slave; failover is complex          | Masterless; survives partial node failure                           |
| **Write Performance**   | Moderate (due to transactions)             | Very fast (write-optimized)                                         |
| **Read Performance**    | Fast with indexes                          | Varies depending on data model and replication                      |
| **Use Cases**           | Structured data (banking, ERP, user auth)  | High-volume unstructured or semi-structured data (IoT, logs, feeds) |
| **Transaction Support** | Full ACID support                          | Limited (supports lightweight transactions only)                    |
| **Replication/Backup**  | Manual/master-slave                        | Built-in automatic replication, high availability                   |

---

### ✅ Quick Recommendation

| Use Case                                            | Recommended DB   |
| --------------------------------------------------- | ---------------- |
| Complex joins, structured data, strict transactions | 👉 **RDBMS**     |
| High write throughput, scalability, fault tolerance | 👉 **Cassandra** |

---

### 💡 Real-world Examples

* **RDBMS Examples**: Bank account management, order systems, user authentication
* **Cassandra Examples**:

  * News feed system like **Instagram**
  * Collecting data from **millions of sensors**
  * Storing **real-time logs**

---

## 3. Cassandra vs Other NoSQL

### ✅ Use Cases: Cassandra, Redis, MongoDB

| Database      | Key Features                                                        | Example Use Cases                                                                       | Companies/Projects Using It                                                              |
| ------------- | ------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Cassandra** | - Distributed NoSQL<br>- High write performance<br>- Fault-tolerant | - Log collection<br>- IoT sensor data<br>- News feed timeline<br>- Event stream storage | ▶ Netflix – viewing history<br>▶ Instagram – user feed<br>▶ Uber – real-time data        |
| **Redis**     | - In-memory DB<br>- Extremely fast<br>- Key-value based             | - Session storage<br>- Caching<br>- Leaderboards<br>- Pub/Sub messaging                 | ▶ Twitter – timeline cache<br>▶ GitHub – session management<br>▶ Tinder – matching queue |
| **MongoDB**   | - Document-based NoSQL<br>- Flexible schema<br>- JSON storage       | - CMS systems<br>- User profiles<br>- Product catalogs<br>- Blog/comments               | ▶ Facebook – messages/comments<br>▶ eBay – product catalog<br>▶ Forbes – content storage |

---

### ✅ Summary Table

| Scenario                                       | Best DB         |
| ---------------------------------------------- | --------------- |
| Write-heavy, fault-tolerant distributed system | ✅ **Cassandra** |
| Fast access to data, caching, real-time data   | ✅ **Redis**     |
| Storing flexible, document-like data           | ✅ **MongoDB**   |

---

### ✅ Common Real-world Combinations

* **Redis + MongoDB**
  → Cache product data from MongoDB in Redis for faster access

* **Cassandra + Kafka**
  → Stream real-time event data from Kafka and persist it to Cassandra


---

## 4. Cassandra CRUD: CQL (Cassandra Query Language)

**CRUD operations (Create, Read, Update, Delete)** in **Apache Cassandra** are performed using **CQL (Cassandra Query Language)**.
The syntax is similar to SQL, but there are **limitations**, such as no support for **JOINs or full transactions**.

---

### ✅ CRUD Examples in Cassandra

#### 1. **Create (Insert Data)**

```sql
INSERT INTO users (id, name, email) VALUES (1, 'Alice', 'alice@example.com');
```

* In Cassandra, `INSERT` acts as an **UPSERT**.
  → If the given `id` already exists, it behaves like an **UPDATE**.

---

#### 2. **Read (Select Data)**

```sql
SELECT * FROM users WHERE id = 1;
```

* **WHERE clauses must include a primary key or an indexed column.**
* Queries **without a partition key are not allowed**.

---

#### 3. **Update (Modify Data)**

```sql
UPDATE users SET email = 'new_email@example.com' WHERE id = 1;
```

* The `WHERE` clause **must include the primary key**.
* If the row does not exist, it will be created (UPSERT behavior).

---

#### 4. **Delete (Remove Data)**

```sql
DELETE FROM users WHERE id = 1;
```

* Deletes a single row.
* You can also delete specific columns:

```sql
DELETE email FROM users WHERE id = 1;
```

---

### ✅ Basic Table Definition Example

```sql
CREATE TABLE users (
  id int PRIMARY KEY,
  name text,
  email text
);
```

---

### ✅ Summary of CRUD Behavior

| Operation | Example  | Notes                                                    |
| --------- | -------- | -------------------------------------------------------- |
| Create    | `INSERT` | Behaves as UPSERT (insert or update)                     |
| Read      | `SELECT` | Requires a WHERE clause with primary key                 |
| Update    | `UPDATE` | Requires primary key; creates row if not exists (UPSERT) |
| Delete    | `DELETE` | Can delete specific columns or entire row                |

---

### ✅ SQL-like Features Available in CQL

CQL uses a syntax similar to SQL, making it relatively easy to learn.

| SQL Feature | Supported in CQL | Example                                             |
| ----------- | ---------------- | --------------------------------------------------- |
| `SELECT`    | ✅ Yes            | `SELECT * FROM users WHERE id = 1;`                 |
| `INSERT`    | ✅ Yes            | `INSERT INTO users (id, name) VALUES (1, 'Alice');` |
| `UPDATE`    | ✅ Yes            | `UPDATE users SET name = 'Bob' WHERE id = 1;`       |
| `DELETE`    | ✅ Yes            | `DELETE FROM users WHERE id = 1;`                   |
| `WHERE`     | ✅ Partially      | Only partition keys or indexed columns are allowed  |

---

### ❌ SQL Features **Not Supported** in Cassandra

| Feature            | Supported?     | Explanation                                                                  |
| ------------------ | -------------- | ---------------------------------------------------------------------------- |
| **JOIN**           | ❌ No           | Relational joins are not supported                                           |
| **GROUP BY**       | ❌ No / Limited | Aggregation support is minimal                                               |
| **HAVING**         | ❌ No           | Not supported for filtered aggregation                                       |
| **Subqueries**     | ❌ No           | Nested queries like `SELECT ... FROM (SELECT ...)` are not allowed           |
| **Transactions**   | ❌ No           | Full ACID transactions not supported (only lightweight transactions per row) |
| **Foreign Keys**   | ❌ No           | No relational constraints                                                    |
| **Auto Increment** | ❌ No           | No built-in auto-increment; UUIDs or timestamps must be used manually        |

---

### ✅ Summary

| Question                              | Answer                                                                     |
| ------------------------------------- | -------------------------------------------------------------------------- |
| Can you use SQL exactly in Cassandra? | ❌ Not entirely. CQL is SQL-like but with significant limitations.          |
| What SQL operations are allowed?      | Basic DML: `SELECT`, `INSERT`, `UPDATE`, `DELETE`                          |
| What SQL features are not supported?  | `JOIN`, `GROUP BY`, subqueries, transactions, foreign keys, auto increment |

---

#### 💡 Cassandra is designed to **avoid joins** and **optimize write performance**.

→ Therefore, **data modeling in Cassandra should be based on read/query patterns**, not traditional normalization.

---

## 5. Cassandra Write Path vs RDBMS

Cassandra and RDBMS (such as PostgreSQL) have very different **write paths**.
Cassandra follows an **append-only model**, while RDBMS follows a **seek-and-modify model**.

---

### ✅ Cassandra Write Path (Append-only)

1. **Write to Commit Log (Disk)**

   * The write is first recorded to disk for crash recovery.

2. **Write to Memtable (Memory)**

   * The data is then stored temporarily in memory.

3. **Acknowledge the write to the client**

   * At this point, the client receives a successful write acknowledgment.

4. **Flush to SSTable (Disk) periodically**

   * When the memtable is full or at scheduled intervals, data is flushed to disk.

5. **No overwrite, just append**

   * Data is always appended; existing records are never overwritten.

**📌 Characteristics:**

* Fast due to **sequential disk writes**.
* No random seek or modification; **new data is simply appended**.

---

### ✅ RDBMS (e.g., PostgreSQL) Write Path

1. **Write to WAL (Write-Ahead Log, Disk)**

   * First, the write is logged to ensure recoverability.

2. **Immediately update the actual DB file (Disk)**

   * The corresponding page in the database file is located and modified directly.

3. **Acknowledge the write to the client**

**📌 Characteristics:**

* Requires **random disk access** to locate and update the correct position.
* Designed for **data consistency and full ACID transactions**.
* Can be relatively slower due to overhead.

---

### ✅ Summary Comparison

| Feature      | Cassandra (NoSQL)                   | RDBMS (e.g., PostgreSQL)                  |
| ------------ | ----------------------------------- | ----------------------------------------- |
| Write Model  | Append-only                         | Seek & Modify                             |
| Disk Access  | Sequential (fast)                   | Random (can be slower)                    |
| Transactions | Limited (lightweight only)          | Full ACID support                         |
| Write Speed  | Very fast                           | Relatively slower (consistency-focused)   |
| Main Purpose | High-throughput, distributed writes | Data integrity and relational constraints |
# Elastic Search
- [Elastic Search](#elastic-search-1)
- [Elasticsearch vs RDBMS](#elasticsearch-vs-rdbms-comparison)
- [Additional Info](#additional-info)

&nbsp;

## Elastic Search

### 1. **Suitability of Elastic Search and No-SQL**
- **Aliases**
  - Distributed Search Engine
  - Text Search Engine
  - Real-Time Data Analytics Platform
  - NoSQL Database
  - Distributed Data Store

- **Suitability**
  - Elastic Search is primarily used as a **search engine**, but it is highly suitable for searching and analyzing document-based data.
  - It stores **document-based data** (data in JSON format) and processes search and analytics efficiently.
  - As a **NoSQL** system, it excels at handling unstructured data or dynamically changing schemas.
  - Therefore, when dealing with **document data**, **Elastic Search** is an excellent choice. It provides fast search performance as a distributed system suitable for handling unstructured data, unlike relational databases (RDBMS).

---

### 2. **Inserting Real-Time Data into Elastic Search**
- **Aliases**
  - Real-Time Data Search Engine
  - Data Indexing Service
  - Fast Search Updates

- **Data Insertion Methods**
  - The method to insert **real-time data into Elastic Search** typically involves using **CDC (Change Data Capture)** or **message queue systems**, although other methods can also be used.
  - For example, inserting data into **Elastic Search** when **DML** (INSERT, UPDATE, DELETE) occurs can be done by implementing **triggers** or **synchronization between the database and Elastic Search**. **Kafka**, a message queue, is widely used for this purpose.
  - However, excluding message queues, data can also be inserted into Elastic Search directly from application logic whenever a data change occurs. This method allows real-time data synchronization but may **add load to the system**.

---

### 3. **Real-Time Synchronization in ETL Pipelines**
- **Aliases**
  - Real-Time Data Synchronization
  - Data Pipeline
  - ETL (Extract, Transform, Load)

- **Real-Time Synchronization in ETL**
  - While ETL pipelines are typically used for **batch processing**, they can also handle **real-time synchronization**.
  - In Elastic Search, when **real-time data processing** is essential, data can be streamed in **real-time** through the **ETL pipeline**. Here, data is transmitted according to **immediate changes**, not in **periodic intervals**.
  - This method is useful for real-time analysis and monitoring.

---

### 4. **Handling Batch Jobs in Elastic Search**
- **Aliases**
  - Batch Data Processing
  - Large-Scale Data Indexing
  - Data Processing Tasks

- **Batch Processing Methods**
  - Elastic Search is fundamentally suited for **batch jobs**, but it does not **automatically execute batch tasks**.
  - Therefore, **separate logic** must be implemented for batch processing. For example, a system that **inserts data into Elastic Search in batches** at specific time intervals or uses **CRON jobs** to periodically insert data is needed.
  - Generally, logic must be implemented in services to **insert data into Elastic Search**.

---

### 5. **Full Text Index in Elastic Search**
- **Aliases**
  - Text Search Index
  - Fast Search Engine
  - Full Text Search

- **Full Text Index**
  - Elastic Search natively provides a **Full Text Index**.
  - Similar to the **Full Text Index** provided by **RDBMS**, it allows for **efficient search** on text data.
  - **Search performance** in Elastic Search is much faster and more efficient due to its use of **distributed systems** and **inverted indexing**.
  - It provides **fast response times** and **efficient text search**, especially for **large volumes of data**.

---

### 6. **Distributed Architecture in Elastic Search**
- **Aliases**
  - Distributed System
  - Data Sharding
  - Distributed Storage System

- **Distributed System**
  - Elastic Search uses a **distributed system** based on **sharding** and **replication**, not a **Master-Slave** architecture.
  - **Shards** divide the data into pieces and store them across **multiple nodes**, enabling **horizontal scaling** and providing high availability and load balancing.
  - **Data synchronization** occurs **automatically**, with **real-time synchronization** between **shards** and **replica shards**.
  - Unlike **RDBMS Read Replicas**, **Elastic Search distributes data across shards** and **replicates it**, offering high availability.

---

### 7. **Spell Correction and Search History**
- **Aliases**
  - Spell Correction
  - Similar Search
  - Text Processing

- **Spell Correction**
  - Elastic Search natively provides **automatic spell correction** for errors.
  - It offers **auto-completion** for **similar words** or **spelling variations**, allowing **flexible searches** even for **incomplete search terms**.
  - Spell tolerance can be set via **document mappings** and **query parameters**. For example, **Fuzzy Queries** can be used to find **similar words**.

---

### 8. **Response Format in Elastic Search**
- **Aliases**
  - Query Response Format
  - Search Results

- **Response Data Format**
  - Elastic Search returns query response data in **JSON format**.
  - This **JSON response** can be processed as needed and delivered to the client. **Server-side response formats** can be configured, and required data can be filtered or **sorted**.
  - For example, **using the `_source` field** to filter out original data or applying **aggregations** to obtain summary data.
  - The response format can **dynamically change**, and additional processing can be done in **backend logic** before delivering it to the client.

---

### Conclusion

Elasticsearch is a **distributed search engine** that is well-suited for handling **document-based data** and is highly efficient for **text searching** and **real-time data synchronization**. In comparison to **RDBMS**, it offers advantages in **high-speed search performance** and **distributed processing**, making it ideal for text-based search systems. It also supports **Full Text Indexing** and allows for **fuzzy search** to handle some degree of typo tolerance, which is useful for searching text. However, **batch processing** must be implemented manually, as Elasticsearch does not handle batch jobs natively.


&nbsp;
&nbsp;

## Elasticsearch vs RDBMS Comparison

### 1. **Data Structure**
   - **Elasticsearch**: 
     - Stores data based on **documents** (in JSON format)
     - Efficiently handles **unstructured data**
     - High **schema flexibility**, making it adaptable to changes in data structure
     - Data is stored using **inverted index**, optimized for text search
     
   - **RDBMS**:
     - Stores data based on **tables** (row and column structure)
     - Best suited for **structured data** and requires a **fixed schema**
     - Uses a relational data model to **normalize** data and define relationships through foreign keys
     - Performs data retrieval, insertion, and modification using **SQL**

### 2. **Search Performance**
   - **Elasticsearch**:
     - Optimized for **fast text search**, being a **distributed search engine**
     - Uses **inverted index** to quickly search through text data
     - Excellent at **real-time search** and offers fast performance with large data volumes
     - Supports **scale-out** (horizontal scaling), maintaining performance even with **large datasets**
     - Supports **fuzzy search** and **autocomplete** features

   - **RDBMS**:
     - Capable of highly **accurate searches** for **structured data**
     - Suitable for complex relational queries, such as **JOIN** operations, but less efficient for text-based searches
     - **Indexing** can improve performance, but generally requires **batch processing**
     - Performance can improve through **vertical scaling** (upgrading a single server), but **horizontal scaling** is often challenging

### 3. **Data Consistency**
   - **Elasticsearch**:
     - Uses **eventual consistency** (final consistency model)
     - Being a distributed system, **synchronization delays** may occur
     - **Write performance** is excellent, but it’s not suited for systems requiring **strict consistency**
     
   - **RDBMS**:
     - Guarantees **strong consistency** through **ACID** (Atomicity, Consistency, Isolation, Durability) properties
     - Ensures data consistency and integrity through transactions
     - Strong at managing **concurrency issues** in multi-user environments

### 4. **Scalability**
   - **Elasticsearch**:
     - Supports **horizontal scaling** via clustering, allowing distribution of data across multiple nodes
     - Distributes data processing through **sharding** and **replication**
     - Excellent performance with **large datasets** and **real-time search**
     
   - **RDBMS**:
     - Primarily uses **vertical scaling** by upgrading server performance
     - **Horizontal scaling** can be difficult, leading to performance degradation when handling **large datasets**
     - Some modern **distributed RDBMS** support horizontal scaling, but it involves higher complexity

### 5. **Data Analysis**
   - **Elasticsearch**:
     - Strong in **analytics** and **aggregation**
     - Well-suited for **real-time data analysis** and **large-scale log analysis**
     - Can quickly **aggregate** data and offer various visualization options
     - Integrated with **Elasticsearch Kibana** for **log analysis** and **monitoring**

   - **RDBMS**:
     - Well-suited for data analysis using **SQL queries**
     - Due to the structured nature of the data, **complex analyses** and **aggregations** require the use of **JOINs** or **subqueries**
     - **Performance degradation** can occur with large data volumes, and **batch processing** may be necessary

### 6. **Real-time Data Processing**
   - **Elasticsearch**:
     - Optimized for **real-time search**, with **instant reflection** of data changes
     - Strong for **log collection**, **real-time alerts**, and **data streaming**
     - **Search after data input** is immediately available

   - **RDBMS**:
     - Has limitations in **real-time processing**
     - Data is searchable only after **a certain delay** post-insertion
     - Guarantees **immediate consistency** in transaction processing but is not suited for real-time analysis

### 7. **Operations and Management**
   - **Elasticsearch**:
     - A **distributed system** that requires management of clusters and nodes
     - Maintenance can be complex, with proper **replication** and **sharding** configuration needed
     - Utilizing **managed services** (AWS, GCP, etc.) makes management easier
     
   - **RDBMS**:
     - Optimized for managing **structured data**, and is **easy to use and intuitive**
     - **SQL** makes data management straightforward
     - **Complex backup and recovery** tasks may need to be done manually

### 8. **Key Use Cases**
   - **Elasticsearch**:
     - **Log analysis** (log collection, real-time search)
     - **Search engines** (website, application search)
     - **Recommendation systems** (user behavior analysis)
     - **Monitoring and alerts** (real-time data monitoring)
     
   - **RDBMS**:
     - **Transaction management** (banking, financial systems)
     - **Structured data processing** (accounting systems, inventory management)
     - **Complex relational queries** (customer management systems)
     - **Permanent data storage** (user data storage, corporate databases)

### 9. **Elasticsearch vs RDBMS (Summary)**

| Aspect                        | Elasticsearch                                | RDBMS (Relational Database)                    |
|-------------------------------|----------------------------------------------|-----------------------------------------------|
| **Data Model**                 | Document-based (No-SQL style, JSON)          | Table and row-based (Relational model)        |
| **Search Features**            | Full-text search, fuzzy search, autocomplete | Full-text search (limited performance)        |
| **Performance**                | Very fast search for large datasets          | Performance degradation with large datasets   |
| **Batch Processing**           | ETL and periodic data updates needed         | Batch processing possible but inefficient     |
| **Distributed System**         | Distributed processing via sharding and replication | Read replicas for distribution (mostly read-only) |
| **Real-time Synchronization**  | Possible with CDC, triggers, etc.            | Real-time sync limited to transactional consistency |

---

### Conclusion

- **Elasticsearch** is suitable for systems that require **unstructured data** and **real-time search**. It supports **horizontal scalability** through its **distributed system** and is strong in processing **large-scale data**. It is also well-suited for **fast text search** and **log analysis**, among other use cases.

- **RDBMS** deals with **structured data**, guarantees **ACID transactions**, and is advantageous in handling **complex relational data** and ensuring **strong consistency**. While it may have limitations in processing large-scale data, it offers **precise data integrity** and powerful **query performance** through **SQL**.

Therefore, depending on the use case, one can appropriately choose between **Elasticsearch** and **RDBMS** or consider a hybrid architecture that utilizes both systems together.

&nbsp;
&nbsp;

---

## Additional Info
### 1. **Relationship Between Elasticsearch and No-SQL**
   - Elasticsearch is a **document-based search engine**, and it is **optimized for search**. It shares some characteristics with **No-SQL databases**, but its primary focus is on **search optimization**. Data is stored in **JSON format documents**, and the data model is flexible or can be adjusted, which shares some No-SQL characteristics. However, Elasticsearch is more specialized for **searching** compared to general No-SQL databases, which may focus on features like **Key-Value storage, scalability**, and more. Elasticsearch is focused on **search optimization**, which allows it to rapidly search large datasets, and its key features include **indexing and search optimization**, which differentiate it from other No-SQL databases.

### 2. **Inserting Data into Elasticsearch When Data Changes in RDBMS (Excluding CDC and MQ)**
   - **Common Method**: When data changes in RDBMS (INSERT, UPDATE, DELETE), it's common to update Elasticsearch directly using **asynchronous processing**. 
   - **Without using message queues** like Kafka, it is possible to update Elasticsearch in real-time through **triggers** or **application logic** in RDBMS. For instance, data changes in the **application logic** can trigger insert or update operations in Elasticsearch.
   - **Using Triggers**: You can set triggers in RDBMS to send data to Elasticsearch in real time when data changes. However, this method may lead to **performance degradation** when there is **high traffic**, so it should be used cautiously.

### 3. **ETL Pipelines and Real-Time Synchronization**
   - **ETL Pipelines** are generally **batch processes** that extract, transform, and load data. However, more recent approaches use **Change Data Capture (CDC)** or **streaming data processing** (e.g., Kafka) to handle data in real time. 
   - **Real-time synchronization** differs from **batch processing** in that it updates data immediately as changes occur. In systems like Elasticsearch, **streaming data processing** can be applied to ensure data is reflected in real time.

### 4. **Batch Jobs and Elasticsearch**
   - **Elasticsearch** does not automatically handle **batch jobs**. To periodically reflect data in Elasticsearch, separate **services** or **logic** need to be implemented to handle batch processing.
   - **Batch jobs** can be set up to extract data from RDBMS at regular intervals (e.g., once a day) and bulk upload it to Elasticsearch. ETL tools or simple scripts can be used to regularly fetch and update the data.

### 5. **Full-Text Index and Performance**
   - **Elasticsearch** supports **Full-Text Indexing** natively. Similar to RDBMS, Elasticsearch uses **inverted indexes** to optimize text-based search.
   - In terms of **performance**, **Elasticsearch is much faster**. It is optimized as a **search engine**, making it highly efficient for large-scale text searches. In contrast, RDBMS Full-Text Indexes can slow down over time, particularly with large datasets.

### 6. **Elasticsearch’s Distributed System**
   - **Elasticsearch is a distributed system**, where data is split into **shards** and distributed across multiple servers. This differs from **RDBMS Read Replicas**.
   - **Read Replicas** generally replicate data in a **master-slave** model to improve read performance. However, **Elasticsearch** uses a **sharding** approach to distribute data across nodes, enabling parallel processing of data.
   - **Synchronization**: Each node communicates with a **master node** to update data and ensure data consistency. Each shard can independently access data and handle queries.

### 7. **Spell Correction and Fuzzy Search**
   - **Spell correction** is not a built-in feature of **Elasticsearch**, but **autocomplete** or **fuzzy search** can be configured. For instance, using a **fuzzy query** allows Elasticsearch to return results even with typographical errors.
   - **Autocomplete**: Elasticsearch provides an **autocomplete** feature to predict and recommend terms as users type in a search.
   - **Tolerance Settings**: By using **fuzzy queries** or **edge n-grams**, Elasticsearch can be configured to search for similar words even when there are spelling mistakes.

### 8. **Elasticsearch Query Response Format**
   - The query response format of Elasticsearch is **JSON**. Elasticsearch returns search results in a **JSON** format.
   - The response data can be **processed** on the backend before being sent to the client, and the **response format** can be **customized**. For example, the search results can be **filtered** or **sorted** before sending only the relevant information to the client.
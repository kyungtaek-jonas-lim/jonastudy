## **1. Caching Strategies & Cache Eviction Policies**
### **1-1) Caching Strategies**

Caching strategies determine how data is stored and retrieved in cache systems. These methods improve performance and reduce database load.

| **Method** | **Description** |
|-----------|----------------|
| **Lazy Loading** | Data is cached only when requested. If the data is not found in the cache, it is retrieved from the database and stored in the cache for future use. |
| **Eager Loading** | Data is preloaded into the cache at startup or when changes occur in the database. |
| **Write-Through** | Data is written to both the cache and the database simultaneously, ensuring consistency. |
| **Write-Back (Write-Behind)** | Data is first written to the cache and asynchronously persisted to the database later, improving performance but risking data loss if the cache fails. |

**Most common:** `Lazy Loading` and `Write-Through` are the most widely used strategies.

---

### **1-2) Cache Eviction Policies**

Cache eviction policies determine how cache systems remove old or less useful data to free up space.

| **Policy** | **Description** |
|-----------|----------------|
| **TTL (Time-To-Live)** | Cache entries expire and are deleted after a specified time. |
| **LRU (Least Recently Used)** | The least recently accessed cache entry is removed when space is needed. |
| **LFU (Least Frequently Used)** | The least frequently accessed cache entry is removed. |
| **Manual Eviction** | Cache entries are removed explicitly by the application when needed. |

**Most common:** A combination of `TTL` and `LRU` is widely used in most caching systems.
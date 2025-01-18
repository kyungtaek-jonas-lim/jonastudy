# Set

### 1. **HashSet**
- **Features**
  - `HashSet` is a `Set` implemented based on a **HashMap**.
  - Elements are stored using a **hash table**.
  - Does not guarantee the order of elements.
  - Does not allow duplicate elements and allows a single `null` value.
- **Time Complexity**
  - Add, delete, search: Average **O(1)** (performance may degrade in case of hash collisions)
- **Usage Example**
  ```java
  Set<String> hashSet = new HashSet<>();
  hashSet.add("A");
  hashSet.add("B");
  hashSet.add("C");
  ```

---

### 2. **LinkedHashSet**
- **Features**
  - Similar to `HashSet`, but maintains **insertion order**.
  - Uses a doubly linked list internally to manage the order.
  - Does not allow duplicate elements.
- **Time Complexity**
  - Add, delete, search: Average **O(1)** (uses slightly more memory due to order management)
- **Usage Example**
  ```java
  Set<String> linkedHashSet = new LinkedHashSet<>();
  linkedHashSet.add("A");
  linkedHashSet.add("B");
  linkedHashSet.add("C");
  ```

---

### 3. **TreeSet**
- **Features**
  - Stores elements in a **sorted order**.
  - Implemented using a **Red-Black Tree** (binary search tree).
  - Elements must implement the `Comparable` interface or a `Comparator` should be provided at the time of creation.
  - Does not allow duplicate elements.
- **Time Complexity**
  - Add, delete, search: Average **O(log n)**
- **Usage Example**
  ```java
  Set<String> treeSet = new TreeSet<>();
  treeSet.add("C");
  treeSet.add("A");
  treeSet.add("B");
  // Output: [A, B, C] (sorted order)
  ```

---

### 4. **EnumSet**
- **Features**
  - A `Set` implementation specialized for `Enum` types.
  - All values are limited to `Enum` elements, making it very **efficient**.
  - Internally implemented using a bit vector, consuming less memory and being fast.
  - Does not maintain insertion order or sorted order.
- **Time Complexity**
  - Add, delete, search: **O(1)**
- **Usage Example**
  ```java
  enum Day { MONDAY, TUESDAY, WEDNESDAY }
  
  Set<Day> enumSet = EnumSet.of(Day.MONDAY, Day.WEDNESDAY);
  ```

---

### Comparison Summary

| **Implementation** | **Maintains Order**  | **Allows Duplicates** | **Sorted**         | **Time Complexity**    |
|---------------------|----------------------|-----------------------|--------------------|------------------------|
| `HashSet`           | X (No order)        | X                     | X                  | O(1)                   |
| `LinkedHashSet`     | O (Insertion order) | X                     | X                  | O(1)                   |
| `TreeSet`           | X (Sorted order)    | X                     | O (Sorted order)   | O(log n)               |
| `EnumSet`           | X                  | X                     | X                  | O(1) (under conditions)|

- `LinkedHashSet`: Uses a **doubly linked list** internally to manage the order.
- `TreeSet`: Implemented using a **Red-Black Tree** (binary search tree).
- `EnumSet`: All values are limited to `Enum` elements, making it very **efficient**.

---

### Selection Criteria
1. If **fast lookup** is required and order is not important: `HashSet`
2. If **insertion order** needs to be maintained: `LinkedHashSet`
3. If **sorting** is required: `TreeSet`
4. If the elements are of `Enum` type: `EnumSet`





---
# List
### 1. **ArrayList**
- **Features**
  - A `List` implementation based on a **dynamic array**.
  - Elements are stored in a contiguous memory block.
  - Provides **fast reading** and **random access**, but insertion and deletion can be inefficient (especially when modifying middle elements).
  - Allows duplicate elements and maintains insertion order.
- **Time Complexity**
  - Access: **O(1)** (supports random access)
  - Insertion/Deletion: **O(n)** (requires shifting elements for middle modifications)
- **Usage Example**
  ```java
  List<String> arrayList = new ArrayList<>();
  arrayList.add("A");
  arrayList.add("B");
  arrayList.add("C");
  ```

---

### 2. **LinkedList**
- **Features**
  - A `List` implementation based on a **doubly linked list**.
  - Each element is stored as a node containing references to the previous and next elements.
  - **Insertion** and **deletion** are fast, but accessing elements is slower due to sequential search.
  - Allows duplicate elements and maintains insertion order.
- **Time Complexity**
  - Access: **O(n)** (requires sequential traversal)
  - Insertion/Deletion: **O(1)** (if the reference to the target node is known)
- **Usage Example**
  ```java
  List<String> linkedList = new LinkedList<>();
  linkedList.add("A");
  linkedList.add("B");
  linkedList.add("C");
  ```

---

### 3. **Vector**
- **Features**
  - Similar to `ArrayList`, but it is **Thread-Safe**.
  - Provides synchronized methods, making it safe for use in multi-threaded environments but slower than `ArrayList`.
  - Allows duplicate elements and maintains insertion order.
- **Time Complexity**
  - Access: **O(1)**
  - Insertion/Deletion: **O(n)**
- **Usage Example**
  ```java
  List<String> vector = new Vector<>();
  vector.add("A");
  vector.add("B");
  vector.add("C");
  ```

---

### 4. **Stack**
- **Features**
  - An extension of `Vector`, following the **LIFO (Last In, First Out)** structure.
  - Mainly used for stack operations like `push`, `pop`, and `peek`.
  - Thread-safe but less commonly used compared to `Deque` for stack-like operations.
- **Time Complexity**
  - `push`/`pop`: **O(1)**
- **Usage Example**
  ```java
  Stack<String> stack = new Stack<>();
  stack.push("A");
  stack.push("B");
  stack.pop(); // Returns "B"
  ```

---

### Comparison Summary

| **Implementation** | **Underlying Structure** | **Maintains Order** | **Allows Duplicates** | **Features**                           | **Time Complexity (Access/Insertion/Deletion)** |
|---------------------|--------------------------|----------------------|-----------------------|----------------------------------------|------------------------------------------------|
| `ArrayList`         | Dynamic Array           | O                   | O                     | Fast reading/random access             | O(1) / O(n) / O(n)                              |
| `LinkedList`        | Doubly Linked List      | O                   | O                     | Fast insertion/deletion                | O(n) / O(1) / O(1)                              |
| `Vector`            | Dynamic Array           | O                   | O                     | Thread-safe                            | O(1) / O(n) / O(n)                              |
| `Stack`             | Dynamic Array           | O                   | O                     | LIFO structure, thread-safe            | O(1) / O(1) / O(1)                              |

- `LinkedList`: A List implementation based on a doubly linked list.
- `Vector`: Similar to `ArrayList`, but it is **Thread-Safe**.
- `Stack`: **LIFO (Last In, First Out)** structure (`push`, `pop`, and `peek`), Thread-safe
- Key Difference Between `ArrayList` & `LinkedList`
	- **ArrayList**: Uses indices directly, providing **constant time** access for elements.
	- **LinkedList**: Also allows index-based access, but it's **sequential** and thus slower for large lists.

---

### Selection Criteria
1. If **fast reading and random access** are required: `ArrayList`
2. If **frequent insertion and deletion** occur: `LinkedList`
3. For **multi-threaded environments** where synchronization is needed:
   - For general use: `Vector`
   - For stack operations: `Stack`



---
# Map
### 1. **HashMap**
- **Features**
  - `HashMap` is a **non-synchronized** `Map` implementation based on a **hash table**.
  - Keys must be unique, and values can be duplicated.
  - **Insertion order is not guaranteed.**
  - Allows one `null` key and multiple `null` values.
- **Time Complexity**
  - Add, delete, search: **O(1)** (performance may degrade with hash collisions)
- **Usage Example**
  ```java
  Map<String, Integer> hashMap = new HashMap<>();
  hashMap.put("A", 1);
  hashMap.put("B", 2);
  hashMap.put(null, 3); // Allows null key
  hashMap.put("C", null); // Allows null values
  ```

---

### 2. **LinkedHashMap**
- **Features**
  - Similar to `HashMap`, but **maintains insertion order.**
  - Internally uses a doubly linked list to maintain order.
  - Allows one `null` key and multiple `null` values.
- **Time Complexity**
  - Add, delete, search: **O(1)**
- **Usage Example**
  ```java
  Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
  linkedHashMap.put("A", 1);
  linkedHashMap.put("B", 2);
  linkedHashMap.put("C", 3);
  // Output order: A, B, C
  ```

---

### 3. **TreeMap**
- **Features**
  - Stores key-value pairs in **sorted order** of the keys.
  - Implemented using a **Red-Black Tree** (a type of binary search tree).
  - Keys must implement `Comparable` or a custom `Comparator` should be provided.
  - Does **not allow `null` keys** (but allows `null` values).
- **Time Complexity**
  - Add, delete, search: **O(log n)**
- **Usage Example**
  ```java
  Map<String, Integer> treeMap = new TreeMap<>();
  treeMap.put("C", 3);
  treeMap.put("A", 1);
  treeMap.put("B", 2);
  // Output order: A, B, C (sorted order)
  ```

---

### 4. **Hashtable**
- **Features**
  - An older, **synchronized** `Map` implementation.
  - Safe for use in multi-threaded environments but slower than modern alternatives.
  - **Does not allow `null` keys or values.**
  - Currently, `ConcurrentHashMap` is preferred over `Hashtable`.
- **Time Complexity**
  - Add, delete, search: **O(1)** (performance may degrade with hash collisions)
- **Usage Example**
  ```java
  Map<String, Integer> hashtable = new Hashtable<>();
  hashtable.put("A", 1);
  hashtable.put("B", 2);
  ```

---

### 5. **ConcurrentHashMap**
- **Features**
  - A thread-safe `HashMap` for multi-threaded environments.
  - Provides better performance than `Hashtable` by allowing concurrent read and write operations through segment-level locking.
  - **Does not allow `null` keys or values.**
- **Time Complexity**
  - Add, delete, search: **O(1)**
- **Usage Example**
  ```java
  Map<String, Integer> concurrentHashMap = new ConcurrentHashMap<>();
  concurrentHashMap.put("A", 1);
  concurrentHashMap.put("B", 2);
  ```

---

### Comparison Summary

| **Implementation**       | **Maintains Order**      | **Sorted**       | **Thread-Safe** | **Allows Null Keys/Values**     | **Time Complexity**          |
|---------------------------|--------------------------|------------------|-----------------|----------------------------------|------------------------------|
| `HashMap`                | X (No order)            | X               | X               | Key: Yes (1), Value: Yes         | O(1)                         |
| `LinkedHashMap`          | O (Insertion order)     | X               | X               | Key: Yes (1), Value: Yes         | O(1)                         |
| `TreeMap`                | X (Sorted order)        | O (Sorted keys) | X               | Key: No, Value: Yes              | O(log n)                     |
| `Hashtable`              | X                      | X               | O               | Key: No, Value: No               | O(1)                         |
| `ConcurrentHashMap`      | X                      | X               | O               | Key: No, Value: No               | O(1)                         |

- `HashMap`: Insertion order is not guaranteed.
- `LinkedHashMap`: Internally uses a doubly linked list to maintain order.
- `TreeMap`: Implemented using a Red-Black Tree (a type of binary search tree).
- For **thread-safe** operations:
   - Use `ConcurrentHashMap` for better performance.
   - Use `Hashtable` only if legacy code requires it.



---

### Selection Criteria
1. If **fast access and no order** are needed: `HashMap`
2. If **insertion order** must be maintained: `LinkedHashMap`
3. If **sorted keys** are required: `TreeMap`
4. For **thread-safe** operations:
   - Use `ConcurrentHashMap` for better performance.
   - Use `Hashtable` only if legacy code requires it.
   
  
  
---
# Summary

### Set

| **Implementation** | **Maintains Order**  | **Allows Duplicates** | **Sorted**         | **Time Complexity**    |
|---------------------|----------------------|-----------------------|--------------------|------------------------|
| `HashSet`           | X (No order)        | X                     | X                  | O(1)                   |
| `LinkedHashSet`     | O (Insertion order) | X                     | X                  | O(1)                   |
| `TreeSet`           | X (Sorted order)    | X                     | O (Sorted order)   | O(log n)               |
| `EnumSet`           | X                  | X                     | X                  | O(1) (under conditions)|

- `LinkedHashSet`: Uses a **doubly linked list** internally to manage the order.
- `TreeSet`: Implemented using a **Red-Black Tree** (binary search tree).
- `EnumSet`: All values are limited to `Enum` elements, making it very **efficient**.


### List

| **Implementation** | **Underlying Structure** | **Maintains Order** | **Allows Duplicates** | **Features**                           | **Time Complexity (Access/Insertion/Deletion)** |
|---------------------|--------------------------|----------------------|-----------------------|----------------------------------------|------------------------------------------------|
| `ArrayList`         | Dynamic Array           | O                   | O                     | Fast reading/random access             | O(1) / O(n) / O(n)                              |
| `LinkedList`        | Doubly Linked List      | O                   | O                     | Fast insertion/deletion                | O(n) / O(1) / O(1)                              |
| `Vector`            | Dynamic Array           | O                   | O                     | Thread-safe                            | O(1) / O(n) / O(n)                              |
| `Stack`             | Dynamic Array           | O                   | O                     | LIFO structure, thread-safe            | O(1) / O(1) / O(1)                              |

- `LinkedList`: A List implementation based on a doubly linked list.
- `Vector`: Similar to `ArrayList`, but it is **Thread-Safe**.
- `Stack`: **LIFO (Last In, First Out)** structure (`push`, `pop`, and `peek`), Thread-safe
- Key Difference Between `ArrayList` & `LinkedList`
	- **ArrayList**: Uses indices directly, providing **constant time** access for elements.
	- **LinkedList**: Also allows index-based access, but it's **sequential** and thus slower for large lists.



### Map

| **Implementation**       | **Maintains Order**      | **Sorted**       | **Thread-Safe** | **Allows Null Keys/Values**     | **Time Complexity**          |
|---------------------------|--------------------------|------------------|-----------------|----------------------------------|------------------------------|
| `HashMap`                | X (No order)            | X               | X               | Key: Yes (1), Value: Yes         | O(1)                         |
| `LinkedHashMap`          | O (Insertion order)     | X               | X               | Key: Yes (1), Value: Yes         | O(1)                         |
| `TreeMap`                | X (Sorted order)        | O (Sorted keys) | X               | Key: No, Value: Yes              | O(log n)                     |
| `Hashtable`              | X                      | X               | O               | Key: No, Value: No               | O(1)                         |
| `ConcurrentHashMap`      | X                      | X               | O               | Key: No, Value: No               | O(1)                         |

- `HashMap`: Insertion order is not guaranteed.
- `LinkedHashMap`: Internally uses a doubly linked list to maintain order.
- `TreeMap`: Implemented using a Red-Black Tree (a type of binary search tree).
- For **thread-safe** operations:
   - Use `ConcurrentHashMap` for better performance.
   - Use `Hashtable` only if legacy code requires it.
# Set
Java에서 `Set`은 중복을 허용하지 않는 컬렉션 인터페이스입니다. 주요 구현 클래스와 종류는 다음과 같으며, 각 클래스는 동작 방식과 특징에서 차이가 있습니다.

---

### 1. **HashSet**
- **특징**
  - `HashMap`을 기반으로 구현된 `Set`입니다.
  - 요소들은 **해시 테이블**을 사용해 저장됩니다.
  - 요소의 순서를 보장하지 않습니다.
  - 중복 요소를 허용하지 않으며, `null` 값을 하나만 저장할 수 있습니다.
- **시간 복잡도**
  - 추가, 삭제, 탐색: 평균 **O(1)** (해시 충돌 발생 시 성능 저하 가능)
- **사용 예시**
  ```java
  Set<String> hashSet = new HashSet<>();
  hashSet.add("A");
  hashSet.add("B");
  hashSet.add("C");
  ```

---

### 2. **LinkedHashSet**
- **특징**
  - `HashSet`과 유사하지만, **삽입 순서**를 유지합니다.
  - 내부적으로 이중 연결 리스트를 사용하여 순서를 관리합니다.
  - 중복 요소를 허용하지 않습니다.
- **시간 복잡도**
  - 추가, 삭제, 탐색: 평균 **O(1)** (순서 관리로 약간의 추가 메모리 사용)
- **사용 예시**
  ```java
  Set<String> linkedHashSet = new LinkedHashSet<>();
  linkedHashSet.add("A");
  linkedHashSet.add("B");
  linkedHashSet.add("C");
  ```

---

### 3. **TreeSet**
- **특징**
  - **정렬된 순서**로 요소를 저장합니다.
  - 내부적으로 **Red-Black Tree**(이진 탐색 트리)를 사용하여 구현됩니다.
  - 요소가 `Comparable` 인터페이스를 구현하거나, 생성 시 `Comparator`를 제공해야 합니다.
  - 중복 요소를 허용하지 않습니다.
- **시간 복잡도**
  - 추가, 삭제, 탐색: 평균 **O(log n)**
- **사용 예시**
  ```java
  Set<String> treeSet = new TreeSet<>();
  treeSet.add("C");
  treeSet.add("A");
  treeSet.add("B");
  // 출력: [A, B, C] (정렬된 순서)
  ```

---

### 4. **EnumSet**
- **특징**
  - `Enum` 타입에 특화된 `Set` 구현입니다.
  - 모든 값이 `Enum` 요소로 제한되며, 매우 **효율적**으로 작동합니다.
  - 내부적으로 비트 벡터를 사용해 구현되므로 메모리 사용량이 적고 빠릅니다.
  - 삽입 순서 또는 정렬 순서를 유지하지 않습니다.
- **시간 복잡도**
  - 추가, 삭제, 탐색: **O(1)**
- **사용 예시**
  ```java
  enum Day { MONDAY, TUESDAY, WEDNESDAY }
  
  Set<Day> enumSet = EnumSet.of(Day.MONDAY, Day.WEDNESDAY);
  ```

---

### 비교 요약

| **구현 클래스**   | **순서 유지**        | **중복 허용** | **정렬**          | **시간 복잡도**     |
|-------------------|---------------------|---------------|-------------------|---------------------|
| `HashSet`         | X (순서 보장 안 함) | X             | X                 | O(1)                |
| `LinkedHashSet`   | O (삽입 순서)       | X             | X                 | O(1)                |
| `TreeSet`         | X (정렬된 순서)     | X             | O (정렬된 순서)   | O(log n)            |
| `EnumSet`         | X                  | X             | X                 | O(1) (특정 조건)    |

---

### 선택 기준
1. **빠른 검색**이 필요하고 순서가 중요하지 않다면: `HashSet`
2. **삽입 순서**를 유지해야 한다면: `LinkedHashSet`
3. **정렬**이 필요하다면: `TreeSet`
4. 요소가 `Enum` 타입이라면: `EnumSet`



---
# List
Java에서 `List`는 순서가 있는 컬렉션을 나타내는 인터페이스로, 중복을 허용하며, 요소에 **인덱스**를 통해 접근할 수 있습니다. `List`의 주요 구현 클래스는 다음과 같으며, 각각 동작 방식과 특징에서 차이가 있습니다.

---

### 1. **ArrayList**
- **특징**
  - **동적 배열** 기반으로 구현된 `List`.
  - 요소는 연속된 메모리 블록에 저장됩니다.
  - **빠른 읽기**와 **랜덤 접근**을 지원하지만, 삽입과 삭제가 비효율적일 수 있습니다(특히 중간 요소를 수정할 때).
  - 중복을 허용하며, 삽입 순서를 유지합니다.
- **시간 복잡도**
  - 접근: **O(1)** (랜덤 접근이 가능)
  - 삽입/삭제: **O(n)** (중간 삽입 또는 삭제 시 요소를 이동해야 함)
- **사용 예시**
  ```java
  List<String> arrayList = new ArrayList<>();
  arrayList.add("A");
  arrayList.add("B");
  arrayList.add("C");
  ```

---

### 2. **LinkedList**
- **특징**
  - **이중 연결 리스트** 기반으로 구현된 `List`.
  - 각 요소는 노드로 저장되며, 노드는 이전/다음 요소에 대한 참조를 가집니다.
  - **삽입**과 **삭제**가 빠르지만, 요소에 접근할 때는 순차 검색이 필요하므로 느립니다.
  - 중복을 허용하며, 삽입 순서를 유지합니다.
- **시간 복잡도**
  - 접근: **O(n)** (순차 검색 필요)
  - 삽입/삭제: **O(1)** (특정 위치의 노드 참조가 주어질 경우)
- **사용 예시**
  ```java
  List<String> linkedList = new LinkedList<>();
  linkedList.add("A");
  linkedList.add("B");
  linkedList.add("C");
  ```

---

### 3. **Vector**
- **특징**
  - `ArrayList`와 비슷하지만, **Thread-Safe**합니다.
  - 동기화된 메서드를 제공하므로 멀티스레드 환경에서 안전하지만, 성능이 떨어질 수 있습니다.
  - 중복을 허용하며, 삽입 순서를 유지합니다.
- **시간 복잡도**
  - 접근: **O(1)**
  - 삽입/삭제: **O(n)**
- **사용 예시**
  ```java
  List<String> vector = new Vector<>();
  vector.add("A");
  vector.add("B");
  vector.add("C");
  ```

---

### 4. **Stack**
- **특징**
  - `Vector`를 확장한 클래스로, **LIFO (Last In, First Out)** 구조를 따릅니다.
  - 주로 스택 연산 (`push`, `pop`, `peek`)에 사용됩니다.
  - 동기화되어 있어 멀티스레드 환경에서 안전하지만, 일반적인 `List`로는 잘 사용되지 않습니다.
- **시간 복잡도**
  - `push`/`pop`: **O(1)**
- **사용 예시**
  ```java
  Stack<String> stack = new Stack<>();
  stack.push("A");
  stack.push("B");
  stack.pop(); // "B" 반환
  ```

---

### 비교 요약

| **구현 클래스** | **기반 구조**        | **순서 유지** | **중복 허용** | **특징**                            | **시간 복잡도 (접근/삽입/삭제)** |
|-----------------|---------------------|---------------|---------------|------------------------------------|--------------------------------|
| `ArrayList`     | 동적 배열           | O             | O             | 읽기/랜덤 접근이 빠름              | O(1) / O(n) / O(n)            |
| `LinkedList`    | 이중 연결 리스트    | O             | O             | 삽입/삭제가 빠름                  | O(n) / O(1) / O(1)            |
| `Vector`        | 동적 배열           | O             | O             | 동기화 지원                       | O(1) / O(n) / O(n)            |
| `Stack`         | 동적 배열           | O             | O             | LIFO 구조, 동기화 지원             | O(1) / O(1) / O(1)            |

---

### 선택 기준
1. **읽기와 랜덤 접근**이 주로 필요하다면: `ArrayList`
2. **삽입과 삭제**가 빈번하다면: `LinkedList`
3. 멀티스레드 환경에서 동기화가 필요하다면: `Vector`
4. **스택 연산**이 필요하다면: `Stack`





---
# Map
Java에서 `Map`은 **키와 값의 쌍**(key-value pair)으로 데이터를 저장하는 인터페이스로, 키는 중복을 허용하지 않으며 값은 중복될 수 있습니다. 주요 구현 클래스는 다음과 같으며, 각각의 특징과 동작 방식이 다릅니다.

---

### 1. **HashMap**
- **특징**
  - `HashMap`은 **해시 테이블**을 기반으로 구현된 비동기적 `Map`.
  - 키는 고유하며, 중복을 허용하지 않습니다.
  - **삽입 순서가 보장되지 않습니다.**
  - `null` 키를 하나만 허용하며, 여러 `null` 값을 저장할 수 있습니다.
- **시간 복잡도**
  - 삽입, 삭제, 탐색: **O(1)** (해시 충돌 발생 시 성능이 저하될 수 있음)
- **사용 예시**
  ```java
  Map<String, Integer> hashMap = new HashMap<>();
  hashMap.put("A", 1);
  hashMap.put("B", 2);
  hashMap.put(null, 3); // null 키 허용
  hashMap.put("C", null); // null 값 허용
  ```

---

### 2. **LinkedHashMap**
- **특징**
  - `HashMap`과 비슷하지만, **삽입 순서**를 유지합니다.
  - 내부적으로 이중 연결 리스트를 사용하여 순서를 관리합니다.
  - `null` 키와 값을 지원합니다.
- **시간 복잡도**
  - 삽입, 삭제, 탐색: **O(1)**
- **사용 예시**
  ```java
  Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
  linkedHashMap.put("A", 1);
  linkedHashMap.put("B", 2);
  linkedHashMap.put("C", 3);
  // 출력 순서: A, B, C
  ```

---

### 3. **TreeMap**
- **특징**
  - **정렬된 순서**로 키-값 쌍을 저장합니다.
  - 내부적으로 **Red-Black Tree**(이진 탐색 트리)를 사용합니다.
  - 키가 `Comparable` 인터페이스를 구현하거나, 생성 시 `Comparator`를 제공해야 합니다.
  - `null` 키를 허용하지 않습니다(값은 `null` 가능).
- **시간 복잡도**
  - 삽입, 삭제, 탐색: **O(log n)**
- **사용 예시**
  ```java
  Map<String, Integer> treeMap = new TreeMap<>();
  treeMap.put("C", 3);
  treeMap.put("A", 1);
  treeMap.put("B", 2);
  // 출력 순서: A, B, C (정렬된 순서)
  ```

---

### 4. **Hashtable**
- **특징**
  - **동기화된** `Map` 구현으로, 멀티스레드 환경에서 안전합니다.
  - 키와 값 모두 `null`을 허용하지 않습니다.
  - 오래된 클래스이며, 현재는 주로 `ConcurrentHashMap`이 권장됩니다.
- **시간 복잡도**
  - 삽입, 삭제, 탐색: **O(1)** (해시 충돌 발생 시 성능 저하 가능)
- **사용 예시**
  ```java
  Map<String, Integer> hashtable = new Hashtable<>();
  hashtable.put("A", 1);
  hashtable.put("B", 2);
  ```

---

### 5. **ConcurrentHashMap**
- **특징**
  - 동기화된 `HashMap`으로, 멀티스레드 환경에서 사용됩니다.
  - `Hashtable`보다 성능이 뛰어나며, 병렬 처리를 지원합니다.
  - `null` 키와 값을 허용하지 않습니다.
  - 내부적으로 세그먼트 락(Segment Lock)을 사용하여 성능을 향상시킵니다.
- **시간 복잡도**
  - 삽입, 삭제, 탐색: **O(1)**
- **사용 예시**
  ```java
  Map<String, Integer> concurrentHashMap = new ConcurrentHashMap<>();
  concurrentHashMap.put("A", 1);
  concurrentHashMap.put("B", 2);
  ```

---

### 비교 요약

| **구현 클래스**       | **순서 유지**         | **정렬**       | **동기화**  | **null 키/값 허용**      | **시간 복잡도**       |
|-----------------------|-----------------------|----------------|-------------|--------------------------|-----------------------|
| `HashMap`             | X (순서 없음)        | X              | X           | 키: O, 값: O             | O(1)                 |
| `LinkedHashMap`       | O (삽입 순서 유지)   | X              | X           | 키: O, 값: O             | O(1)                 |
| `TreeMap`             | X (정렬된 순서)      | O (정렬된 순서)| X           | 키: X, 값: O             | O(log n)             |
| `Hashtable`           | X                   | X              | O           | 키: X, 값: X             | O(1)                 |
| `ConcurrentHashMap`   | X                   | X              | O           | 키: X, 값: X             | O(1)                 |

---

### 선택 기준
1. **빠른 검색과 수정**이 필요하다면: `HashMap`
2. **삽입 순서**를 유지해야 한다면: `LinkedHashMap`
3. **정렬된 키**를 유지해야 한다면: `TreeMap`
4. 멀티스레드 환경에서 동기화된 `Map`이 필요하다면:
   - 더 나은 성능이 필요하면: `ConcurrentHashMap`
   - 단순 동기화를 원하면: `Hashtable` (권장하지 않음)
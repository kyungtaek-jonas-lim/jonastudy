
## ✅ **GeoHashing**

### 📘 개념
![QuadTree](https://raw.githubusercontent.com/kyungtaek-jonas-lim/jonastudy/main/concept/spatial_indexing_techniques/geohasing.png)
- GeoHash는 위도(latitude)와 경도(longitude)를 이진수로 변환한 후, 이를 **Base32로 인코딩한 문자열로 표현**합니다.
- 이 방식은 **지도 전체를 균일하게 격자로 분할**하며, 원하는 정밀도에 도달할 때까지 영역을 재귀적으로 나눕니다.
  - 이 분할은 **데이터 밀도와 무관하게**(not density-dependent), 단순히 정해진 수준까지 나누는 방식입니다.
- 문자열이 길수록 더 정밀한 위치를 나타냅니다.
- Redis에서는 **RedisGeo** 모듈이 GeoHash 기반으로 동작하며, `GEOADD`, `GEORADIUS` 등의 명령어를 통해 위치 기반 검색을 매우 빠르게 처리할 수 있습니다.

### 👍 장점 (Pros)
| 항목 | 설명 |
|------|------|
| 간편한 계산과 저장 | 별도의 자료구조 없이 쉽게 계산되고 저장되며, 문자열만으로 위치를 표현할 수 있습니다. |
| 공유 용이 | 단일 문자열로 표현되므로, 위치를 **URL, API 등으로 공유하기에 매우 편리**합니다. |
| 근접 검색 최적화 | 인접한 지역은 **공통 prefix**를 가지므로, proximity search에 효율적입니다. |
| 균일한 해시 분포 | hash 값이 전체 공간에 걸쳐 균일하게 분포하여, 로드 밸런싱 등에 유리합니다. |

### 👎 단점 (Cons)
| 항목 | 설명 |
|------|------|
| 위도에 따른 정밀도 차이 | 고위도 지역에서는 **정밀도가 떨어지는 문제**가 있습니다. |
| 바운딩 박스 검색에 비효율 | Z-curve(모튼 커브) 기반 인코딩 특성상 **범위 검색은 복잡해질 수 있음** |
| 경계 문제 | 인접한 위치라도 해시 prefix가 달라질 수 있어 **근접 탐색 

---

## ✅ [QuadTree](https://github.com/kyungtaek-jonas-lim/jonastudy/blob/main/concept/spatial_indexing_techniques/quadtree_ko.md)와 비교

| 항목 | **QuadTree** | **GeoHashing** |
|------|--------------|----------------|
| 구조 | 계층적 트리 | 격자 + 문자열 해시 |
| 데이터 밀도 의존성 | 있음 (density-dependent) | 없음 |
| 정밀도 제어 | 동적으로 조정 가능 | 문자열 길이로 조절 (정적) |
| 공간 검색 | 매우 효율적 (bounding box 포함) | proximity 중심, bounding box는 어려움 |
| 구현 난이도 | 상대적으로 복잡 | 상대적으로 단순 |
| 저장 공간 | 큼 (포인터 등 필요) | 작음 (단일 문자열) |
| PostgreSQL 활용 | PostGIS의 GiST 인덱스로 유사 구현 | `ST_GeoHash()` 가능하나 실무에서는 적음 |
| Redis 활용 | 직접 구현 필요 | RedisGeo에서 기본 제공 |

---

## ✅ [실무 팁](https://github.com/kyungtaek-jonas-lim/jonastudy/blob/main/concept/spatial_indexing_techniques/quadtree_geohashing_tips_ko.md)
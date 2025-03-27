
## ✅ **QuadTrees**

### 📘 개념
![QuadTree](https://raw.githubusercontent.com/kyungtaek-jonas-lim/jonastudy/main/concept/spatial_indexing_techniques/quadtree.png)
- QuadTree는 **2차원 공간을 네 개의 사분면으로 재귀적으로 분할하는 계층적 트리 구조**입니다.
- 공간의 **데이터 밀도(density)**에 따라 트리의 깊이가 달라질 수 있으며, 밀도가 높은 구역은 더 세밀하게 분할됩니다. 이런 특성 덕분에 **density-dependent partitioning**이 가능합니다.
- PostGIS에서도 이와 유사한 공간 인덱싱이 사용되며, 특히 `GiST` 인덱스는 QuadTree 또는 R-Tree 방식으로 공간 데이터를 효과적으로 관리합니다.

### 👍 장점 (Pros)
| 항목 | 설명 |
|------|------|
| 효율적인 계층 구조 | 계층적 구조는 공간 데이터를 빠르게 인덱싱하고 검색하는 데 매우 효율적입니다. |
| 바운딩 박스 및 공간 질의에 적합 | 사분면 분할을 기반으로 한 구조는 **bounding box 검색 및 다양한 공간 질의**에 효과적입니다. |
| 전역 정밀도 유지 | 공간 전체에서 **일관된 정밀도**를 제공하며, 특정 지역에 치우치지 않습니다. |

### 👎 단점 (Cons)
| 항목 | 설명 |
|------|------|
| 복잡한 구현 | GeoHash보다 구현이 더 복잡하며, 트리의 구조 때문에 계산 비용이 더 들 수 있습니다. |
| 높은 저장 공간 요구 | 포인터와 트리 구조로 인해 **더 많은 저장 공간**이 필요합니다. |
| 공유에 부적합 | GeoHash처럼 간단한 문자열 표현이 아니므로 **위치를 직관적으로 공유하기 어려움** |

---

## ✅ [GeoHashing](https://github.com/kyungtaek-jonas-lim/jonastudy/blob/main/concept/spatial_indexing_techniques/geohashing_ko.md)과 비교

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
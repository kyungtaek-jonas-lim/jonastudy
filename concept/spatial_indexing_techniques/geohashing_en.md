
## ✅ **GeoHashing**

### 📘 Overview
![QuadTree](https://raw.githubusercontent.com/kyungtaek-jonas-lim/jonastudy/main/concept/spatial_indexing_techniques/geohasing.png)
- GeoHashing encodes **latitude and longitude** into a **Base32-encoded string** after converting them to binary.
- It recursively splits the earth's surface into a grid until the desired level of precision is reached.  
  - This splitting is **not density-dependent**—regions are divided uniformly regardless of how populated they are.
- The longer the GeoHash string, the more precise the location it represents.
- Tools like **Redis** (via RedisGeo) are built around GeoHashing and support spatial operations like `GEOADD` and `GEORADIUS` using these encoded strings.

### 👍 Pros
| Feature | Description |
|--------|-------------|
| Easy to compute and store | Does not require complex data structures; simple to implement and efficient to store. |
| Easy to share | Encoded as a single string, making it ideal for URLs, APIs, or caching. |
| Efficient for proximity search | Nearby locations often share common prefixes, enabling fast neighborhood lookups. |
| Uniform hash distribution | Evenly distributes values across space, helping in caching and load balancing. |

### 👎 Cons
| Feature | Description |
|--------|-------------|
| Precision varies with latitude | Precision is lower in higher latitudes due to how the grid is encoded. |
| Less effective for bounding box searches | The underlying **Z-order curve** may lead to inefficiencies when performing range-based queries. |
| Boundary issues | Adjacent areas may not share the same prefix, which can cause **gaps in proximity searches**. |
| Not optimal for uneven data distribution | Since it splits space uniformly, GeoHashing may perform poorly in areas with **highly uneven density**.

---

## ✅ Comparison Summary: [QuadTree](https://github.com/kyungtaek-jonas-lim/jonastudy/blob/main/concept/spatial_indexing_techniques/quadtree_en.md) vs. GeoHashing

| Feature | **QuadTree** | **GeoHashing** |
|--------|--------------|----------------|
| Structure | Hierarchical tree | Grid with Base32 string encoding |
| Density awareness | Yes (density-dependent) | No (uniform grid splitting) |
| Precision control | Dynamically adjustable | Fixed by string length |
| Spatial search efficiency | High, especially for bounding boxes | Good for proximity; limited for bounding boxes |
| Implementation complexity | Relatively high | Relatively simple |
| Storage requirements | High (tree structure, pointers) | Low (string only) |
| PostgreSQL usage | Well-supported via PostGIS GiST index | Supported via `ST_GeoHash()`, but rarely used for querying |
| Redis usage | Requires manual structure | Fully supported via RedisGeo module |

---

## ✅ [Practical Tips](https://github.com/kyungtaek-jonas-lim/jonastudy/blob/main/concept/spatial_indexing_techniques/quadtree_geohashing_tips_en.md)
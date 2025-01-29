## **1. Ways of Shortening URLs** ([Reference](https://github.com/kyungtaek-jonas-lim/jonas-api-master/blob/main/src/routes/common/urlRoutes.ts))
There are several common techniques for shortening URLs. Each method has its own advantages and disadvantages.

| **Method** | **Pros** | **Cons** | **Description** |
|-----------|----------|----------|--------------|
| **ShortID (`shortid`)** | Simple and fast | Slightly predictable, deprecated | Generates a random alphanumeric string for short URLs. |
| **Base62 Encoding** | Short, URL-friendly | Can be predictable | Converts numbers into Base62 (0-9, A-Z, a-z), commonly used in URL shorteners. |
| **SHA-256 Hashing** | Same input → same output, prevents duplication | Slight chance of collision when shortened | Uses SHA-256 hashing and extracts the first 8 characters for a shortened URL. |
| **Sequential ID + Random Suffix** | Unique and harder to predict | Slightly longer URLs | Uses a sequential ID with a random suffix to improve uniqueness. |
| **UUID (v4)** | Universally unique | Too long for URL shortening | Generates a UUID and truncates it to create a shortened URL. |

**Recommendation:**  
Among these methods, **Base62 encoding** is the most common and efficient choice for URL shortening services because it produces short, URL-safe strings that are easy to read and share.
# **📘 Section 15 — Caching Deep Dives (11)**

**Read Caching Strategies + Write Caching Strategies + Pros & Cons**

Caching is one of the most important backend concepts. These patterns are frequently asked in **system design interviews** for FAANG, fintech, and high-scale companies.

---

# **Read Caching Strategies**

Read caching strategies define **how an application fetches data** when a read happens.

There are **three main patterns**:

---

## **1️⃣ Cache Aside (Lazy Loading)**

**Most commonly used strategy.**

### ✔ How it works

1. App tries to read from cache
2. If data is NOT in cache → read from DB
3. Write result to cache for future use

```
Client → Cache miss → Database → Cache write → Return data
```

---

### ✔ Advantages

* Simple, widely used
* Only hot data gets cached
* Cache never stores unused/waste data
* Easy to reason about

### ✔ Disadvantages

* First request is slow (cache miss)
* Stale cache if not invalidated properly
* More application logic needed

### ✔ Best When

* Read-heavy workloads
* Data doesn’t change every second
* Ecommerce product pages
* Social media posts

### ✔ Real Examples

* Reddit posts
* Netflix metadata
* Amazon product details via Redis

---

## **2️⃣ Read Through**

### ✔ How it works

* Application always reads **from cache ONLY**
* If miss → cache layer fetches from DB
  (not the application)

```
Client → Cache → (automatically) DB fetch → Cache fill → Return
```

---

### ✔ Advantages

* Simplifies app logic
* Cache stays warm automatically
* Consistent behavior

### ✔ Disadvantages

* Cache becomes bottleneck
* Higher load on caching service
* Slightly slower on miss vs cache-aside

### ✔ Best When

* Need a clean architecture
* Using managed caching platforms

### ✔ Real Examples

* AWS ElastiCache “read-through” mode
* Akamai / Cloudflare edge key-value cache

---

## **3️⃣ Write Through Cache (for reads)**

Although primarily a **write strategy**, write-through enables reads to always hit cache.

### ✔ How It Works

* Every write goes to cache AND DB
* Cache always has the latest version

```
Client Read → Cache → (always up-to-date)
```

### ✔ Best When

* Read performance must be extremely fast
* Strong consistency needed

---

# **Write Caching Strategies**

Write strategies control **what happens when data is updated**.

There are **3 major strategies**:

---

## **1️⃣ Write Through**

### ✔ How it works

* On write:

  * First write to cache
  * Then write to DB
* Cache is always fresh

```
Client → Cache Write → DB Write → Acknowledge
```

---

### ✔ Advantages

* Strong consistency
* Cache never holds stale data
* Safe for critical data

### ✔ Disadvantages

* Higher latency on writes
* More expensive operations
* Slows down write-heavy systems

### ✔ Best When

* Banking
* Financial transactions
* Inventory that must always be correct

### ✔ Real Examples

* DynamoDB + DAX
* Memcached write-through setups

---

## **2️⃣ Write Back (Write Behind)**

**Fastest write strategy**

### ✔ How it works

* Write goes ONLY to cache
* Cache asynchronously updates DB later

```
Client → Cache write → (asynchronously) → DB update
```

---

### ✔ Advantages

* Very fast writes
* Reduces load on DB
* Great for high-throughput systems

### ✔ Disadvantages

* Risk of data loss if cache node fails
* More complex system
* Harder to maintain consistency

### ✔ Best When

* Analytics events
* Logging systems
* User activity streams

### ✔ Real Examples

* Facebook’s TAO
* Kafka-like buffering combined with Redis

---

## **3️⃣ Write Around**

### ✔ How it works

* Write goes to DB ONLY
* Cache is bypassed
* Cache gets filled only on next read

```
Write → DB  
Read → Cache miss → DB → Cache insert
```

---

### ✔ Advantages

* Avoids polluting cache with rarely-read data
* Good for write-heavy but not read-heavy traffic

### ✔ Disadvantages

* Many cache misses after writes
* Read may be slower often

### ✔ Best When

* A lot of writes but few reads
* Logging tables
* User-generated content not frequently accessed

---

# **210. Read Cache Strategies – Pros & Cons**

Here is the full comparison:

---

## **Cache Aside**

| Aspect   | Value                                   |
| -------- | --------------------------------------- |
| **Pros** | Simple, scalable, flexible              |
| **Cons** | First read is slow, stale data possible |
| **Use**  | 90% real systems (ecommerce, blogs)     |

---

## **Read Through**

| Aspect   | Value                                    |
| -------- | ---------------------------------------- |
| **Pros** | Cleaner code, auto-warming               |
| **Cons** | Cache becomes dependency, slower misses  |
| **Use**  | Enterprise systems using managed caching |

---

## **Write Through (for reads)**

| Aspect   | Value                           |
| -------- | ------------------------------- |
| **Pros** | Strong consistency              |
| **Cons** | Slow writes                     |
| **Use**  | Finance, high integrity systems |

---

# **211. Write Cache Strategies – Pros & Cons**

## **Write Through**

| Pros               | Cons           |
| ------------------ | -------------- |
| Strong consistency | Slow writes    |
| Cache always fresh | More expensive |

---

## **Write Back**

| Pros                        | Cons                    |
| --------------------------- | ----------------------- |
| Ultra-fast writes           | Data loss risk          |
| DB load reduced             | Complex, async failures |
| Great for high-scale writes | Hard to debug           |

---

## **Write Around**

| Pros                         | Cons              |
| ---------------------------- | ----------------- |
| Reduces cache pollution      | High cache misses |
| Good for write-heavy systems | Slower reads      |

---

# **🔥 Ultimate Summary Table**

| Strategy      | Read Speed             | Write Speed | Consistency | Ideal Use                    |
| ------------- | ---------------------- | ----------- | ----------- | ---------------------------- |
| Cache Aside   | Medium (miss on first) | Normal      | Medium      | General systems              |
| Read Through  | High                   | Normal      | High        | Large apps w/ managed caches |
| Write Through | High                   | Slow        | Highest     | Financial apps               |
| Write Back    | High                   | Highest     | Low         | Analytics, logs              |
| Write Around  | Medium                 | Normal      | Medium      | Write-heavy workloads        |

---

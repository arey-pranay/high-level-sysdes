# **Introduction**

This section covers data-storage concepts every modern backend engineer must know:

* SQL Databases
* NoSQL Databases
* SQL vs NoSQL differences
* Object Storage
* Cache
* CDN

They each solve **different data problems**, and interviewers expect you to know *when to use which*.

---

# **202. Relational Database / SQL Database**

## ⭐ **What is a SQL / Relational Database?**

A database that stores data in **tables with rows & columns**, following a **predefined schema**.

Popular examples:

* MySQL
* PostgreSQL
* MSSQL
* Oracle
* MariaDB

---

## ⭐ **Need**

* Strict relationships
* Transaction-heavy systems
* Financial / accounting-like correctness
* Complex queries with joins

---

## ⭐ **How It Works**

* Data is stored in **normalized tables**
* Each row represents an entity
* Tables are connected using **foreign keys**
* SQL is used to query

Example table:

| id | name | age |
| -- | ---- | --- |
| 1  | John | 22  |

---

## ⭐ **Advantages**

✔ Strong integrity (ACID transactions)
✔ Complex queries supported (JOINs)
✔ Good for structured, predictable data
✔ Highly optimized for consistency

---

## ⭐ **Disadvantages**

❌ Scaling horizontally is hard
❌ Strict schema → less flexible
❌ JOIN-heavy queries may degrade performance

---

## ⭐ **Used In**

* Banking
* Fintech
* E-commerce orders
* Inventory management
* Government data systems

---

# **203. Non-Relational Database / NoSQL**

## ⭐ **What is NoSQL?**

A database that stores data **without strict tables or schemas**.

Types:

* **Document DB** → MongoDB
* **Key-Value DB** → Redis
* **Wide-Column DB** → Cassandra
* **Graph DB** → Neo4j

---

## ⭐ **Need**

* Flexible schema
* Massive horizontal scalability
* High write throughput
* Distributed systems

---

## ⭐ **How It Works**

Data stored in more flexible formats:

### Example (Document DB):

```json
{
  "name": "John",
  "age": 22,
  "skills": ["react", "node", "sql"]
}
```

No rigid structure → allows rapid changes.

---

## ⭐ **Advantages**

✔ Horizontally scalable
✔ Flexible, no schema migrations
✔ Great performance for distributed apps
✔ Perfect for big data

---

## ⭐ **Disadvantages**

❌ No ACID guarantees in many NoSQL DBs (some exceptions)
❌ Weak consistency (eventual consistency)
❌ Hard for complex JOINs
❌ Sometimes overused unnecessarily

---

## ⭐ **Used In**

* Real-time apps
* IoT
* Social media
* Location-based apps
* Recommendation systems

---

# **204. SQL vs NoSQL**

## ⭐ **Key Comparison Table**

| Feature        | SQL           | NoSQL                           |
| -------------- | ------------- | ------------------------------- |
| Data Structure | Tables        | Documents / Key-value / Graph   |
| Schema         | Fixed         | Flexible                        |
| Scaling        | Vertical      | Horizontal                      |
| Consistency    | Strong (ACID) | Eventual (BASE)                 |
| Best For       | Transactions  | High-speed reads/writes         |
| Query Language | SQL           | Proprietary APIs                |
| Use Case       | Banking, ERP  | Social networks, analytics, IoT |

---

## ⭐ **When to Use SQL**

✔ Data integrity
✔ Complex queries
✔ Transactions
✔ Financial & enterprise apps

## ⭐ **When to Use NoSQL**

✔ Unstructured data
✔ High scalability
✔ Real-time systems
✔ Distributed environments

---

# **205. Object Storage**

## ⭐ **What is Object Storage?**

A storage mechanism for large, unstructured binary files (objects).

Examples:

* AWS S3
* Google Cloud Storage
* Azure Blob Storage
* DigitalOcean Spaces

---

## ⭐ **Need**

* To store huge files efficiently
* Cost-effective storage
* Access via URLs
* 99.999999999% durability

Used for:

* Images
* Videos
* Backups
* Logs
* Models
* Static assets

---

## ⭐ **How It Works**

Each object has:

* **Data**
* **Metadata**
* **Unique ID** / key

Objects stored in **buckets**, retrievable via HTTP.

---

## ⭐ **Advantages**

✔ Unlimited storage
✔ Extremely cheap
✔ Highly durable & available
✔ Accessible via URL
✔ Integrates with CDN

---

## ⭐ **Disadvantages**

❌ Non-transactional
❌ Slow for small frequent reads
❌ Not a database replacement

---

# **206. Cache**

## ⭐ **What is Cache?**

A **temporary storage layer** that stores frequently accessed data for fast retrieval.

Popular:

* Redis
* Memcached
* Browser cache

---

## ⭐ **Need**

* Reduce database load
* Reduce API latency
* Improve user experience

---

## ⭐ **How It Works**

Example:
Instead of hitting DB every time, store:

```json
"user:123": {
  "name": "Pranay",
  "age": 22
}
```

Next time, fetch from **RAM (very fast)** instead of disk.

---

## ⭐ **Advantages**

✔ Extremely fast (RAM)
✔ Reduces load on primary DB
✔ Improves performance massively
✔ Supports TTL (expiry)

---

## ⭐ **Disadvantages**

❌ Data inconsistency risk
❌ Cache invalidation is tricky
❌ Limited RAM storage
❌ Overuse leads to stale data

---

## ⭐ **Used In**

* Authentication sessions
* Rate limiting
* Leaderboards
* Search results
* Recommendation pages
* Ecommerce homepages

---

# **207. CDN — Content Delivery Network**

## ⭐ **What is a CDN?**

A distributed global network of servers that stores and serves **static assets** from the location closest to the user.

Examples:

* Cloudflare
* Akamai
* AWS CloudFront
* Fastly

---

## ⭐ **Need**

* Reduce latency
* Speed up content delivery
* Reduce server load
* Improve SEO

---

## ⭐ **How It Works**

1. Asset uploaded → distributed to edge servers
2. User requests → served from nearest location
3. Faster speed due to lower physical distance

---

## ⭐ **Advantages**

✔ Much faster load times
✔ Saves backend bandwidth
✔ Improves scalability
✔ Adds security (DDoS protection)
✔ Essential for modern apps

---

## ⭐ **Disadvantages**

❌ Costs money under heavy traffic
❌ Cache invalidation issues
❌ Dynamic content is harder to cache

---

# **📌 Quick Summary Cheat Sheet**

| Concept        | Purpose                                      |
| -------------- | -------------------------------------------- |
| SQL            | Structured, relational data with consistency |
| NoSQL          | Flexible, scalable distributed data          |
| Object Storage | Large binary files                           |
| Cache          | Fast reads for hot data                      |
| CDN            | Fast global delivery of static content       |

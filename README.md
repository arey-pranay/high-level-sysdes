## Disclaimer: Any media file used here probabl belongs to the udemy course mentioned in the repo description. A must-buy course if you want to learn about system design with real examples.

### **Client & Server**

**Definition:**

* The *client* is the entity that requests data or services (e.g., a browser or mobile app).
* The *server* is the entity that provides responses to those requests (e.g., web server, database server).

**Key Points:**

* Communication occurs using HTTP/HTTPS protocols.
* The client sends a **request** → the server processes it → and sends back a **response**.
* Servers can be **stateless** (e.g., REST APIs) or **stateful** (e.g., sockets).

**Example:**
Browser (client) → makes GET request to → `api.example.com` (server) → returns data as JSON.

---

### **Database**

**Definition:**
A database is a structured collection of data that allows efficient storage, retrieval, and management.

**Types:**

1. **Relational Databases (SQL)** — MySQL, PostgreSQL

   * Data stored in tables (rows & columns)
   * Relationships via foreign keys
   * Support ACID properties
2. **NoSQL Databases** — MongoDB, Cassandra, Redis

   * Store data in flexible formats (documents, key-value, wide-column, graph)
   * Designed for scalability and high availability

**Trade-offs:**
SQL ensures consistency; NoSQL provides scalability.

---

### **Vertical vs Horizontal Scaling**

**Vertical Scaling (Scaling Up):**

* Add more power (CPU, RAM, SSD) to the existing server.
* Easier to implement but limited by hardware limits.
* Example: Upgrading a 4-core server to 16-core.

**Horizontal Scaling (Scaling Out):**

* Add more servers to distribute the load.
* Achieved using load balancers and distributed systems.
* Example: Adding multiple web servers to handle requests.

**Comparison:**

| Factor      | Vertical           | Horizontal          |
| ----------- | ------------------ | ------------------- |
| Complexity  | Low                | High                |
| Scalability | Limited            | Virtually unlimited |
| Cost        | Expensive at scale | More flexible       |
| Downtime    | Usually needed     | Often none          |

---

### **Load Balancer**

**Definition:**
A load balancer distributes incoming network traffic across multiple servers to ensure no single server is overloaded.

**Types:**

1. **Layer 4 (Transport-level)** — Distributes traffic based on IP and port.
2. **Layer 7 (Application-level)** — Distributes based on URL, cookies, headers, etc.

**Benefits:**

* Improves reliability and uptime
* Increases throughput
* Enables horizontal scaling

**Examples:** Nginx, HAProxy, AWS ELB

---

### **Database Sharding**

**Definition:**
Sharding is splitting a large database into smaller, faster, more manageable parts called **shards**.

**Key Concepts:**

* Each shard holds a portion of the data (e.g., by user ID range).
* Reduces read/write load on each shard.
* Sharding key determines which shard data belongs to.

**Challenges:**

* Cross-shard queries are complex.
* Rebalancing data when shards grow unevenly.

---

### **Database Replication**

**Definition:**
Replication is the process of copying data from one database server to another.

**Types:**

1. **Master-Slave (Primary-Replica):**

   * Writes happen on the master.
   * Reads can happen on slaves.
2. **Multi-Master:**

   * All nodes can handle writes.
   * Harder to maintain consistency.

**Benefits:**

* High availability
* Read scalability
* Fault tolerance

**Example:**
PostgreSQL Replication, MySQL Binlog Replication

---

### **Cache**

**Definition:**
A cache temporarily stores frequently accessed data for faster retrieval.

**Types:**

* **In-memory cache:** Redis, Memcached
* **Application cache:** Local or session-level caching

**Benefits:**

* Reduces database load
* Improves response time
* Enhances scalability

**Common Strategies:**

* **Write-through:** Data written to cache + DB
* **Write-back:** Data written to cache, DB later
* **Cache-aside:** App checks cache → if miss → fetch DB → store in cache

---

### **Content Delivery Network (CDN)**

**Definition:**
A CDN is a network of geographically distributed servers that cache and deliver content closer to users.

**Purpose:**

* Reduce latency
* Improve site performance
* Offload traffic from the origin server

**Examples:** Cloudflare, Akamai, AWS CloudFront

**How it works:**
User requests → routed to nearest CDN edge server → if content cached, served directly.

---

### **Monolith & Microservice**

**Monolithic Architecture:**

* Entire application (frontend + backend + DB logic) is one unified codebase.
* Simple to deploy and develop initially.
* Hard to scale individual components.

**Microservices Architecture:**

* App split into independent, self-contained services.
* Each service has its own database and API.
* Easier to scale and deploy individually.

**Comparison:**

| Factor          | Monolith  | Microservice |
| --------------- | --------- | ------------ |
| Deployment      | One unit  | Independent  |
| Scaling         | Whole app | Per service  |
| Fault isolation | Poor      | Strong       |
| Complexity      | Low       | High         |

---

### **Message Queue**

**Definition:**
A message queue enables asynchronous communication between services.

**How it works:**

* Producer sends messages to a queue.
* Consumer reads and processes them later.

**Benefits:**

* Decouples systems
* Handles spikes in traffic
* Ensures reliability (no message loss)

**Examples:** RabbitMQ, Kafka, AWS SQS

**Use Case:**
Order placed → Message sent to queue → Payment, inventory, and email services process independently.

---

### **API Gateway**

**Definition:**
An API Gateway is a single entry point that routes requests to multiple backend services.

**Responsibilities:**

* Routing and load balancing
* Authentication and rate limiting
* Response aggregation
* Logging and monitoring

**Benefits:**

* Simplifies client communication
* Centralized security and metrics

**Examples:** Nginx, Kong, AWS API Gateway

**Use Case:**
Mobile app → sends request to API Gateway → routes to User, Order, and Payment services.

# ** GraphQL**

## ⭐ **What is GraphQL?**

A **query language** + **runtime** for APIs that allows clients to specify **exactly the data they need** — no more, no less.

Created by **Facebook**.

---

## ⭐ **Need**

* Traditional REST often over-fetches/under-fetches.
* Mobile devices need optimized network payloads.
* Modern apps require high flexibility (e.g., Instagram-like single feed with mixed data).

---

## ⭐ **How It Works**

Client sends a **structured query**:

```graphql
{
  user(id: "1") {
    name
    age
    posts {
      title
    }
  }
}
```

Server returns **exact shape** of requested data.

---

## ⭐ **Advantages**

✔ Fetch only the required data
✔ Single endpoint for all operations (`/graphql`)
✔ Strongly typed schema
✔ Great for complex UIs (React, React Native)
✔ Good for microservices aggregation

---

## ⭐ **Disadvantages**

❌ Over-complex for simple CRUD APIs
❌ Caching is harder compared to REST
❌ Requires GraphQL server + schema overhead
❌ File uploads, authentication require patterns

---

## ⭐ **Real-Life Tech Examples**

* Facebook
* GitHub API
* Shopify API
* Netflix
* Airbnb

---

## ⭐ **When to Choose GraphQL**

Choose GraphQL when:
✔ UI needs multiple nested resources in one request
✔ You want to avoid API versioning
✔ Mobile apps need optimized payload
✔ You need schema-driven development
✔ You want a single endpoint for all data

**Don’t choose GraphQL when:**
❌ Simple CRUD backend
❌ High caching requirements (CDN-friendly REST is better)

---

## ⭐ **Components**

* Schema
* Query type
* Mutation type
* Resolvers
* GraphQL server (Apollo/Express/NestJS)

---

# ** gRPC**

## ⭐ **What is gRPC?**

A **high-performance, binary-based, transport protocol** for service-to-service communication.

Uses:

* **Protocol Buffers (Protobuf)** instead of JSON
* **HTTP/2** instead of HTTP/1.1
* **Streaming** support

Created by **Google**.

---

## ⭐ **Need**

* Microservices communicating internally
* Extremely fast and low-latency communication
* Strongly typed contracts (Protobuf schemas)

---

## ⭐ **How It Works**

1. You define a `.proto` file:

```protobuf
service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
}
```

2. gRPC code generator produces **client + server** code in any language.
3. Communication happens over HTTP/2 using a binary protocol.

---

## ⭐ **Advantages**

✔ Extremely fast (binary, HTTP/2)
✔ Bi-directional streaming
✔ Very lightweight payload
✔ Auto-generated clients
✔ Strong type safety
✔ Great for microservices

---

## ⭐ **Disadvantages**

❌ Not ideal for browsers (limited HTTP/2 streaming)
❌ Harder to debug than JSON
❌ Requires Protobuf learning
❌ Not SEO-friendly (not for public-facing APIs)

---

## ⭐ **Real-Life Tech Examples**

* Google
* Netflix
* Postman internal services
* Uber microservices
* Dropbox

---

## ⭐ **When to Choose gRPC**

Choose gRPC when:
✔ Microservices talk internally
✔ You need real-time streaming (chat, logs, telemetry)
✔ Low latency is critical
✔ Polyglot system (Go + Python + Java)

Avoid if:
❌ API needs to be consumed directly by browsers
❌ You need human-readable responses (use REST/GraphQL)

---

## ⭐ **Components**

* `.proto` schema
* gRPC client
* gRPC server
* Interceptors
* Load balancers

---

# ** Message Queues**

## ⭐ **What is a Message Queue?**

A system where different services communicate **asynchronously** by sending messages to a queue — the receiver processes them later.

Examples: Kafka, RabbitMQ, SQS.

---

## ⭐ **Need**

* Decouple services
* Avoid blocking operations
* Process heavy tasks asynchronously
* Ensure reliability even when services fail

---

## ⭐ **How It Works**

1. Producer sends message
2. Message stored in queue or topic
3. Consumer picks message when ready
4. Processes it
5. Acknowledges completion

---

## ⭐ **Advantages**

✔ Decoupled architecture
✔ High reliability and persistence
✔ Handles spikes in traffic
✔ Enables event-driven architecture
✔ Great for microservices
✔ Improves system resilience

---

## ⭐ **Disadvantages**

❌ Adds operational complexity
❌ Debugging becomes harder
❌ Requires strong monitoring
❌ Latency is introduced (not real-time)

---

## ⭐ **Real-Life Tech Examples**

* **Kafka** → Netflix, LinkedIn
* **RabbitMQ** → Uber, Instagram
* **AWS SQS** → Amazon ecosystem
* **Google Pub/Sub**
* **Redis Streams**

---

## ⭐ **When to Choose Message Queues**

Choose MQ when:
✔ Heavy tasks (email sending, video encoding)
✔ Event-driven microservices
✔ Need durability / retries
✔ Systems need decoupling

Avoid when:
❌ You need real-time sync responses
❌ Simple API with no async work

---

## ⭐ **Components**

* Producer
* Queue/Topic
* Consumer
* Broker (Kafka/RabbitMQ server)
* Acknowledgement & retry system

---

# ** REST API**

## ⭐ **What is REST?**

A web API architectural style that uses **HTTP** for communication between client and server.

Data is typically in **JSON**.

---

## ⭐ **Need**

* To allow clients (web, mobile, microservices) to fetch data using familiar HTTP methods.

---

## ⭐ **How It Works**

Uses common HTTP verbs:

| Verb   | Meaning      |
| ------ | ------------ |
| GET    | Fetch data   |
| POST   | Create data  |
| PUT    | Replace data |
| PATCH  | Modify data  |
| DELETE | Remove data  |

---

## ⭐ **Advantages**

✔ Simple
✔ Works on all browsers
✔ Easy caching
✔ Great for public APIs
✔ Easy debugging
✔ SEO-friendly

---

## ⭐ **Disadvantages**

❌ Over-fetching/under-fetching issues
❌ Client-dependent on server-defined responses
❌ Multiple round-trips for nested data

---

## ⭐ **Real-Life Examples**

* Twitter API
* Stripe API
* GitHub REST
* Google Maps API
* Any HTTP-based client-server architecture

---

## ⭐ **When to Choose REST**

Choose REST when:
✔ Public API
✔ Mobile + Web usage
✔ SEO needed
✔ Caching is critical
✔ Simpler CRUD system

Avoid when:
❌ Very nested data (GraphQL better)
❌ High performance microservices (gRPC better)

---

## ⭐ **Components**

* Resource URLs
* HTTP methods
* Status codes
* JSON/XML payload

---

# **📌 Quick Comparison Table**

| Feature         | REST        | GraphQL         | gRPC              | Message Queue   |
| --------------- | ----------- | --------------- | ----------------- | --------------- |
| Protocol        | HTTP/1.1    | HTTP            | HTTP/2            | N/A (async)     |
| Data Format     | JSON/XML    | JSON            | Protobuf (binary) | Binary/JSON     |
| Speed           | Medium      | Medium          | **Fastest**       | Asynchronous    |
| Real-time       | ❌           | ❌               | ✔ (streaming)     | ❌               |
| Use Case        | Public APIs | Complex UI      | Microservices     | Async tasks     |
| Flexibility     | Low         | **High**        | Medium            | High            |
| Browser Support | Excellent   | Excellent       | Limited           | N/A             |
| Best For        | CRUD APIs   | Mobile/Frontend | Internal services | Background jobs |

---

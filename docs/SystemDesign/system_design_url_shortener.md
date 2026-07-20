# System Design Revision Notes - URL Shortener

## Goal

Convert

https://very-long-url.com/abc

↓

https://tiny.ly/aB12X

---

# Functional Requirements

- Create short URL
- Redirect to original URL
- Support millions of URLs
- Fast redirects
- High availability

---

# APIs

## Create URL

POST /shorten

Request

{
  "url":"https://google.com"
}

Response

{
  "shortUrl":"https://tiny.ly/aB12X"
}

---

## Redirect

GET /aB12X

Response

HTTP 302 Redirect

Location:
https://google.com

---

# High-Level Architecture

Client

↓

Application Load Balancer

↓

Application Servers

↓

Redis Cache

↓

Primary Database

↓

(Optional) Read Replicas

---

# Database Schema

Table: urls

| Column | Purpose |
|---------|----------|
| id | Primary Key |
| short_code | Unique short URL |
| original_url | Actual URL |
| created_at | Creation Time |
| expiry | Expiry Date |
| click_count | Analytics |

Index

short_code

---

# Request Flow

Client

↓

ALB

↓

Application Server

↓

Redis

↓

Cache Hit?

YES

↓

Return Original URL

NO

↓

Database

↓

Update Redis

↓

Return Original URL

This pattern is called:

Cache-Aside

---

# Why Redis?

Because the system is

Read Heavy

Example

Create URLs

10 Million/day

Redirects

500 Million/day

Reads >> Writes

Redis reduces database load and improves response time.

---

# Why Load Balancer?

Distributes traffic across multiple servers.

Benefits

- High availability
- Horizontal scaling
- Fault tolerance

---

# Why Stateless Servers?

Servers do not store user session or request state.

Any request can go to any server.

Easy to scale horizontally.

---

# Short URL Generation Options

## Option 1

Random String

Pros

- Simple

Cons

- Collision checks required

---

## Option 2 (Preferred)

Auto Increment ID

↓

Base62 Encoding

Pros

- No collisions
- Compact
- Fast

---

## Option 3

Hash Original URL

Pros

- Deterministic

Cons

- Collision handling required

---

# Scaling Techniques

- Redis Cache
- Read Replicas
- Database Indexing
- Load Balancer
- Horizontal Scaling
- CDN (Global Access)

---

# Failure Handling

Redis Down

↓

Read directly from Database

System becomes slower

NOT unavailable

---

# Analytics

Every redirect produces an event.

Instead of writing directly to the database:

Application

↓

Kafka / SQS

↓

Analytics Worker

↓

Analytics Database

Benefits

- Fast redirects
- Asynchronous processing
- Better scalability

---

# Rate Limiting

Prevent abuse.

Example

100 URL creations per minute per user.

Can be implemented using Redis.

---

# Interview Discussion Points

- Functional Requirements
- Non-functional Requirements
- APIs
- Database Schema
- Cache Strategy
- Read vs Write Ratio
- Load Balancer
- Stateless Servers
- Short Code Generation
- Scaling
- Failure Handling
- Analytics
- Trade-offs

---

# Trade-offs

Random String

+ Easy

- Collision detection

Base62

+ No collisions

+ Predictable

Hash

+ Deterministic

- Collision handling

---

# Daily Checklist

□ Can I explain the API?

□ Can I draw the architecture?

□ Can I explain Cache-Aside?

□ Why Redis?

□ Why Load Balancer?

□ Why Stateless Servers?

□ Why Base62?

□ What happens if Redis fails?

□ How would I scale to 1 Billion redirects/day?

If you can answer these without looking, you understand the fundamentals of URL Shortener design.
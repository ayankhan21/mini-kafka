# 🧩 Concurrent Event Streaming Platform (mini-Kafka)

A lightweight, Kafka-inspired **event streaming platform** built with **Java (Spring Boot)** and **React**, designed to explore concepts like concurrency, partitioning, consumer groups, and performance tuning.  
It demonstrates how distributed event brokers manage **throughput**, **latency**, **retention**, and **real-time monitoring** — all in a reproducible local setup.

---

## 🚀 Features

### 🧠 Core System
- **Producers → Broker → Consumers** flow
- **Partitioned queues** with append-only log persistence
- **Thread-pool based concurrency** for producers & consumers
- **Offset management** per consumer group
- **Retention & replay** from persisted logs
- **Backpressure and rate limiting** for overload protection

### 📊 Monitoring & Metrics
- Real-time metrics via **Server-Sent Events (SSE)**
- Metrics tracked:
  - Events per second (produced/consumed)
  - Queue depth per partition
  - Consumer lag
  - Enqueue latency (p50, p95)
- Frontend dashboard visualizing throughput and lag

### 🧰 Tooling
- Load generator for performance testing (multi-threaded producer)
- Benchmarks using **JMH**
- Stress tests via **JMeter**
- One-command local setup using **Docker Compose**

---

## 🏗️ Architecture Overview


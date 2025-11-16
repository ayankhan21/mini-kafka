# 🧩 Concurrent Event Streaming Platform (mini-Kafka)

A lightweight, Kafka-inspired **event streaming platform** built with **Java** , **gPRC** and **React**, designed to explore concepts like concurrency, partitioning, consumer groups, and performance tuning.
With the aim of achieving a throughput of between 50k - 100k events/minute, gRPC was one of the best alternatives for inter service Rest API calls.
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

## ⚙️ Overview

This system simulates a miniature Kafka-like environment where one service (Payments) continuously emits thousands of events per minute.  
Other services (Orders, Notifications, Data Analytics) consume those events in parallel via **consumer groups**.

A **Node.js Aggregator** collects live metrics from all consumers and streams them to a **React dashboard** that visualizes throughput, lag, and queue depths in real time.

Payments → [Broker / Partitions] → {Orders, Notifications, Data Analytics}
↓
Node Aggregator → React UI

## 🧩 Services

| Service | Role | Language |
|----------|------|-----------|
| **Payments Service** | Produces events at a fixed or user-defined rate (e.g., 10k/min) | Java |
| **Orders Service** | Consumes events; simulates order processing | Java |
| **Notifications Service** | Consumes events; mimics message delivery | Java |
| **Data Analytics Service** | Consumes events; aggregates or logs metrics | Java |
| **Node Aggregator** | Collects live consumer stats and streams via SSE/WebSocket | Node.js |
| **Frontend Dashboard** | Visualizes real-time event rates, consumer lag, queue depth | React + Vite |
| **Mini-Broker** | In-memory Kafka-like broker handling partitions, offsets, backpressure | Java |

---

## 🏗️ Architecture

- **Partitioned Log Model** — Events are distributed across partitions, providing parallel consumption.
- **Consumer Groups** — Each service has its own group; scaling consumers increases throughput.
- **Backpressure & Rate Limiting** — Protects hot partitions from overload.
- **Monitoring Layer** — Node Aggregator throttles metrics slightly for near-real-time updates.
- **Full Dockerized Environment** — All seven containers communicate over a shared bridge network.

---

## 🧰 Repositories

| Repo | Description |
|------|--------------|
| [main-infra](https://github.com/ayankhan/event-stream-infra) | Contains `docker-compose.yml`, environment configs |
| [payments-service](https://github.com/ayankhan/payments-service) | Event producer |
| [orders-service](https://github.com/ayankhan/orders-service) | Consumer service |
| [notifications-service](https://github.com/ayankhan/notifications-service) | Consumer service |
| [data-analytics-service](https://github.com/ayankhan/data-analytics-service) | Consumer service |
| [node-aggregator](https://github.com/ayankhan/node-aggregator) | Real-time event forwarder |
| [frontend-dashboard](https://github.com/ayankhan/frontend-dashboard) | React-based visualization |
| [mini-kafka-broker](https://github.com/ayankhan/mini-kafka-broker) | In-memory broker core |

---

## 🚀 Run the System (One Command)

After cloning all repositories into one directory, simply run:

```bash```
docker compose up

This spins up all containers:
broker → consumers → node-aggregator → frontend

# Once running:
- Visit the React dashboard at http://localhost:5173
- Click “Start Stream” to trigger the Payments producer
# Watch live charts for:
- Events per second/minute
- Queue depth & lag per service
- Consumer performance comparison

All services automatically connect to the shared virtual network and communicate internally.
No manual setup or configuration is required.




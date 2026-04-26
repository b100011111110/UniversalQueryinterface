# 🧠 UniversalQueryInterface

> **An adaptive, multi-layer context intelligence system for unstructured information retrieval across heterogeneous data sources.**

[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](./LICENSE)
[![Python](https://img.shields.io/badge/python-3.10%2B-blue?style=flat-square)](https://python.org)

---

> **Early Development / MVP Phase** — This is an experimental architecture and research prototype. The system design is expected to evolve significantly as implementation progresses.

---

## 📖 Overview

**UniversalQueryInterface** is an MCP (Model Context Protocol) server designed to handle **unstructured information from multiple heterogeneous data sources** by routing queries across different database types through a unified orchestration engine.

Rather than treating data as static records, this system treats every piece of information as **dynamic contextual memory** — scored, layered, connected to related entities, and subject to time-based importance decay.

The long-term vision is a **self-evolving retrieval engine** that bridges:

- 🗄️ **Structured databases** (SQL/PostgreSQL)
- 🕸️ **Graph-based reasoning** (Neo4j)
- 🔍 **Semantic vector search** (ChromaDB)
- 📈 **Time-series data** (InfluxDB)
- ⚡ **Intelligent caching and load control** (Redis)

All unified under a single Python orchestration layer.

---

## 🎯 Project Goal

To build a **self-evolving contextual retrieval system** that does not simply store data — but instead maintains evolving contextual memory across multiple data sources with:

- ⏱️ **Time-aware importance scoring**
- 🗂️ **Layered memory retrieval**
- 🧩 **Graph-based multi-hop reasoning**
- 🔄 **Adaptive caching and intelligent routing**

---

## 🏛️ System Architecture

### Phase 1 (Current)

```
┌─────────────────────────────────────────────────────────────┐
│                    MCP Client / LLM Agent                   │
└────────────────────────┬────────────────────────────────────┘
                         │  query
                         ▼
┌─────────────────────────────────────────────────────────────┐
│              Python Orchestration Layer                     │
│   • Query routing       • Result merging & ranking          │
│   • Concurrency mgmt    • Deduplication coordination        │
└───┬──────────────────┬──────────────────┬───────────────────┘
    │                  │                  │
    ▼                  ▼                  ▼
┌──────────┐    ┌───────────┐    ┌─────────────────┐
│  Neo4j   │    │ MongoDB   │    │   PostgreSQL    │
│  Graph   │    │ Documents │    │   (SQL / RDBMS) │
│  Memory  │    │           │    │                 │
└──────────┘    └───────────┘    └─────────────────┘
      │
      ▼
┌───────────────────────┐
│   Multi-Layer Memory  │
│  (Narrow → Wide ctx)  │
└───────────────────────┘

  ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ -----┐
  │  ChromaDB (Vector)  — selective use only       │
  │  Not all data; only curated high-value items   │
  └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ -----┘
```

### Future Phases *(Planned)*

Redis sieve layer, InfluxDB time-series, and full memory lifecycle will be introduced in later phases.

---

## 🧩 System Components

### 🔹 1. Multi-Source Data Integration

Connects to multiple heterogeneous databases through a unified connector interface:

#### Databases

| Database       | Type              | Role                                   |
|----------------|-------------------|----------------------------------------|
| PostgreSQL     | Relational SQL    | Structured data storage                |
| Neo4j          | Graph Database    | Relationships, reasoning & memory      |
| MongoDB        | Document Store    | Unstructured / semi-structured data    |

#### Selective / Optional

| Database       | Type              | Role                                              | 
|----------------|-------------------|---------------------------------------------------|
| ChromaDB       | Vector Database   | Semantic search — **curated data only, not full** |

> ⚠️ ChromaDB is **not** a primary store. It holds only selected, high-value data items where semantic similarity search is specifically needed. 

#### Future Phases

| Database       | Type              | Role                            | Status          |
|----------------|-------------------|---------------------------------|-----------------|
| Redis          | In-Memory Cache   | Sieve layer & fast lookups      | 🔲 Future phase |
| InfluxDB       | Time-Series DB    | Temporal data & metrics         | 🔲 Future phase |

---

### 🔹 2. Multi-Layer Memory Model 

Data is organized into evolving layers where **layer depth determines context breadth**, not importance:

```
Layer 1 (Narrow)  — Highly specific context; precise, focused information
Layer 2           — Slightly broader context; related entities and details
Layer 3           — Intermediate context; topic-level associations
Layer 4           — Broad context; domain-wide relationships
Layer 5 (Wide)    — Broadest context; general background knowledge
```

The deeper the layer, the **wider the contextual scope** of the data it holds. A query may retrieve from a single layer for precision, or span multiple layers for richer contextual understanding.

> Layers are not static — their boundaries and definitions will evolve as the system matures.

---

### 🔹 3. Importance & Decay System 

Each data entity will eventually support:

| Property              | Description                                   |
|-----------------------|-----------------------------------------------|
| **Importance Score**  | Assigned at ingestion; updated on access      |
| **Time-Based Decay**  | Score degrades as data ages                   |
| **Frequency Boost**   | Score increases with repeated access          |
| **Layer Promotion**   | High-scoring items move to hotter layers      |
| **Layer Demotion**    | Low-scoring items move to colder layers       |
| **Eviction**          | Out-of-context data is removed from memory    |

---
### 🔹 4. Dual Mode Operation *(Planned)*

#### 🌞 Day Mode — Serving Mode
- Optimized for **fast retrieval**
- Operates on cached + hot memory only
- Serves only the most important, recent data
- **Target latency:** 5–30 seconds per query

#### 🌙 Night Mode — Processing Mode
- Background processing window for:
  - 🕸️ Graph updates and relationship building
  - 🧹 Deduplication across sources
  - 🔄 Memory restructuring and layer rebalancing

### 🔹 4. Redis Sieve Layer *(Planned)*

A lightweight control layer using Redis to ensure system stability under unpredictable load:

- 🚦 **Request caching** — absorbs burst traffic spikes
- 🗃️ **Temporary state storage** — holds in-flight query context
- ⚡ **Fast lookup** — serves repeated queries from memory
- 🔀 **Traffic shaping** — prevents overloading downstream databases

---

## 🔬 Research Context

This project is being developed as a **research-oriented prototype** to explore:

- **Multi-source data orchestration** — How can a single system coherently query and merge results from fundamentally different database paradigms?
- **Context-aware retrieval** — Can importance scoring and decay produce more relevant results than naive lookups?
- **Adaptive memory hierarchies** — What are the right tradeoffs between retrieval speed and memory depth?
- **Graph-based reasoning over heterogeneous data** — How do graph relationships across multi-source entities enable reasoning that flat retrieval cannot?
- **Load-aware intelligent caching** — Can a Redis sieve layer meaningfully absorb real-world traffic variance?

---
## 🤝 Contributing

This project is in early architecture and experimentation phase. Contributions, ideas, and feedback are welcome — especially around:

- Graph memory design patterns
- Distributed caching strategies
- Multi-source query fusion techniques

Please open an issue before submitting a pull request to discuss significant changes.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

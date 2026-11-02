# 1.3 AI Ready

Engineering-as-Code is architected from the ground up to enable autonomous AI agents to operate as reliable, context-aware co-authors of codebases. 

This readiness extends far beyond simple prompt engineering: it is embedded directly into the **document formats, standardized metadata, deterministic directory layout, and predictable taxonomy** of the repository.

---

### 1.3.1 Markdown and YAML Frontmatters

To prevent context-window exhaustion and ensure deterministic navigation, every governance artifact under `arch/` starts with standardized YAML frontmatter:

```yaml
---
id: ADR-0002
title: Document Title
phase: decision
type: adr
status: accepted
created: YYYY-MM-DD
updated: YYYY-MM-DD
authors: ["Author"]
relations:
  derives_from: ["RFC-0004"]
  governed_by: []
  implements: []
  affects: ["doc/book/"]
---
```

#### Deterministic Graph Traversal
* **Targeted Ingestion:** Rather than flooding an LLM with massive, uncurated code dumps, agents first inspect `.eoc/taxonomy.yaml` and the YAML frontmatter headers across relevant folders. They selectively pull only the exact documents pertinent to their task.
* **Bi-Directional Lineage:** The `relations` block links every document upstream (`derives_from`, `governed_by`) and downstream (`implements`, `affects`). Agents can traverse upstream to confirm original business intent and governing decisions, or downstream to assess the blast radius of a proposed modification.

---

### 1.3.2 Agent-Driven Architecture

The framework establishes strict structural constraints that make agent interactions safe, predictable, and verifiable:

* **The Hierarchy of Truth:** Accepted decisions (`ADR`) are treated as immutable axioms. An agent cannot propose code or designs that contradict an active ADR without drafting a new RFC to formally debate the pivot.
* **The Test Twin Axiom:** An agent is structurally blocked from writing production code in `src/` without first authoring or updating the paired test specification in `arch/05-design/` and the executable test suite in `tst/`.
* **Zero Unanchored Commits:** Every change introduced by an agent must trace back to an approved upstream design and decision.

#### Extensibility: MCP Knowledge Services & Enterprise AI Search
Because the directory hierarchy is strictly categorized (`arch/01-seed/`, `02-concept/`, etc.) and all artifacts possess explicit metadata (`type`, `phase`, `status`), the repository is an ideal data source for modern AI infrastructure:

1. **Model Context Protocol (MCP) Knowledge Services:**
   * Teams can easily build a repository-level **MCP Server** that exposes EoC artifacts as native tools and resources to coding assistants (like Claude Code, Cursor, or custom IDE sidecars).
   * Instead of guessing repository state, the MCP service provides agents with structured tools: e.g., `get_active_adrs()`, `trace_lineage(artifact_id)`, or `query_untested_designs()`.

2. **Enterprise AI Search & Knowledge Bases:**
   * The standardized layout makes it trivial to author connectors and ingestors for enterprise search platforms:
     * **Azure AI Search**
     * **Google Vertex AI Search**
     * **AWS Bedrock Knowledge Bases / OpenSearch**
     * **Vector Databases (Pinecone, Qdrant, Weaviate, pgvector)**
   * **Hybrid Precision Retrieval:** Naive RAG pipelines struggle because raw code files lack intent. In EoC, ingestion pipelines index documents with rich, deterministic metadata filters (e.g., `WHERE phase == 'decision' AND status == 'accepted'`). This allows semantic search to pinpoint the exact governing decision or design contract with zero hallucination.

---

| [❮ Previous: 1.2 Building Blocks](02-building-blocks.md) | [Summary](../SUMMARY.md) | [Next: 2.1 The Philosophy of Journey ❯](../02-lifecycle/01-philosophy-of-journey.md) |
| :--- | :---: | ---: |

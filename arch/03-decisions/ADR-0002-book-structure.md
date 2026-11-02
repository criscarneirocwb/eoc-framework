---
id: ADR-0002
title: EoC Framework Book Navigation Architecture and Chapter-Based Structure
phase: decision
type: adr
status: accepted
created: 2026-11-01
updated: 2026-11-01
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [book-navigation, information-architecture, summary, readme, chapter-structure, documentation, eoc-book]
relations:
  derives_from: ["arch/02-concept/archive/RFC-0004-book-structure.md"]
  governed_by: ["arch/03-decisions/ADR-0001-doc-structure.md"]
  implements: []
  affects: [
    "doc/book/README.md",
    "doc/book/SUMMARY.md",
    "doc/book/01-foundations/",
    "doc/book/02-lifecycle/",
    "doc/book/03-ai-tooling/",
    "doc/book/04-tooling/",
    "README.md"
  ]
---

# ADR-0002: EoC Framework Book Navigation Architecture and Chapter-Based Structure

## 1. Context
* **Background:**
  In [ADR-0001](arch/03-decisions/ADR-0001-doc-structure.md), `doc/book/` was established as the theoretical and philosophical source of truth for the Engineering-as-Code (EoC) methodology, designed to serve as the publishing source for the public EoC Wiki. However, `doc/book/` lacked an internal layout, entry point, and navigational hierarchy.
* **Governing Need:**
  Derived from the business requirements in [PID-0004-BR](arch/01-seed/PID-0004-BR-book-navigation.md) and technical consensus in [RFC-0004](arch/02-concept/archive/RFC-0004-book-structure.md), the framework requires an information architecture that balances human narrative discovery with fast reference indexing, avoids deep filesystem nesting, and automates index maintenance to prevent broken links.

## 2. Decision
We adopt **Option A: The Chapter-Based Dual-Navigation Architecture**, governed by the following core structural rules:

1. **Dual-File Navigation System:**
   * **`doc/book/README.md` (Human-Authored / Editorial):** The narrative landing page and high-level roadmap linked directly from the repository root `README.md`. Explains the core philosophy and introduces the roadmap of the four chapters.
   * **`doc/book/SUMMARY.md` (Automated Structured Index):** The exhaustive, clickable table of contents conforming to the standard GitBook / mdBook / Wiki specification. It is treated strictly as a **machine-generated build artifact** maintained by an **internal repository maintenance utility** (internal script/CI workflow), completely decoupled from the consumer-facing `EoC CLI`.

2. **Formatting & Audience Principle:**
   * Book documents are written in pure, human-facing Markdown without YAML frontmatter boilerplate. AI agent ingestion remains anchored in upstream governance artifacts (`arch/`).

3. **Chapter-Based Filesystem Organization:**
   * **Directory Rule:** Subdirectories exist **only at the Chapter level** directly under `doc/book/`.
   * **Topic Rule:** Each primary topic within a chapter is authored as an independent Markdown file directly inside that chapter's directory.
   * **Subtopic Rule:** Granular subtopics are structured as internal Markdown headings (`###`) within the topic file.

4. **Four Foundational Chapters:**
   * **Chapter 1: Foundations (`doc/book/01-foundations/`):**
     * `01-vision-and-philosophy.md` (Topic 1.1: Vision and philosophy)
     * `02-building-blocks.md` (Topic 1.2: Seeds, Concept, Decisions, Specs, Design)
     * `03-ai-ready.md` (Topic 1.3: Frontmatters, Agent-driven architecture)
   * **Chapter 2: Lifecycle (`doc/book/02-lifecycle/`):**
     * `01-philosophy-of-journey.md` (Topic 2.1: The philosophy of journey)
     * `02-standard-journey.md` (Topic 2.2: Standard invariant & deliverables package)
     * `03-side-journeys.md` (Topic 2.3: Incident workflows & alternative sanctioned paths)
   * **Chapter 3: AI Tooling (`doc/book/03-ai-tooling/`):**
     * `01-agent-first-philosophy.md` (Topic 3.1: Agent-first philosophy & AI-Aided Design)
     * `02-roles.md` (Topic 3.2: Specialized persona roles, starting with the Architect role)
     * `03-tasks.md` (Topic 3.3: Predefined automated agent tasks & workflows)
   * **Chapter 4: Tooling (`doc/book/04-tooling/`):**
     * `01-eoc-cli.md` (Topic 4.1: The primary CLI gateway & entry point)

*(Note: Operational runbooks covering installing, initializing, running, updating, and expanding projects are decoupled from the book and governed by their own dedicated initiatives).*

## 3. Considered Options
1. **Option A (Selected): Chapter-Based Dual-Navigation Architecture:**
   * *Rationale for Selection:* Provides the best balance between human narrative discovery and clickable index lookup, avoids deep folder trees, ensures link integrity via an automated internal generator, and natively maps to public wiki generators.
2. **Option B (Rejected): Flat Numbered Chapter Files:**
   * *Rationale for Discarding:* Placing 15+ numbered files in a single folder lacks thematic chapter cohesion and creates numbering collisions.
3. **Option C (Rejected): Single Monolithic Book.md File:**
   * *Rationale for Discarding:* Causes severe merge conflicts during concurrent contributions and violates modular Docs-as-Code principles.

## 4. Consequences
* **Positive Outcomes:**
  * Clean, predictable filesystem: subdirectories exist only at the chapter level.
  * Zero manual maintenance overhead or broken links in `SUMMARY.md` due to automated generation.
  * Direct 1:1 mapping between `doc/book/` and the published public EoC Wiki.
  * Clear boundary between the theoretical Book and operational Runbooks/Playbooks.
* **Negative Trade-Offs / Operational Liabilities:**
  * Requires building and maintaining an internal repository script/CI check to regenerate `SUMMARY.md`.

## 5. Reversibility & Lifespan
* **Reversibility Level:** Type 2 (Two-way door / Documentation directory convention). Highly stable foundational decision.
* **Review Triggers:** A major wiki publishing technology shift requiring incompatible navigation manifests.

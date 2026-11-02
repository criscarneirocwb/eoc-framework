---
id: RFC-0004
title: EoC Framework Book Navigation Architecture and Thematic Structure
phase: concept
type: rfc
status: proposed
created: 2026-10-29
updated: 2026-10-29
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [book-navigation, information-architecture, summary, readme, documentation-structure, eoc-book]
relations:
  derives_from: ["arch/01-seed/PID-0004-BR-book-navigation.md"]
  governed_by: ["arch/03-decisions/ADR-0001-doc-structure.md"]
  implements: []
  affects: ["arch/03-decisions/ADR-0004-book-structure.md"]
---

# RFC-0004: EoC Framework Book Navigation Architecture and Thematic Structure

## 1. Problem Statement
* **Technical Challenge:**
  In [ADR-0001](arch/03-decisions/ADR-0001-doc-structure.md), the repository established `doc/book/` as the theoretical and philosophical source of truth for the Engineering-as-Code (EoC) methodology, designed to serve as the direct publishing source for the public EoC Wiki. However, `doc/book/` currently lacks an internal layout, entry point, and navigational hierarchy.
  
  Derived from the requirements set forth in [PID-0004-BR](arch/01-seed/PID-0004-BR-book-navigation.md), the framework requires an information architecture that satisfies two distinct reading journeys:
  1. **Narrative Discovery:** Welcoming new human contributors, architects, and engineering leads with high-level conceptual context, core philosophy, and reading roadmaps.
  2. **Structured Reference Indexing:** Enabling returning practitioners to jump directly to specific methodology rules, lifecycle definitions, and artifact specifications.

  Additionally, the organization must be extensible enough to accommodate the complete upcoming development horizon (artifact templates, `.eoc/` runtime contract, global taxonomy, agent skills, tooling, and bootstrapping) without recurring directory restructurings.

---

## 2. Proposed Architecture: Dual-File Navigation & Thematic Partitioning

### 2.1 Dual-File Navigation Paradigm
To resolve the tension between narrative discovery and quick reference indexing, the root of `doc/book/` will feature two complementary navigation anchors:

1. **`doc/book/README.md` (The Narrative Landing & Roadmap):**
   * Acts as the primary entry point linked directly from the repository root `README.md`.
   * Written in warm, accessible prose welcoming the reader to Engineering-as-Code.
   * Summarizes the core philosophy and provides a high-level roadmap explaining what each major thematic Part covers and why it matters.
2. **`doc/book/SUMMARY.md` (Automated Structured Index):**
   * Conforms to the standard mdBook / GitBook / Wiki index format.
   * Houses an exhaustive, hierarchical, clickable table of contents linking directly to all chapters, topic files, and section anchors across the book.
   * **Automation & Maintenance Principle:** `SUMMARY.md` is treated strictly as a **machine-generated build artifact**, avoiding manual link maintenance and preventing broken relative paths.
   * **Internal Project Utility:** It will be generated and synchronized by a dedicated **internal repository maintenance utility** (internal script / CI mechanism) belonging specifically to the `eoc-framework` codebase, completely decoupled from the consumer-facing `EoC CLI`.
   * **CI/CD Synchronization:** Repository CI/CD pipelines will automatically rebuild or verify `SUMMARY.md` whenever markdown files in `doc/book/` are modified.

---

### 2.2 Formatting & Audience Principle: Pure Human-Facing Markdown
* **No Frontmatter Boilerplate:** Unlike governance records under `arch/` (which rely on machine-parsable YAML frontmatter for AI agent traversal), book files under `doc/book/` are authored strictly for human reading and web publishing.
* Documents will be written in standard, clean GitHub-Flavored Markdown without YAML frontmatter, prioritizing typography, readability, diagrams, and clean navigation links.

---

### 2.3 Chapter-Based Structural Architecture

To prevent deep, convoluted filesystem nesting while keeping reading journeys intuitive, the book is organized strictly by **Chapters**:
* **Directory Rule:** Subdirectories exist **only at the Chapter level** directly under `doc/book/` (e.g. `doc/book/01-foundations/`).
* **Topic Rule:** Each primary topic within a chapter is authored as an independent Markdown file directly inside that chapter's directory.
* **Subtopic Rule:** Granular subtopics are structured as internal Markdown headings (`###`) within the topic file, keeping related definitions cohesive and avoiding file proliferation.

---

### 2.4 Detailed Chapter Definitions

#### Chapter 1: Foundations (`doc/book/01-foundations/`)
Grounds the reader in why EoC exists, defines the core architectural primitives, and explains how the framework is natively engineered for autonomous AI agents.

* **Topic 1.1 - Vision and Philosophy (`01-vision-and-philosophy.md`):**
  * Why we created EoC: moving from Docs-as-Code to Engineering-as-Code.
  * Overcoming context drift, unanchored generation, and architectural erosion in AI-driven software development.
* **Topic 1.2 - Building Blocks (`02-building-blocks.md`):**
  * Concepts and definitions over which EoC is built:
    * *1.2.1 - Seeds:* `OC`, `BR`, `PR`, `PD` (the origins and triggers of all initiatives).
    * *1.2.2 - Concept:* `RFC` (solution hypotheses, options debate, and spikes).
    * *1.2.3 - Decisions:* `ADR` (crystallized, immutable architectural decisions).
    * *1.2.4 - Specifications:* `SPEC` (system topologies, cross-component boundaries, and data flows).
    * *1.2.5 - Design:* `SDD` (low-level module design), `TST` (paired test twins), and `schemas/` (machine-readable contracts).
* **Topic 1.3 - AI Ready (`03-ai-ready.md`):**
  * How EoC is designed to run with and by AI:
    * *1.3.1 - Markdown and YAML Frontmatters:* Human-readable prose paired with deterministic graph metadata for efficient agent traversal without context exhaustion.
    * *1.3.2 - Agent-Driven Architecture:* How the framework is consumed, traversed, and enforced by autonomous agents, respecting the hierarchy of truth.

#### Chapter 2: Lifecycle (`doc/book/02-lifecycle/`)
Walks the reader through the procedural journey of how initiatives emerge, evolve through debate, get decided, and materialize into code, tests, and documentation, as well as sanctioned emergency side paths.

* **Topic 2.1 - The Philosophy of Journey (`01-philosophy-of-journey.md`):**
  * How the journey shapes institutional knowledge; why following the deliberate path prevents shortcut-induced drift and ensures the "why" is never lost.
* **Topic 2.2 - The Standard Journey (`02-standard-journey.md`):**
  * The canonical invariant: $\mathbf{Seed} \rightarrow \mathbf{Concept} \rightarrow \mathbf{Decision} \rightarrow \mathbf{Spec} \rightarrow \mathbf{Design} \rightarrow \mathbf{src \mid tst \mid doc}$.
  * *2.2.1 - The Seeds:* Deep dive into how to select the right trigger (`OC`, `BR`, `PR`, `PD`).
  * *2.2.2 - The Concept:* Capturing the evolution of ideas, trade-offs, and tested hypotheses in RFCs for future reflection and preventing re-litigation.
  * *2.2.3 - The Decision:* The immutability principle of ADRs; superseding decisions rather than rewriting history.
  * *2.2.4 - The Specification:* Why a system-level SPEC precedes module design; how 1 SPEC spans multiple components and artifacts.
  * *2.2.5 - The Design:* Focused component twins (`SDD` + `TST`) and machine schemas.
  * *2.2.6 - Build / Test / Document:* The unified deliverable package—code, tests, and documentation delivered together as one verified unit.
* **Topic 2.3 - The Side Journeys (`03-side-journeys.md`):**
  * Why alternative paths will always be needed, and why formalizing and sanctioning them protects framework integrity.
  * *2.3.1 - Incident Workflow:* The emergency break-glass protocol (`OID-IR` + `OID-PM`), the hotfix fast-track, and the upstream seed lock.

#### Chapter 3: AI Tooling (`doc/book/03-ai-tooling/`)
Details the agent-first philosophy and how autonomous AI agents operate as first-class collaborators within the framework, covering specialized persona roles and predefined automated tasks.

* **Topic 3.1 - Agent-First Philosophy (`01-agent-first-philosophy.md`):**
  * How the framework is built for AI-Aided Design (AIAD) from the ground up; treating agents not as glorified auto-completers, but as first-class engineering collaborators that read, propose, and enforce governance.
* **Topic 3.2 - Roles (`02-roles.md`):**
  * The concept of specialized persona roles, boundaries, and how human teams can define or extend them.
  * *3.2.1 - Architect Role:* The architect persona description, responsibilities, trade-off analysis, and guidelines for pair-architecting.
  * *(Future roles such as Developer, Security Reviewer, and QA Engineer will be appended here as they are designed).*
* **Topic 3.3 - Tasks (`03-tasks.md`):**
  * Predefined automated tasks and workflows executed by agents (e.g. pre-commit lineage verification, scaffolding new seeds/RFCs, auditing test twins, synchronizing schemas).
  * *(Content will grow as automated tools, agent tasks, and skills are specified).*

#### Chapter 4: Tooling (`doc/book/04-tooling/`)
Covers the software tooling and utilities developed and distributed alongside the EoC framework to streamline developer workflows and automate governance.

* **Topic 4.1 - EoC CLI (`01-eoc-cli.md`):**
  * The primary command-line gateway for the framework.
  * Command architecture, entry points, configuration flags, and how sub-tools and workflows are invoked through it.
  * *(Future tools—such as linters, scaffolders, and sync utilities—will be added as separate files like `02-....md` over time).*

```text
doc/book/
├── README.md                           # Master Narrative Roadmap & Landing Page
├── SUMMARY.md                          # Structured Clickable Index (TOC)
│
├── 01-foundations/                     # Chapter 1: Foundations
│   ├── 01-vision-and-philosophy.md     # Topic 1.1: Vision & Philosophy
│   ├── 02-building-blocks.md           # Topic 1.2: Building Blocks (Seeds, Concept, Decisions, Specs, Design)
│   └── 03-ai-ready.md                  # Topic 1.3: AI Ready (Frontmatters, Agent Architecture)
│
├── 02-lifecycle/                       # Chapter 2: Lifecycle
│   ├── 01-philosophy-of-journey.md     # Topic 2.1: The Philosophy of Journey
│   ├── 02-standard-journey.md          # Topic 2.2: The Standard Journey (Seeds through Build/Test/Doc)
│   └── 03-side-journeys.md             # Topic 2.3: The Side Journeys (Incident Workflow)
│
├── 03-ai-tooling/                      # Chapter 3: AI Tooling
│   ├── 01-agent-first-philosophy.md    # Topic 3.1: Agent-First Philosophy
│   ├── 02-roles.md                     # Topic 3.2: Roles (Architect Role & future extensions)
│   └── 03-tasks.md                     # Topic 3.3: Tasks (Automated agent tasks & workflows)
│
└── 04-tooling/                         # Chapter 4: Tooling
    └── 01-eoc-cli.md                   # Topic 4.1: EoC CLI (Primary CLI gateway & entry point)
```

---

## 3. Evaluated Approaches & Alternatives

### Option A: Dual Navigation with Chapter-Based Structure (Proposed)
* **Technical Design:** As detailed above. Dual-file navigation (`README.md` for narrative introduction and `SUMMARY.md` for structured TOC), modular subdirectories strictly at the chapter level (Chapters 1–4), individual Markdown files per topic, and pure human-readable Markdown without YAML frontmatter.
* **Pros:**
  * Clean separation of concerns between narrative discovery and rapid reference lookup.
  * Direct 1:1 compatibility with modern documentation site generators (mdBook, GitBook, MkDocs, Docusaurus).
  * Flat, predictable filesystem layout avoiding deep directory nesting.
  * Zero cognitive clutter from YAML frontmatter on human readers.
* **Cons:**
  * Requires maintaining both `README.md` and `SUMMARY.md` when introducing new major sections.

### Option B: Flat Numbered Chapter List
* **Technical Design:** Placing all chapters directly in `doc/book/` with numeric prefixes (e.g., `doc/book/01-philosophy.md`, `02-pipeline.md`, ... `15-bootstrapping.md`).
* **Pros:**
  * Simpler single-level directory structure.
* **Cons:**
  * Poor scalability as topics expand.
  * Lacks chapter-level grouping, making high-level browsing overwhelming.
  * Does not map naturally to multi-tier wiki sidebars.

### Option C: Single Monolithic `Book.md` File
* **Technical Design:** Authoring the entire framework methodology in a single, massive markdown file.
* **Pros:**
  * Everything in one place.
* **Cons:**
  * Severe merge conflicts during concurrent team contributions.
  * Unusable on mobile or web readers due to file length.
  * Violates Docs-as-Code modularity.

---

## 4. Trade-Off Analysis

| Evaluation Criteria | Option A (Chapter-Based Dual-Nav) | Option B (Flat Numbered) | Option C (Monolithic File) |
| :--- | :--- | :--- | :--- |
| **Reading Experience** | **High:** Narrative guide + structured TOC. | **Moderate:** Uncategorized chapter list. | **Low:** Overwhelming wall of text. |
| **Extensibility for Topics**| **High:** 4 chapters cleanly expand via topic files. | **Moderate:** Re-numbering collisions. | **Low:** Massive merge conflict risk. |
| **Wiki / DocSite Compatibility** | **Native:** Compatible with standard tools. | **Moderate:** Manual sidebar configuration. | **Poor:** Single page only. |
| **Maintenance Overhead** | Low / Moderate (dual index files). | Low (single index). | Zero folder structure. |

---

## 5. Implementation & Execution Plan

Upon ADR approval of this proposal:
1. **Scaffold Chapter Directories:**
   * Create the four chapter subdirectories under `doc/book/`: `01-foundations/`, `02-lifecycle/`, `03-ai-tooling/`, and `04-tooling/`.
2. **Author Master Navigation Files & Generator:**
   * Author `doc/book/README.md` containing the narrative introduction and chapter summaries.
   * Provide the initial `doc/book/SUMMARY.md` and establish the internal repository script/utility to automate its continuous generation and CI/CD validation.
3. **Repository Entry Point:**
   * Update the root `README.md` to provide a clear link pointing directly to `doc/book/README.md`.
4. **Incremental Topic Authoring:**
   * Populate topic files incrementally based on existing ratified ADRs (`ADR-0001`) and future accepted decisions.

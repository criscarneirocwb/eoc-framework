# Engineering-as-Code (EoC) Framework: Overview & Agent Context

This document serves as both a human-readable quick-start guide and an authoritative context map for autonomous AI agents navigating this repository. 

---

## 1. Core Philosophy & Objectives
The **Engineering-as-Code (EoC)** framework extends traditional *Docs-as-Code* principles to govern the entire software development lifecycle—from exploratory business discovery and strategic requirements through architectural decisions, test specifications, and module design down to executable source code.

* **Single Source of Truth:** Code implementation (`src/`) and test suites (`tst/`) are strictly bound to and derived from upstream governance artifacts (`arch/`).
* **Machine-Navigable Graph:** Every document uses standardized YAML frontmatter to establish explicit upstream drivers and downstream dependencies, allowing AI agents to traverse the project context deterministically.
* **Test Twins:** Every design document is born alongside an exact numerical test specification twin.

---

## 2. Directory Structure

The project separates internal technical governance (`arch/`), end-user consumption documentation (`doc/`), test source code (`tst/`), and implementation code (`src/`).

```text
[Project root]
|
├── .eoc/                         # Global project metadata for agent ingestion
|   ├── EoC.md                    # Engineering-as-Code general guide
|   ├── taxonomy.yaml             # Domain glossary, component names, system acronyms
|   ├── agents/                   # AI agents rules, instructions, skills, etc.
|   |   ├── context.md            # Initial instructions to the agent
|   |   └── rules.md              # Instructions, tool constraints, traversal guidelines
|   ├── profile/                  # Project-specific layer (git-tracked for the specific repo)
|   |   ├── project.yaml          # The ONLY hard-coded file mapping rules & overrides
|   |   └── ...                   # Any custom markdown rules, security policies, or domain assets
|   └── templates/                # Templates for the artifacts generated in the project
|
├── arch/                         # Project Governance & Architecture Root
|   ├── 01-seed/                  # Living strategic baselines, discovery, and requirements
|   │   ├── PID-0001-OC-*.md      # Opportunity Canvases (exploratory discovery & viability)
|   │   ├── PID-0002-BR-*.md      # Business Requirements Documents (compliance & commercial constraints)
|   │   └── PID-0003-PR-*.md      # Product Requirements Documents (functional scopes & user flows)
|   │
|   ├── 02-concept/               # Collaborative proposals and spike evaluations
|   │   ├── active/               # Concepts and RFCs currently under debate
|   │   │   └── RFC-0002-*.md
|   │   └── archive/              # Resolved RFCs (accepted, rejected, or abandoned)
|   │       └── RFC-0001-*.md
|   │
|   ├── 03-decisions/             # Immutable log of architectural decisions
|   │   └── ADR-0001-*.md          # Architecture Decision Records (ADRs)
|   │
|   ├── 04-specs/                 # Global system architecture and topology
|   │   └── SPEC-0001-*.md         # End-to-end data flows, boundaries, runtime topologies
|   │
|   └── 05-design/                # Low-level component specifications, test twins, and contracts
|       ├── schemas/              # Machine-readable schemas (OpenAPI, JSON Schema, Protobuf)
|       ├── SDD-0001-*.md         # Software Design Documents (prompts, state machines, tools)
|       └── TST-0001-*.md         # Paired Test Specifications (BDD scenarios, eval datasets, verification)
|
├── src/                          # Production Source Code & Implementation
|
├── tst/                          # Executable Test Code
|   ├── unit/                     # Unit test suites mapping to modules
|   ├── functional/               # Functional verification test suites
|   └── integration/              # End-to-end and contract verification tests
|
└── doc/                          # End-User & Operational Documentation
    ├── guides/                   # User help, getting started, and feature walkthroughs
    ├── api-reference/            # External consumer API documentation
    ├── operators-manual/         # Deployment, monitoring, and operational guides
    └── ...                       # Any other documentation related to the product

```

---

## 3. Artifact Types & Naming Conventions

| Phase | Artifact Type | Prefix | Example Filename | Purpose |
| --- | --- | --- | --- | --- |
| `01-seed/` | Opportunity Canvas | `PID-OC` | `PID-0001-OC-ai-inventory.md` | Exploratory discovery & viability |
| `01-seed/` | Business Requirements | `PID-BR` | `PID-0002-BR-gdpr-audit.md` | Compliance & commercial constraints |
| `01-seed/` | Product Requirements | `PID-PR` | `PID-0003-PR-auth-flow.md` | Functional scopes & user journeys |
| `02-concept/` | Request for Comments | `RFC` | `RFC-0001-guardrails.md` | Alternative technical proposals |
| `03-decisions/` | Architecture Decision | `ADR` | `ADR-0001-use-slm.md` | Immutable decision log |
| `04-specs/` | System Specification | `SPEC` | `SPEC-0001-rag-pipeline.md` | High-level system topology |
| `05-design/` | Software Design Doc | `SDD` | `SDD-0004-guardrail.md` | Low-level module architecture |
| `05-design/` | Test Specification | `TST` | `TST-0004-guardrail.md` | Paired BDD scenarios & test harness spec |

---

## 4. Stage Definitions & Governance

### `arch/01-seed/` (Strategic Baselines, Discovery & Requirements)

* **Objective:** Define *why* the initiative exists and establish clear boundaries through three specialized artifact types depending on the triggering event:
1. **Opportunity Canvas (`PID-XXXX-OC-*.md`):** Explores viability, market value, and problem definition for exploratory or greenfield initiatives. Answers: *Should we pursue this?*
2. **Business Requirements Document (`PID-XXXX-BR-*.md`):** Captures corporate financial targets, regulatory compliance mandates, and operational/legal constraints. Answers: *What business guardrails must be met?*
3. **Product Requirements Document (`PID-XXXX-PR-*.md`):** Defines functional scopes, user journeys, user stories, and success metrics for validated features. Answers: *What user experience and capabilities must be delivered?*


* **Lifecycle & Mutability:** Living baseline. Updated when business priorities, compliance mandates, or product scopes pivot.

### `arch/02-concept/` (Proposals & Trade-Off RFCs)

* **Objective:** Explore *what* approaches could solve the strategic problem. Evaluates multiple implementation options, model classes, pipeline architectures, and third-party solutions.
* **Lifecycle & Mutability:** Mutable while open. Moves from `arch/02-concept/active/` to `arch/02-concept/archive/` once debate closes.
* **Key Artifacts:** Requests for Comments (RFCs), Proof-of-Concept (PoC) Spike writeups, Comparative Benchmark Reports.
* **Rule:** Rejected concepts must be preserved in `archive/` alongside reasons for rejection to prevent re-litigating discarded approaches.

### `arch/03-decisions/` (Architecture Decision Records - ADRs)

* **Objective:** Record *which* path was chosen, the rationale, accepted trade-offs, and consequences.
* **Lifecycle & Mutability:** **Strictly immutable (append-only).** Never edit an accepted ADR to reflect a new direction. To change a past decision, author a new ADR (e.g., `ADR-012`) that explicitly supersedes the older record (e.g., `ADR-0003`).
* **Key Artifacts:** Architecture Decision Records (ADRs) derived directly from closed RFCs.

### `arch/04-specs/` (System Specifications)

* **Objective:** Define *how* the end-to-end system topology fits together. Captures high-level service architecture, data pipelines, orchestration frameworks, context/memory tiers, latency budgets, and disaster recovery.
* **Lifecycle & Mutability:** Versioned technical documentation. Changes require updating the document revision and referencing governing ADRs.
* **Key Artifacts:** System Architecture Specifications, Threat Models, Integration Specifications.

### `arch/05-design/` (Software Design Documents, Test Twins & Contracts)

* **Objective:** Define *how* individual modules, agents, workers, or microservices are built and tested. Every design document (`SDD-XXXX`) is born alongside an exact numerical test specification twin (`TST-XXXX`) in the same folder.
* **Lifecycle & Mutability:** Versioned along with the code and test harness implementation in `tst/`.
* **Key Artifacts:** Software Design Documents (SDDs), Test Specifications (TSTs), Pydantic/Protobuf/JSON schemas, OpenAPI specs.

---

## 5. Metadata Schema & Inter-Document Graph

Every document in the repository must start with a standardized YAML frontmatter block. This guarantees deterministic parsing and enables AI agents to traverse upstream drivers and downstream dependencies across the project graph. Note that `01-seed/` documents utilize the `type` field to distinguish between OCs, BRDs, and PRDs.

```yaml
---
id: string                    # Unique document identifier (e.g., OC-0001, BRD-0001, PRD-0001, ADR-0003, SDD-0004, TST-0004)
title: string                 # Concise, descriptive document title
phase: string                 # seed | concept | decision | spec | design | test
type: string | null           # opportunity-canvas | BRD | PRD | RFC | ADR | SDD | TST | SPEC
status: string                # draft | proposed | accepted | rejected | deprecated | superseded
created: YYYY-MM-DD           # Creation date (ISO 8601)
updated: YYYY-MM-DD           # Last modified date (ISO 8601)
authors: [string]             # List of authors or owners
supersedes: string | null     # ID of previous document replaced by this one
superseded_by: string | null  # ID of newer document replacing this one
keywords: [keyword1,keyword2] # List of keywords related to the document for future search
relations:
  derives_from: [string]      # Direct upstream source documents (e.g., SDD-0004 links to TST-0004 and SPEC-0002)
  governed_by: [string]       # Governing decision IDs (e.g., [ADR-0001, ADR-0003])
  implements: [string]        # Functional specifications being realized
  affects: [string]           # Downstream components, specs, or code modules (e.g., src/ and tst/)
---
```

## 6. Key Governance Rules

1. **Hierarchy of Truth:** Accepted decisions (`ADR`) are strictly immutable. Code or designs violating an active ADR are invalid unless superseded by a new ADR.
2. **The Test Twin Rule:** Every `SDD-XXXX` must be accompanied by an exact numerical `TST-XXXX` file under `arch/05-design/` before implementation begins.
3. **Frontmatter Lineage:** All markdown files in `arch/` must include YAML frontmatter populated with `id`, `type`, `status`, and `relations` (`derives_from`, `governed_by`, `implements`, `affects`).
4. **Separation of Concerns:**
* Internal governance and architecture live in `arch/`.
* End-user and operator documentation live in `doc/`.
* Executable code lives in `src/` and `tst/`.

---

## 7. `.eoc/` Control Center & Configuration Layer

The `.eoc/` directory sits at the repository root and acts as the control center for both human contributors and autonomous AI agents. It cleanly separates **reusable global framework assets** from **repository-specific project policies**.

### Directory Layout

```text
.eoc/                         # Global project metadata for agent ingestion
├── EoC.md                    # Engineering-as-Code general guide
├── taxonomy.yaml             # Domain glossary, component names, system acronyms
├── agents/                   # AI agents rules, instructions, skills, etc.
|   ├── context.md            # Initial instructions to the agent
|   └── rules.md              # Instructions, tool constraints, traversal guidelines
├── profile/                  # Project-specific layer (git-tracked for the specific repo)
|   ├── project.yaml          # The ONLY hard-coded file mapping rules & overrides
|   └── ...                   # Any custom markdown rules, security policies, or domain assets
└── templates/                # Templates for the artifacts generated in the project
```

### Component Breakdown

1. **`EoC.md`**: The user-facing and agent-readable overview of the Engineering-as-Code (EoC) methodology deployed in the workspace.
2. **`taxonomy.yaml`**: Standardized domain glossary, component names, and system acronyms ensuring semantic consistency across all project artifacts.
3. **`agents/rules.md`**: Core behavioral constraints and instructions instructing AI agents on how to traverse the document graph and respect the hierarchy of truth.
4. **`templates/`**: The core, immutable engine templates. These remain pristine and generic so they can be reused across entirely different projects without modification.
5. **`profile/`**: The repository-specific extension zone.
* **`profile/project.yaml`**: The single hard-coded configuration file in this layer. It defines project identifiers, compliance tiers, and explicitly maps customizations, rule injections, or template overrides.
* **Custom Additions**: Any auxiliary markdown files, security addendums, or audit requirements referenced by `project.yaml` live organically within this folder or its subdirectories.

### Project-Specific Customization Pattern

To enforce repository-specific requirements (such as strict security checks in RFCs or custom audit requirements in SDDs) without altering the global baseline templates, agents follow this resolution path:

1. Load the pristine base template from `.eoc/templates/`.
2. Read `.eoc/profile/project.yaml` to identify active project profiles, security tiers, and compliance requirements.
3. Fetch any mapped customization overlays from `.eoc/profile/` and inject those requirements into the generation or review lifecycle.
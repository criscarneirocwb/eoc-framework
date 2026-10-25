# Engineering-as-Code (EoC) Framework

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active%20development-orange.svg)](#status)
[![AI-Ready](https://img.shields.io/badge/AI-Ready-brightgreen.svg)](#-ai-native--human-readable)

> **Engineering-as-Code (EoC)** is an open framework and methodology that unifies software engineering, architectural governance, and product lifecycle management into machine-navigable, human-readable repository artifacts.

---

## 📌 Overview

Traditional software projects often suffer from knowledge drift: product ideas, architectural decisions, technical specifications, and implementation code live in disconnected silos (wikis, ticketing tools, chat threads, and code comments).

**Engineering-as-Code (EoC)** bridges this gap by extending *Docs-as-Code* into a complete engineering lifecycle standard. It guides projects from the earliest seed of an idea through collaborative product conception, architectural decision-making, system specifications, detailed component design with paired test twins, down to production source code and executable tests.

EoC is designed as a continuous, cyclical methodology: as software evolves with new market opportunities, business shifts, and operational demands, the lifecycle seamlessly loops back to iterate on governance baselines and downstream code.

---

## 🎯 Key Objectives

The `eoc-framework` project pursues two primary pillars:

### 1. Framework Development & Methodology
- Establish and standardize the EoC lifecycle stages, artifact models, directory conventions, and metadata schemas.
- Continuously mature and modernize the methodology to meet emerging engineering paradigms and organizational scales.
- Provide clear reference patterns, templates, and best practices.

### 2. Framework Tooling
- **Developer Tools:** Command-line utilities and workflows for developers to initialize new projects, scaffold artifacts, validate traceability graphs, and manage framework upgrades.
- **AI Agent Tooling:** Context maps, prompt contracts, and integration hooks (e.g., for Cursor, Claude Code, GitHub Copilot, and custom autonomous agents) to empower AI systems to deterministically navigate, reason across, and contribute to EoC-governed repositories.

---

## 💡 Core Principles

### 👥 Human-Readable & Transparent
All artifacts are plain Markdown and structured YAML. Directories and naming patterns follow an intuitive hierarchy so that any human engineer, product manager, or stakeholder can easily inspect the rationale behind any line of code or architectural choice.

### 🤖 AI-Native by Design
Every document features structured YAML frontmatter establishing explicit upstream drivers (`drives:`) and downstream dependencies (`driven-by:`). This transforms the entire repository into a deterministic knowledge graph that AI agents can traverse to understand context, impact, and constraints without hallucinations.

### 🔄 Traceable Test Twins
Under EoC, software designs and their verification criteria evolve in lockstep. Component specifications (`SDD`) are created alongside their numerical test twins (`TST`), ensuring that testability and contract guarantees precede implementation.

---

## 🏗️ Repository Architecture & Taxonomy

An EoC-compliant repository organizes governance, source code, tests, and documentation into distinct lifecycle tiers:

```text
[Project Root]
├── .eoc/                     # Global EoC governance, templates & agent definitions
│   ├── EoC.md                # Comprehensive framework specification
│   ├── taxonomy.yaml         # Domain terminology and system acronyms
│   ├── agents/               # Universal instructions and rules for AI agents
│   ├── profile/              # Repository-specific profile configuration
│   └── templates/            # Standard templates for all artifact types
│
├── arch/                     # Architecture & Engineering Governance Root
│   ├── 01-seed/              # Strategic baselines, discovery, and requirements
│   │   ├── PID-*-OC-*.md     # Opportunity Canvases (discovery & viability)
│   │   ├── PID-*-BR-*.md     # Business Requirements (constraints & compliance)
│   │   └── PID-*-PR-*.md     # Product Requirements (user flows & functional scope)
│   ├── 02-concept/           # Collaborative technical proposals and RFCs
│   │   ├── active/           # Concepts actively debated
│   │   └── archive/          # Concluded proposals (accepted / rejected)
│   ├── 03-decisions/         # Immutable Architectural Decision Records (ADRs)
│   ├── 04-specs/             # System-level specifications, boundaries & topologies
│   └── 05-design/            # Component designs (SDDs) and paired test twins (TSTs)
│
├── src/                      # Production source code
├── tst/                      # Executable test suites (unit, functional, integration)
└── doc/                      # End-user documentation, guides, and manuals
```

For the complete specification and artifact lifecycle rules, refer to [`.eoc/EoC.md`](file:///D:/criscarneirocwb/eoc-framework/.eoc/EoC.md).

---

## 🛠️ The EoC Lifecycle at a Glance

| Phase | Directory | Artifact Prefix | Purpose |
| :--- | :--- | :--- | :--- |
| **01 Seed** | `arch/01-seed/` | `PID-OC`, `PID-BR`, `PID-PR` | Strategic discovery, business requirements, and product scope |
| **02 Concept** | `arch/02-concept/` | `RFC` | Exploratory proposals and RFC evaluations |
| **03 Decisions** | `arch/03-decisions/` | `ADR` | Immutable log of architectural and technical decisions |
| **04 Specs** | `arch/04-specs/` | `SPEC` | System architecture, runtime topologies, and data flows |
| **05 Design** | `arch/05-design/` | `SDD` / `TST` | Low-level component specifications paired with test specs |
| **Implementation** | `src/` & `tst/` | Source Code | Concrete code implementations and executable test harnesses |

---

## 🐕 Dogfooding

The `eoc-framework` project is developed strictly using the **EoC Framework itself**. 

As we define new lifecycle stages, refine metadata conventions, and build tooling, this repository adapts in real time. We use our own methodology to define its requirements, debate RFCs, record ADRs, and implement the upcoming EoC developer and AI tools.

---

## 🗺️ Roadmap & Current Status

- [x] Initial framework taxonomy and baseline specification ([`.eoc/EoC.md`](.eoc/EoC.md))
- [x] Core artifact templates (`OC`, `BR`, `PR`, `RFC`, `ADR`, `SPEC`, `SDD`, `TST`)
- [x] AI agent context and rules bootstrap (`.eoc/agents/`, `.cursor/`, `.claude/`, `.github/`)
- [ ] EoC CLI developer tooling (scaffolding, graph validation, status)
- [ ] Agent integrations & automated artifact verification
- [ ] Community guides and reference implementations

---

## 🤝 Contributing

We welcome contributions, discussions, and feedback from engineers, architects, and AI practitioners. Please check the concept discussions in [`arch/02-concept/`](arch/02-concept/) or submit an issue/RFC to get involved.

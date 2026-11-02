---
id: PID-0004-BR
title: Business Requirements for EoC Book Navigation and Information Architecture
phase: seed
type: brd
status: accepted
created: 2026-10-29
updated: 2026-11-01
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [business-requirements, book-navigation, information-architecture, user-experience, documentation, seed]
relations:
  derives_from: []
  governed_by: ["arch/03-decisions/ADR-0001-doc-structure.md", "arch/03-decisions/ADR-0002-book-structure.md"]
  implements: []
  affects: ["arch/02-concept/archive/RFC-0004-book-structure.md"]
---

# PID-0004-BR: Business Requirements for EoC Book Navigation and Information Architecture

## 1. Business Objectives & Drivers
* **Framework Adoption & Developer Experience:**
  The Engineering-as-Code (EoC) framework methodology must be easily discoverable, digestible, and navigate-able by human engineering teams, software architects, and tech leads. If the foundational documentation is difficult to browse or lacks a coherent reading journey, practitioners will face high onboarding friction and the framework will fail to achieve adoption.
* **Cost of Inaction:**
  In [ADR-0001](arch/03-decisions/ADR-0001-doc-structure.md), we established `doc/book/` as the theoretical methodology knowledge base and public wiki source of truth. Without a structured entry point and navigational architecture, the book remains a collection of disjointed markdown files, creating cognitive fatigue, obscuring architectural decisions, and impeding community collaboration.

## 2. Operational & Governance Constraints
* **Clean, Human-Optimized Reading Experience:**
  Unlike governance records in `arch/` which require machine-navigable YAML frontmatter for AI agent traversal, the EoC Book is written for human readers. It must be authored in pure, readable Markdown without repetitive frontmatter boilerplate.
* **Dual-Layer Navigability:**
  The information architecture must support two primary reading patterns:
  1. *Narrative Discovery:* New readers seeking an end-to-end understanding with clear section introductions, learning context, and logical concept progression.
  2. *Reference Indexing:* Returning practitioners and architects seeking immediate, direct access to specific methodology rules or operational definitions.
* **Structural Extensibility:**
  The information hierarchy must accommodate the complete upcoming framework development pipeline—including artifact templates, the `.eoc/` runtime contract, global taxonomy, agent skills, automation tooling, and project bootstrapping—without requiring disruptive structural reorganizations as new ADRs are ratified.

## 3. Business Acceptance Criteria & KPIs
* **Unambiguous Entry Point:**
  An explicit, welcoming landing page must be established at the root of `doc/book/`, directly reachable from the repository root `README.md`.
* **Structured Navigation Index:**
  A comprehensive, clickable Table of Contents must be provided that organizes topics into clear, thematic areas.
* **Readiness for Incremental Authoring:**
  The navigation structure must be ready to receive content derived from existing and future accepted ADRs, allowing documentation to evolve incrementally alongside architectural decisions.

## 4. Stakeholders & Approving Authorities
* **Business & Framework Owners:** Maintainers of the EoC framework repository.
* **Impacted Audience:** Engineering organizations, human developers, open-source contributors, and architects adopting the EoC methodology.

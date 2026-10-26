---
id: ADR-0001
title: Knowledge Architecture, Documentation Taxonomy, and Distributable Assets Structure
phase: decision
type: adr
status: accepted
created: 2026-10-25
updated: 2026-10-25
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [documentation, taxonomy, book, playbook, tools, runbook, resources, knowledge-architecture, decision]
relations:
  derives_from: ["arch/02-concept/archive/RFC-0003-doc-structure.md"]
  governed_by: []
  implements: []
  affects: [
    "doc/book/",
    "doc/playbook/",
    "doc/tools/",
    ".eoc/profile/runbook/",
    "res/",
    "README.md",
    ".eoc/taxonomy.yaml"
  ]
---

# ADR-0001: Knowledge Architecture, Documentation Taxonomy, and Distributable Assets Structure

## 1. Context
* **Background:**
  The Engineering-as-Code (EoC) framework develops methodology rules, operational playbooks, software tooling, and distribution assets (templates/schemas). The repository initially used generic placeholder folders under `doc/` (`guides/`, `api-reference/`, `operators-manual/`), which failed to distinguish between theoretical framework rules, practitioner adoption guides, tool references, and internal repository runbooks. Additionally, there was architectural ambiguity between the local dogfooded `.eoc/` engine and the framework assets intended for packaging and distribution to consumer projects.
* **Governing Concept:**
  This decision crystallizes the consensus reached in [RFC-0003](arch/02-concept/archive/RFC-0003-doc-structure.md) (derived from [PID-0003-PD](arch/01-seed/PID-0003-PD-doc-structure.md)).

## 2. Decision
We adopt **Option A: The Four-Tier Knowledge Architecture & Root Distributable Assets Directory (`res/`)**, along with four specialized downstream production scenarios:

1. **Four-Tier Documentation Structure:**
   * **`doc/book/` (EoC Book):** The theoretical and philosophical source of truth for the framework methodology, modularly structured to serve as the direct publishing source for the public EoC Wiki.
   * **`doc/playbook/` (EoC Playbook):** Practical, scenario-driven operational guides for engineers and agents adopting and following EoC.
   * **`doc/tools/` (EoC Tooling):** Reference documentation, installation manuals, CLI syntax, and SDK guides for tools distributed with EoC.
   * **`.eoc/profile/runbook/` (EoC Runbook):** Repository-specific governance and operational policies that control *how this repository operates*, without altering framework definitions.

2. **Decoupled Distributable Assets (`res/`):**
   * A dedicated root directory (`res/`) holds pristine, export-ready distribution assets (e.g., `res/templates/`, `res/schemas/`).
   * `.eoc/` is recognized strictly as the runtime dogfooding engine governing *this* repository, not an export artifact.

3. **Specialized Downstream Production Routes:**
   * Framework Methodology (`OC`) $\rightarrow$ `RFC` $\rightarrow$ `ADR` $\rightarrow$ `doc/book/` (with conditional updates to `doc/playbook/` and `res/`).
   * Playbook Redaction (`BRD`) $\rightarrow$ `RFC` $\rightarrow$ `ADR` $\rightarrow$ `doc/playbook/`.
   * Tooling Development (`PRD`) $\rightarrow$ `RFC` $\rightarrow$ `ADR` $\rightarrow$ `04-specs` $\rightarrow$ `05-design` (`SDD` + `TST`) $\rightarrow$ `src/`, `tst/`, `doc/tools/`.
   * Internal Project Decisions (`PD`) $\rightarrow$ `RFC` $\rightarrow$ `ADR` $\rightarrow$ `.eoc/profile/runbook/`.

## 3. Considered Options
1. **Option A (Selected): Specialized Four-Tier Knowledge Architecture & Dedicated `res/`:**
   * *Rationale for Selection:* Provides clean separation of concerns across different audiences (architects, practitioners, tool users, repository maintainers), removes ambiguity between the local engine (`.eoc/`) and exportable assets (`res/`), and provides a clean foundation for wiki publishing.
2. **Option B (Rejected): Monolithic Docs-as-Code Directory (Status Quo):**
   * *Rationale for Discarding:* Generic folders (`guides/`, `api-reference/`) conflate methodology with practitioner guides, fail to clearly position project-internal runbooks, and confuse local dogfooding templates with distributable packages.

## 4. Consequences
* **Positive Outcomes:**
  * Absolute structural clarity on where each class of knowledge is authored and consumed.
  * Clean isolation of distributable framework templates under `res/`.
  * Deterministic downstream documentation routing for human contributors and automated AI agents.
* **Negative Trade-Offs / Operational Liabilities:**
  * Requires one-time migration to remove deprecated placeholder folders and establish new directories.
  * Authors must consciously categorize documentation updates into the appropriate tier.

## 5. Reversibility & Lifespan
* **Reversibility Level:** Type 2 (Two-way door / Architectural directory convention). Highly stable foundational decision, but directory structures can be aliased or migrated if future ecosystem tooling demands it.
* **Review Triggers:** A major framework version bump (e.g., EoC v2.0) or introduction of an external documentation generator with incompatible directory conventions.

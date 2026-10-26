---
id: PID-0003-PD
title: Project Decision for EoC Framework Documentation Structure
phase: seed
type: project-decision
status: accepted
created: 2026-10-25
updated: 2026-10-25
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [project-decision, documentation-structure, book, playbook, tools, runbook, seed]
relations:
  derives_from: ["arch/00-brainstorm/active/WBD-0002-eoc-framework-doc-structure.md"]
  governed_by: ["arch/03-decisions/ADR-0001-doc-structure.md"]
  implements: []
  affects: ["arch/02-concept/archive/RFC-0003-doc-structure.md"]
---

# PID-0003-PD: Project Decision for EoC Framework Documentation Structure

## 1. Problem & Context
* **Operational Need / Project Governance Challenge:**
  The Engineering-as-Code (EoC) framework repository develops methodology rules, operational playbooks, framework distribution assets (templates/schemas), and software tooling. Currently, the documentation structure is undifferentiated, creating ambiguity about where theoretical guidance, practitioner playbooks, tool references, and internal repository runbooks live.
* **Cost of Inaction:**
  Without an explicit internal decision governing documentation taxonomy and output classes, documentation will become disorganized and fragmented, hindering both external adoption and internal team operations.

## 2. Solution Hypothesis
* **Conceptual Approach:**
  We hypothesize that establishing a formal classification of documentation into four distinct tiers—**EoC Book** (theoretical methodology and rules), **EoC Playbook** (practitioner's operational guides), **EoC Tooling** (user and CLI references), and **EoC Runbook** (internal project operational rules)—alongside an explicit repository resource directory (`res/`) for framework-distributed assets, will provide clear operational structure for both human contributors and autonomous agents.

  This Project Decision (PD) seeds the formal debate and architectural exploration to be conducted in a downstream RFC.
* **Strategic Alignment:**
  Organizing the framework's knowledge architecture directly supports the long-term usability, educational clarity, and maintainability of the EoC ecosystem.

## 3. Success Metrics & Validation Milestones
* **Quantitative Targets:**
  * Clear categorization of all documentation assets into dedicated directories (`doc/book/`, `doc/playbook/`, `doc/tools/`, `.eoc/profile/runbook/`).
  * Explicit definition of the documentation production lifecycles triggered by accepted ADRs.
* **Validation Milestones:**
  * Authoring of a downstream RFC (`RFC-0003-doc-structure`) exploring the directory structures, migration path, and production flows.
  * Formal ratification into an accepted ADR governing the documentation and asset taxonomy of this repository.

## 4. Preliminary Feasibility & Risks
* **Operational Friction:**
  * Ensuring the four-tier structure remains simple to navigate without creating unnecessary silos.
* **Evolutionary Alignment:**
  * Ensuring that changes to the documentation structure align smoothly with the future formal overhaul of `.eoc/taxonomy.yaml`.

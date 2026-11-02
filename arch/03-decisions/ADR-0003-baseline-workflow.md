---
id: ADR-0003
title: Baseline Engineering-as-Code (EoC) Workflow Lifecycle
phase: decision
type: adr
status: accepted
created: 2026-11-02
updated: 2026-11-02
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [workflow, lifecycle, governance, eoc-framework, baseline, macro-pipeline, decision]
relations:
  derives_from: ["arch/02-concept/archive/RFC-0001-workflow.md"]
  governed_by: []
  implements: []
  affects: [
    "arch/01-seed/",
    "arch/02-concept/",
    "arch/03-decisions/",
    "arch/04-specs/",
    "arch/05-design/",
    "src/",
    "tst/",
    "doc/"
  ]
---

# ADR-0003: Baseline Engineering-as-Code (EoC) Workflow Lifecycle

## 1. Context
* **Background:**
  In automated, agentic, and AI-assisted development environments, engineering initiatives frequently suffer from architectural drift, undocumented design choices, and disconnected code/test implementations. Without an explicit, strictly governed progression pipeline, human contributors and autonomous agents invent ad-hoc development flows, bypassing architecture reviews and invalidating the repository's machine-navigable dependency graph.
* **Governing Concept:**
  This decision crystallizes the architectural consensus reached in [RFC-0001](arch/02-concept/archive/RFC-0001-workflow.md) (derived from the initial opportunity canvas [PID-0001-OC](arch/01-seed/PID-0001-OC-workflow.md)).

## 2. Decision
We adopt **Option A: The Strict Invariant Macro-Pipeline with Paired Component Twins & Operational Urgency Triage**, governed by the following core structural rules:

### 1. Invariant Macro Progression ("No Skipping, Early Exit Allowed")
Work progresses through five strict macro-stages:
$$\mathbf{01\text{-}seed} \longrightarrow \mathbf{02\text{-}concept} \longrightarrow \mathbf{03\text{-}decisions} \longrightarrow \mathbf{04\text{-}specs} \longrightarrow \mathbf{05\text{-}design} \longrightarrow \mathbf{Execution\ (src \mid tst \mid doc)}$$

* **Invariance Rule:** No macro stage may ever be skipped. Production code and module designs cannot bypass an RFC, an ADR, or a system SPEC.
* **Early Exit Property:** An initiative may terminate at any stage if deemed unviable, deprioritized, or concluded with an organizational policy that requires no software implementation.

### 2. Phase Responsibilities & Artifact Taxonomy
1. **`arch/01-seed/` (Strategic & Requirements Entry Points):**
   * **`PID-XXXX-OC` (Opportunity Canvas):** Exploratory opportunities, emerging technology viability, market research.
   * **`PID-XXXX-BR` (Business Requirements Document):** Commercial contracts, compliance, industry standards, legal boundaries.
   * **`PID-XXXX-PR` (Product Requirements Document):** Functional capabilities, user journeys, refactoring, feature requests.
   * **`PID-XXXX-PD` (Project Decision):** Internal repository rules, contributor conventions, and documentation taxonomy.
   * *Flexible Entry:* Work may enter directly at any recognized seed type; chained progression (OC $\rightarrow$ BR $\rightarrow$ PR) is optional.
2. **`arch/02-concept/` (Debate & Exploration):**
   * Proposes and debates solutions in Request for Comments (`RFC-XXXX`).
   * Active discussions reside in `arch/02-concept/active/`.
   * Upon reaching consensus (or formal rejection), the RFC is marked `accepted` or `rejected`, frozen, and moved to `arch/02-concept/archive/` to preserve historical institutional memory.
3. **`arch/03-decisions/` (Crystallization & Immutability):**
   * Outcomes are recorded as Architecture Decision Records (`ADR-XXXX`).
   * **ADR Immutability:** ADRs are strictly immutable (append-only). Amending past decisions requires authoring a new RFC and a new ADR that explicitly supersedes the predecessor.
4. **`arch/04-specs/` (System Topology & Boundaries):**
   * A `SPEC-XXXX` outlines end-to-end data flows, service boundaries, cross-component interfaces, and integration blueprints.
   * Acts as the primary trigger for user and operator documentation.
5. **`arch/05-design/` (Component Design & Test Twins):**
   * A single `SPEC` decomposes into $1:M$ components.
   * For **each distinct component**, a Software Design Document (`SDD-XXXX`) is paired with an exact numerical Test Twin (`TST-XXXX`).
   * `SDD` details internal algorithms, data structures, and state machines, feeding `src/`.
   * `TST` defines executable BDD assertions, evaluation benchmarks, and verification harnesses, feeding `tst/`.
6. **Execution (`src/`, `tst/`, `doc/`):**
   * Deliverables are produced as a synchronized atomic triad satisfying the governing SDD and TST twins.

### 3. Defect & Remediation Lifecycle (Operational Urgency Triage)
Post-merge issues and defects do not exist in an ad-hoc silo; they are integrated into repository governance based on operational urgency:
1. **In-Flight vs. Post-Merge Boundary:**
   * CI/CD validation failures during active branch development are iterated in-place within the current task.
   * Any bug, regression, or compliance gap detected in merged/released code constitutes a post-merge issue.
2. **Operational Urgency Triage:**
   * **Critical / Life-Threatening Emergencies (P0 / Outages / Active Breaches):**
     When time is of the essence to protect system availability, security, or data integrity, the issue branches into the **Operational Incident Response Lifecycle** (governed by RFC-0002 / Incident Twins `OID-IR` + `OID-PM`).
   * **Standard (Non-Life-Threatening) Defects:**
     All routine bugs, functional exceptions, regulatory omissions, or performance bottlenecks must be triaged into an explicit Seed (`PID-PR`, `PID-BR`, or `PID-OC`) and traverse the standard macro-pipeline.
3. **The Test Twin Remediation Guarantee:**
   * If a defect bypassed CI/CD into merged code, the test harness was deficient by definition.
   * Remediation mandates that the paired Test Twin (`TST-XXXX`) and automated test in `tst/` must be updated **first** with a failing reproduction assertion before `src/` is patched.

## 3. Consequences & Traceability
* **Positive:**
  * Eliminates architectural drift and rogue code generation by human contributors or autonomous AI agents.
  * Guarantees 100% test-driven specification coverage prior to writing production code.
  * Preserves an unbroken, machine-navigable graph connecting every line of code to an accepted ADR and Seed.
  * Preserves the rationale of discarded alternatives for future maintainers.
* **Trade-Offs & Mitigations:**
  * Introduces governance authoring friction for small or routine changes.
  * *Mitigation:* Lean RFC and ADR authoring conventions are sanctioned for localized changes, while critical operational outages have a dedicated emergency containment fast-track.

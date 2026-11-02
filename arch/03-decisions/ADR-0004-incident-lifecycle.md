---
id: ADR-0004
title: Operational Incident Response Lifecycle and Incident Twins (OID)
phase: decision
type: adr
status: accepted
created: 2026-11-02
updated: 2026-11-02
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [incident-response, emergency-flow, hotfix, post-mortem, oid, governance, runbook, decision]
relations:
  derives_from: ["arch/02-concept/archive/RFC-0002-incident-workflow.md"]
  governed_by: ["arch/03-decisions/ADR-0003-baseline-workflow.md"]
  implements: []
  affects: [
    "arch/99-incidents/",
    "arch/05-design/",
    "src/",
    "tst/",
    ".eoc/profile/runbook/",
    "doc/book/02-lifecycle/03-side-journeys.md"
  ]
---

# ADR-0004: Operational Incident Response Lifecycle and Incident Twins (OID)

## 1. Context
* **Background:**
  The baseline Engineering-as-Code (EoC) workflow ratified in [ADR-0003](arch/03-decisions/ADR-0003-baseline-workflow.md) mandates sequential progression across five macro phases (`01-seed` $\rightarrow$ `02-concept` $\rightarrow$ `03-decisions` $\rightarrow$ `04-specs` $\rightarrow$ `05-design` $\rightarrow$ `Execution`). While this eliminates architectural drift during planned feature delivery and routine defect remediation, enforcing it during critical production outages, active security breaches, or severe data loss risks introduces crippling operational latency. Without a sanctioned emergency fast-track, teams inevitably resort to unauthorized "shadow engineering"—merging out-of-band hotfixes directly into `src/`—which destroys repository graph integrity and causes post-incident learnings to be forgotten.
* **Governing Concept:**
  This decision crystallizes the architectural consensus reached in [RFC-0002](arch/02-concept/archive/RFC-0002-incident-workflow.md) (derived from the opportunity canvas [PID-0002-OC](arch/01-seed/PID-0002-OC-incident-workflow.md)).

## 2. Decision
We adopt **Option A: The Decoupled Incident Twin Model with Structural Upstream Seed Lock**, governed by the following core structural rules:

### 1. Separation of Concerns: The Incident Twin (`OID-XXXX`)
Operational emergencies are decoupled into two distinct, complementary documents located under `arch/99-incidents/`:
* **Incident Report (`OID-XXXX-IR-...md`):**
  * Focuses strictly on **immediate containment and operational stabilization**.
  * Documents incident detection, telemetry anomalies, blast radius, reproduction steps, and the tactical containment plan.
  * Fast-tracks containment execution by directly commissioning emergency Software Design Documents (`SDD-YYYY`) and Test Twins (`TST-YYYY`) without prior RFC/ADR/SPEC cycles.
  * Status progression: `in-progress` $\longrightarrow$ `contained` $\longrightarrow$ `finished`.
* **Post-Mortem (`OID-XXXX-PM-...md`):**
  * Focuses on **systemic analysis, blameless reflection, and root-cause learning**.
  * Initiated once the system reaches a stabilized or contained state.
  * Evaluates underlying structural defects, process breakdowns, and determines whether resolving the root cause warrants broader architectural or product rework.
  * Status progression: `draft` $\longrightarrow$ `under-review` $\longrightarrow$ `approved` $\longrightarrow$ `closed`.

### 2. Decoupled Monotonic Numbering & Many-to-One ($M:1$) Cardinality
* There is no shared monotonic sequence between `OID-XXXX` and `SDD-YYYY` / `TST-YYYY`.
* Software Design Documents (`SDD`) and Test Twins (`TST`) maintain their own global monotonic sequence under `arch/05-design/`.
* A single high-severity incident containment may modify or introduce multiple distinct modules ($1 \text{ OID-IR} \longrightarrow M \text{ (SDD + TST)}$).
* Graph traceability is maintained deterministically through frontmatter metadata (`relations.derives_from: ["arch/99-incidents/active/OID-XXXX-IR-...md"]`).

### 3. The Test Twin Hotfix Requirement
* Emergency velocity cannot excuse unverified code.
* A hotfix code change cannot be merged into `src/` without an accompanying Test Twin (`TST-YYYY`) and executable automated test in `tst/` reproducing the defect and verifying containment.

### 4. The Upstream Seed Lock (Anti-Amnesia Guarantee)
To eliminate the chronic industry issue of abandoned post-mortem action items:
1. An Incident Report (`IR`) **cannot** transition to `finished` until its paired Post-Mortem (`PM`) is formally approved.
2. If the Post-Mortem identifies that resolving the root cause requires systemic architectural, regulatory, or functional rework, the incident twin **cannot be closed or moved from `active/` to `archive/` until the draft of the new Seed (`OC`, `BRD`, or `PRD`) has been created** and linked in frontmatter (`relations.derives_from: [OID-XXXX-PM]`).

### 5. Framework Mechanism vs. Project Runbook Policy
* **Framework Role:** Establishes the filesystem layout (`arch/99-incidents/active|archive/`), frontmatter schemas, state machine transitions, and the immutable archival closure gate.
* **Project Runbook Role:** Business criteria and operational policies are inherently domain-specific and must be defined in the project's operational runbook (`.eoc/profile/runbook/`), including:
  * Qualification criteria: Defining what severity threshold (e.g., P0/P1, data loss, security CVE) authorizes the opening of an `OID-IR`.
  * Authorization roles: Who possesses authority to trigger an emergency bypass.
  * Resolution SLAs: Target turnaround timeframes for containment and post-mortem approval (e.g., PM approved within 48 to 72 hours of containment).

## 3. Consequences & Traceability
* **Positive:**
  * Eliminates unauthorized shadow engineering during production emergencies.
  * Solves "post-mortem amnesia" by enforcing a structural gate between incident closure and upstream seed creation.
  * Preserves unbroken repository graph traceability without introducing latency during outages.
  * Enforces test-driven verification even under emergency pressure.
* **Trade-Offs & Mitigations:**
  * Requires managing two coupled files per incident rather than a single monolithic log.
  * *Mitigation:* Decoupling containment from reflection prevents operational confusion and keeps triage logs focused during active incidents.

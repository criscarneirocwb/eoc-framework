---
id: ADR-0001
title: [Decision Title]
phase: decision
type: adr
status: accepted
created: YYYY-MM-DD
updated: YYYY-MM-DD
authors: ["Authors"]
supersedes: null
superseded_by: null
keywords: [keyword1,keyword2]
relations:
  derives_from: ["RFC-XXXX"]
  governed_by: []
  implements: []
  affects: ["SPEC-0001", "SDD-0001"]
---

# ADR-XXXX: [Decision Title]

## 1. Context
* **Background:** Summarize the technical challenge and requirements that led to this decision, referencing the originating RFC.
* **Constraints:** Key performance budgets, security boundaries, or operational limitations influencing the choice.

## 2. Decision
* **Chosen Path:** State clearly and concisely what architecture, pattern, library, or design approach is being adopted.
* **Rationale:** Explain *why* this option was selected over alternatives based on the trade-off analysis.

## 3. Considered Options
1. **[Option A - Selected]:** Brief summary of why it won.
2. **[Option B - Rejected]:** Brief summary of why it was discarded (e.g., failed performance SLAs or excessive operational complexity).

## 4. Consequences
* **Positive Outcomes:** Architectural benefits, developer experience improvements, or risk mitigations.
* **Negative Trade-Offs / Liabilities:** Technical debt accepted, operational maintenance burden, or future migration costs.

## 5. Reversibility & Lifespan
* **Reversibility Level:** Type 1 (One-way door / extremely difficult to reverse) or Type 2 (Two-way door / easily refactored or replaced behind an abstraction).
* **Review Triggers:** Conditions or milestones that would prompt re-evaluating this decision.
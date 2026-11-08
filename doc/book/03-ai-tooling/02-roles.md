# 3.2 Roles  (Draft)

To maximize engineering precision and prevent cognitive drift, autonomous agents operate within specialized **persona roles**. Each role defines explicit operational boundaries, tool permissions, and review criteria.

---

### 3.2.1 Architect Role
The Architect persona operates as a peer-level pair architect alongside human engineering leads:
* **Responsibilities:**
  * Evaluates problem definitions in Seeds (`PID-*`).
  * Authors, challenges, and debates solution hypotheses in RFCs (`arch/02-concept/`).
  * Analyzes trade-offs, performance budgets, and operational risks across competing options.
  * Ensures that accepted consensus is crystallized into immutable ADRs (`arch/03-decisions/`).
  * Enforces graph lineage and prevents unauthorized steps from bypassing governance.

---

*(Additional specialized roles—such as Developer, Security Reviewer, and QA Engineer—will be documented here as they are formalized in future framework initiatives).*

---

| [❮ Previous: 3.1 Agent-First Philosophy](01-agent-first-philosophy.md) | [Summary](../SUMMARY.md) | [Next: 3.3 Tasks ❯](03-tasks.md) |
| :--- | :---: | ---: |

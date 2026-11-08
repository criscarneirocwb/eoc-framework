# 3.1 Agent-First Philosophy (Draft)

In Engineering-as-Code, AI agents are not treated as secondary code auto-completers or external chat bots. The framework is designed from the ground up for **AI-Aided Design (AIAD)**.

## Core Premises of Agent-First Engineering

1. **Autonomous Knowledge Navigation:** Agents possess the tools and structured rules needed to traverse upstream drivers (`derives_from`) and downstream impacts (`affects`) across the repository deterministically.
2. **Deterministic Context Boundaries:** Instead of dumping an entire repository into an LLM context window, agents parse `.eoc/taxonomy.yaml` and frontmatter headers, retrieving only the precise context required for their active role.
3. **Rigorous Guardrails:** Agents respect the immutable hierarchy of truth: they cannot generate code that violates an active ADR, and they cannot commit implementation changes without test twins.

---

| [❮ Previous: 2.3 The Side Journeys](../02-lifecycle/03-side-journeys.md) | [Summary](../SUMMARY.md) | [Next: 3.2 Roles ❯](02-roles.md) |
| :--- | :---: | ---: |

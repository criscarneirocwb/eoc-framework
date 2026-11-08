# 4.1 EoC CLI (Draft)

The **EoC CLI** is the primary command-line gateway distributed alongside the framework, enabling human engineers and automated pipelines to interact with and enforce the EoC lifecycle.

---

## Core Command Domains

* **`eoc init`:** Bootstraps an existing or greenfield repository with the EoC runtime environment (`.eoc/`), default profiles, and pristine templates.
* **`eoc new <artifact>`:** Interactively scaffolds a schema-compliant seed (`OC`, `BR`, `PR`, `PD`), RFC, ADR, SPEC, SDD, or TST twin, pre-populating metadata and relations.
* **`eoc validate`:** Performs deterministic graph linting across the repository, verifying frontmatter schemas, checking for broken relative links, and auditing test twin coverage.
* **`eoc status`:** Provides a high-level visual dashboard of all in-flight initiatives, active RFC debates, approved ADRs, and pending implementations.

*(As the tooling suite matures through dedicated PRD and RFC tracks, detailed CLI syntax, installation guides, and SDK references will be expanded here).*

---

| [❮ Previous: 3.3 Tasks](../03-ai-tooling/03-tasks.md) | [Summary](../SUMMARY.md) | [The EoC Book ❯](../README.md) |
| :--- | :---: | ---: |

# 3.3 Tasks (Draft)

Beyond open-ended conversational collaboration, agents execute predefined, automated engineering tasks designed to maintain repository hygiene and verify framework invariants.

---

## Predefined Automated Tasks

* **Lineage & Dependency Audit:** Verifies that every implementation PR modifying `src/` or `tst/` has a complete upstream chain traversing through `arch/05-design` back to an accepted `ADR` and `Seed`.
* **Test Twin Verification:** Scans `arch/05-design/` to ensure every Software Design Document (`SDD-XXXX`) has an exact numerical Test Specification Twin (`TST-XXXX`) and corresponding automated test suite in `tst/`.
* **Artifact Scaffolding:** Generates valid, schema-compliant templates for new initiatives based on active project profiles.
* **Navigation Synchronization:** Automates the regeneration of `doc/book/SUMMARY.md` from the filesystem tree, ensuring 100% link integrity.

*(Additional automated tasks and agent skills will be documented as the framework automation tooling expands).*

---

| [❮ Previous: 3.2 Roles](02-roles.md) | [Summary](../SUMMARY.md) | [Next: 4.1 EoC CLI ❯](../04-tooling/01-eoc-cli.md) |
| :--- | :---: | ---: |

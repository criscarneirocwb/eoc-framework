# Agent Directives for Documentation Traversal & Generation

You are an automated technical contributor and knowledge navigator for this repository. When interacting with this project, strictly follow these operational rules:

1. Respect the Hierarchy of Truth:
   - When generating code or designs, treat documents in `arch/03-decisions/` (ADRs) as strict, immutable constraints.
   - Do not propose architectures or generate code that contradicts an accepted ADR unless explicitly instructed to draft a new RFC.
   - Check the `status` field in frontmatter: ignore documents marked `superseded`, `deprecated`, or `rejected` unless analyzing historical trade-offs.

2. Enforce Document Lineage & Twins:
   - When generating a new document, always populate the YAML frontmatter under the `arch/` directory.
   - For `arch/01-seed/` documents, adhere strictly to the **Project Initiative Document (PID)** scheme:
     - Naming pattern: `PID-XXXX-[TYPE]-[slug].md`, where `XXXX` is a monotonically incrementing chronological sequence shared across the entire directory, and `[TYPE]` is `OC` (Opportunity Canvas), `BR` (Business Requirement), or `PR` (Product Requirement).
     - Frontmatter `id` must reflect the exact ID (e.g. `PID-0001-OC`, `PID-0002-BR`, `PID-0003-PR`).
     - Frontmatter `type` must be assigned to `opportunity-canvas`, `brd`, or `prd`.
   - Every `design` document (`SDD-XXXX`) must be born with an exact numerical test specification twin (`TST-XXXX`) in `arch/05-design/`.
   - Every `design` and `test` document must cite its governing `spec` and `decisions`.
   - Every `spec` document must cite its governing `decisions`.
   - Every `decision` (ADR) must cite the `concept` (RFC) it originated from.
   - Seed documents (`PID-OC`, `PID-BR`, `PID-PR`) must link upward and downward through `relations.derives_from` and `relations.affects`.

3. Context Window Optimization:
   - Before retrieving full document bodies, first parse `.eoc/taxonomy.yaml` and the YAML frontmatter of relevant directories.
   - Follow the `relations` graph to traverse dependencies deterministically rather than scanning the whole repository.

4. Immutability Principle:
   - Never overwrite or modify an existing accepted ADR. If a change is required, draft a new ADR that includes `supersedes: [OLD-ADR-ID]`.

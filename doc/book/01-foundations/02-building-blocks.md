# 1.2 Building Blocks

Engineering-as-Code is founded upon five primary architectural primitives that structure how initiatives originate, debate options, lock decisions, specify systems, and design modules.

---

### 1.2.1 Seeds

Every initiative begins with an explicit Seed document under `arch/01-seed/`. Seeds follow a unified, monotonically incrementing sequence designated as **Project Initiative Documents (PID)** using the pattern `PID-XXXX-[TYPE]-[slug].md`.

The framework recognizes four specialized seed types based on the triggering event:
* **Opportunity Canvas (`PID-XXXX-OC`):** Triggered by external market opportunities or emerging technology trends. Answers: *Should we pursue this, and what is the potential value?*
* **Business Requirements Document (`PID-XXXX-BR`):** Triggered by industry regulations, legal mandates, or commercial constraints. Answers: *What business guardrails must be respected?*
* **Product Requirements Document (`PID-XXXX-PR`):** Triggered by product needs, user journeys, deprecation cycles, or feature requests. Answers: *What functional capabilities must be delivered?*
* **Project Decision (`PID-XXXX-PD`):** Triggered by internal repository operational rules, governance policies, or documentation taxonomy. Answers: *What internal project processes must govern this repository?*

#### The Institutional Memory of Seeds
Crucially, seeds are not ephemeral backlog tickets that vanish once triaged. **Even rejected or deprioritized seeds remain permanently committed in `arch/01-seed/` with their terminal status (`rejected` or `deprecated`) and explicit rationale.** This guarantees that future human contributors and autonomous AI agents have immediate institutional memory of what initiatives were already explored, evaluated, and discarded, preventing teams from endlessly re-litigating unviable ideas.

---

### 1.2.2 Concept

When a seed warrants technical exploration, it enters `arch/02-concept/` as a **Request for Comments (`RFC-XXXX`)**. The RFC is the collaborative arena where competing technical hypotheses, architectural trade-offs, and experimental spikes are rigorously evaluated.

While debates are ongoing, the RFC resides in `arch/02-concept/active/`. Once community or agent consensus is reached (or when an approach is abandoned), the document is updated and moved to `arch/02-concept/archive/`, where it becomes permanently frozen.

#### Answering "Why Did We Choose Y Instead of X?"
The greatest value of an RFC is not just validating the winning idea—it is preserving the **historical context of the debate**. 

Months or years into a project's lifecycle, new engineers and AI agents inevitably ask:
* *"Why did we choose protocol Y instead of X?"*
* *"Did anyone evaluate database Z before writing custom storage?"*
* *"What were the performance trade-offs or constraints that ruled out the simpler alternative?"*

Without an RFC, teams only see the final code and often assume earlier developers were incompetent or made arbitrary choices. An archived RFC provides the definitive time-capsule: it documents the alternative options considered, the benchmark spikes, the pros and cons tables, and the community discussion that shaped the decision. It turns tribal knowledge into searchable, machine-navigable repository history.

---

### 1.2.3 Decisions

When consensus is reached on an RFC, the architectural commitment is registered as an **Architecture Decision Record (`ADR-XXXX`)** under `arch/03-decisions/`.

#### The Clean, Crystallized Source of Truth
While the RFC captures the rich debate history, benchmark spikes, and discarded hypotheses, the **ADR is the clean source of the final decision**, free from conversational noise, exploratory dead-ends, and preliminary speculation. It represents crystallized commitment: an unambiguous, authoritative statement of *what* is being adopted, *why* it won, and *what consequences* are accepted.

#### Why ADRs Are Strictly Immutable
The immutability principle is not an arbitrary constraint—it is the mechanism that preserves the **architectural timeline**:
* **Append-Only History:** An accepted ADR can never be edited in place to reflect a new direction.
* **The Superseding Trail:** When technological demands, scaling requirements, or business priorities shift, the team authors a new ADR (e.g., `ADR-0012`) that explicitly declares `supersedes: [ADR-0003]`.
* **Tracing Product Evolution:** By keeping past decisions intact and linking newer decisions chronologically, human engineers and autonomous agents can follow an unbroken audit trail. This reveals not only what the system does today, but exactly how and why its behavior, patterns, and constraints evolved over time. Rewriting a past ADR would falsify history and destroy that vital evolutionary trail.

---

### 1.2.4 Specifications

When an architectural decision involves software implementation, it cannot immediately be translated into individual code modules. An ADR declares *what* strategy or pattern was chosen, but executing that choice almost always impacts multiple distinct components across the software architecture.

System-level architecture and cross-cutting integration plans are formalized under `arch/04-specs/` via a **System Specification (`SPEC-XXXX`)**.

#### The Master Implementation Plan
A `SPEC` acts as the **master blueprint** for realizing an ADR:
* **The Integration View:** It defines how distinct services, subsystems, and libraries communicate to achieve the desired outcome—specifying end-to-end data flows, network protocols, latency budgets, and security boundaries.
* **Cross-Cutting Orchestration:** A single architectural decision rarely lives in one component. For example, adopting a new authentication protocol might require simultaneous interventions in the API gateway, database user schemas, and client-side token refresh workers. The SPEC orchestrates this entire multi-component topology in one place.
* **Bridge from Strategy to Modules:** The SPEC decomposes the macro decision into discrete, component-level intervention boundaries. It establishes the master plan that answers: *"Which components must change, what are their interface contracts, and how do they integrate together?"*

Without a SPEC, human engineers and autonomous agents are forced to jump straight from high-level ADRs into localized module files. This results in fragmented implementations where individual pieces compile in isolation but fail when integrated into the larger runtime system.

---

### 1.2.5 Design

Once the system-level master plan is established in a `SPEC`, the architecture is decomposed into concrete, module-level specifications under `arch/05-design/`.

#### 1-to-Many Decomposition: From SPEC to Multiple SDDs
A single `SPEC` frequently spins off multiple independent **Software Design Documents (`SDD-XXXX`)**. For example, a system specification introducing asynchronous event streaming might yield:
* `SDD-0010`: The event publisher module in the API service.
* `SDD-0011`: The message broker queue consumer and retry worker.
* `SDD-0012`: The persistence handler updating the read replica.

Each SDD isolates the internal mechanics of a single component—detailing internal algorithms, state machines, memory considerations, and error handling.

#### The Test Twin Axiom & Test-Driven Development (TDD)
EoC deeply embraces **Test-Driven Development (TDD)** and formalizes it through the **Test Twin Axiom**:
* **Numerical Pairing:** Every Software Design Document (`SDD-XXXX`) is born alongside an exact numerical **Test Specification Twin (`TST-XXXX`)** in `arch/05-design/`.
* **Verification Precedes Code:** The `TST` document defines the verifiable acceptance criteria, BDD scenarios (*Given/When/Then*), edge cases, and failure modes *before* a single line of production code is written.
* **Traceable Testing:** Because the design document and test specification share the exact same numeric identifier, the relationship between a component's architectural intent and its verification harness is unambiguous, permanent, and auditable.

#### Guiding Autonomous AI Agents Without Guesswork
In traditional AI-assisted coding, developers prompt an agent with vague instructions, forcing the model to guess business logic, skip edge cases, or write superficial tests. Under EoC, the SDD and TST twin act as deterministic guardrails:
1. **Targeted Implementation:** The `SDD` directs the AI agent on *how* to write production code in `src/`, specifying classes, internal methods, and algorithms.
2. **Automated Verification:** The `TST` directs the AI agent on *how* to construct the automated test suite in `tst/`, ensuring tests validate real contract invariants rather than shallow happy paths.
3. **Closing the Loop:** An agent cannot declare work complete until the automated test suite in `tst/` (derived from the TST twin) runs green against the implementation in `src/` (derived from the SDD).

#### Machine-Readable Schemas: Anti-Hallucination Guardrails
Alongside human-readable design specifications, the design tier maintains machine-readable contracts under `arch/05-design/schemas/` (OpenAPI, JSON Schema, Protobuf, Pydantic):
* **Deterministic Interface Signatures:** Rather than letting an AI agent hallucinate method parameters, payload envelopes, or missing fields, the schema acts as a strict, mathematically verifiable contract.
* **Zero Guesswork:** When generating client SDKs, API serializers, or database entities, the agent derives types and signatures directly from the schema, eliminating interface mismatches between communicating services.

---

| [❮ Previous: 1.1 Vision and Philosophy](01-vision-and-philosophy.md) | [Summary](../SUMMARY.md) | [Next: 1.3 AI Ready ❯](03-ai-ready.md) |
| :--- | :---: | ---: |

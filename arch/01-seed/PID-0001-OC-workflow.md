---
id: PID-0001-OC
title: Opportunity for an Engineering-as-Code (EoC) Baseline Workflow
phase: seed
type: opportunity-canvas
status: accepted
created: 2026-10-24
updated: 2026-10-25
authors: ["criscarneirocwb"]
supersedes: null
superseded_by: null
keywords: [opportunity-canvas, workflow, lifecycle, eoc-framework, governance, seed]
relations:
  derives_from: []
  governed_by: []
  implements: []
  affects: [arch/02-concept/active/RFC-0001-workflow.md]
---

# PID-0001-OC: Opportunity for an Engineering-as-Code (EoC) Baseline Workflow

## 1. Problem & Context
* **User Pain Point / Market Opportunity:**
  In AI-assisted software engineering, agents and human contributors often jump prematurely into implementation without an established lifecycle. This leads to untracked decisions, architectural drift, fragmented documentation, and unanchored code. To unlock the full potential of Engineering-as-Code (EoC), we need a standardized baseline workflow that clearly establishes how work originates, progresses through governance phases, and translates into production assets.
* **Cost of Inaction:**
  Without an agreed-upon baseline workflow, contributors and autonomous agents will invent ad-hoc processes. This undermines the deterministic machine-traversal of the repository, breaks document traceability, and produces technical debt before the framework even takes off.

## 2. Solution Hypothesis
* **Conceptual Approach:**
  We hypothesize that establishing a lean, end-to-end baseline workflow—defining clear transition stages from strategic intent down to implementation, along with the purpose of artifacts generated at each stage (including exploratory Opportunity Canvases, Business Requirements, Product Requirements, and Project Decisions for internal operational governance)—will provide the essential structure needed for both humans and autonomous agents to collaborate effectively.
  
* **Strategic Alignment:**
  Defining the baseline workflow is foundational to the EoC mission. It sets the operational standard for all subsequent development, ensuring every downstream initiative follows a consistent, verifiable path.

## 3. Success Metrics & KPIs
* **Quantitative Targets:**
  * Agreement on a core set of phases and artifact roles that cover the standard development lifecycle (including the addition of the Project Decision seed for repository operations).
  * A description of the mainstream workflow with its stages and expected artifacts.
* **Validation Milestones:**
  * Authoring and submission of `RFC-0001-workflow-lifecycle` exploring the workflow mechanisms and transitions.
  * Reaching team/agent consensus to promote the workflow design to an accepted ADR.
  * Due to the nature of this opportunity, no artifacts beyond the ADR are expected.

## 4. Preliminary Feasibility & Risks
* **Technological Uncertainty:**
  * Determining the right balance between governance rigor and developer velocity to prevent the workflow from feeling overly bureaucratic.
  * Ensuring the lifecycle structure is easily parsed, understood, and enforced by LLM-based autonomous agents.
* **Business / Operational Risks:**
  * Risk of overcomplicating the baseline flow by attempting to solve every edge-case scenario upfront, rather than addressing specific exceptions in future proposals.

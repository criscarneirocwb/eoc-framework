---
description: Project initialization context, document map, and guidelines
trigger: always_on
---

# Agent project context bootstrap

## Summary
This project follows the Engineering-as-Code (EoC) framework.
Agents should read the framework context definition and initialization files described below to get the framework rules and definitions.

## Project rules and taxonomy
Agents should look into the `.eoc` directory for rules, taxonomy and templates used in this project.

* `.eoc/EoC.md` clarifies the "Engineering-as-Code (EoC)" framework used in this project.
* `.eoc/agents/rules.md` defines the rules to be followed for the project organization and its workflow.
* `.eoc/taxonomy.yaml` describes the project taxonomy.
* `.eoc/templates` directory with the template for the documents like OCs, BRDs, PRDs, RFCs, SDDs, etc.
* `.eoc/profile/project.yaml` has the customizations and specifics for this project, indicating custom rules and overrides.

## Project goals and vision
Agents should read the `README.md` at the project root folder to get specific information about the project and its goals.
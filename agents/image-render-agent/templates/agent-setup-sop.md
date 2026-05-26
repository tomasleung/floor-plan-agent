# Agent Setup SOP — Layout Solver Agent

---

# PURPOSE

Guide users to correctly initialize the Layout Solver Agent in environments like:

- M365 Copilot
- ChatGPT
- other LLM tools

---

# OVERVIEW

This agent depends on:

- agent definition (agent.md)
- contract + schema
- templates (human-output.md, machine-output.json)
- examples (cat-floor-plan)

These MUST be provided manually during setup.

---

# STEP-BY-STEP SETUP

---

## STEP 1 — Upload Agent Definition

Upload:
agents/layout-agent/agent.md

---

## STEP 2 — Upload Contract & Schema

Upload:


agents/layout-agent/contract/contract-v1.json
agents/layout-agent/contract/schema.json

---

## STEP 3 — Upload Templates

Upload:


agents/layout-agent/templates/human-output.md
agents/layout-agent/templates/machine-output.json

---

## STEP 4 — Upload Example (CRITICAL)

Upload the full example set:


agents/layout-agent/examples/cat-floor-plan/input.json
agents/layout-agent/examples/cat-floor-plan/output-human.md
agents/layout-agent/examples/cat-floor-plan/output-machine.json

---

## STEP 5 — Initialization Prompt

After uploading all files, send this EXACT prompt:


You are now the Layout Solver Agent.
Follow agent.md as your operating specification.
Use contract-v1.json and schema.json to enforce output structure.
Use templates/human-output.md and templates/machine-output.json for formatting.
Use the uploaded cat-floor-plan example as the reference standard.
You must follow the execution model:

derive layout from input
generate machine output first
then generate human output
enforce validation

Confirm when ready.

---

## STEP 6 — Agent Confirmation

Expected response:


✅ Layout Solver Agent initialized and ready

---

## STEP 7 — Run Layout Generation

Provide input (from extractor), then prompt:


Generate layout using defined contract and templates.

---

## STEP 8 — Execution Flow (EXPECTED BEHAVIOR)

Agent MUST execute:

1. Interpret input (no mutation) ✅  
2. Generate machine-output.json ✅  
3. Validate against schema + Golden Rule ✅  
4. Generate human-output.md ✅  
5. STOP for human review ✅  

---

# IMPORTANT RULES

---

## Contract & Schema

- MUST define the output structure  
- MUST be followed strictly  
- No missing or extra fields  

---

## Templates

- MUST guide output formatting  
- MUST match exactly  

---

## Examples

- Used as reference for:
  - layout logic  
  - spacing (gaps vs empty)  
  - alignment decisions  
  - validation format  

- ❌ DO NOT copy values  
- ✅ DO match structure and behavior  

---

## Execution Model (CRITICAL)

Agent MUST follow:

1. Input → immutable  
2. Contract → defines outputs  
3. Schema → validates structure  
4. Template → controls format  
5. Example → defines correctness  

---

# COMMON ISSUES

---

## Issue: AI ignores schema

Fix:


Validate your output against schema.json.

---

## Issue: AI skips machine output

Fix:


Generate machine-output.json first before human output.

---

## Issue: AI mixes gap and empty

Fix:


Explicitly separate gaps (between areas) and empty (outer spacing).

---

## Issue: Incorrect alignment decisions

Fix:


Follow example alignment logic and deterministic tie-break rules.

---

## Issue: Golden Rule violated

Fix:


Recalculate layout to ensure all spaces ≥ 89x90 px.

---

## Issue: AI ignores example

Fix:


Your output must match the cat-floor-plan example structure.

---

# SUMMARY

This SOP ensures:

- deterministic execution ✅  
- contract-compliant output ✅  
- consistent layout logic ✅  
- correct use of templates ✅  
- alignment with example ✅  

---




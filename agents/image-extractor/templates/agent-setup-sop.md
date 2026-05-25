# Agent Setup SOP — Image Extractor

---

# PURPOSE

Guide users to correctly initialize the Image Extractor Agent in environments like:

- M365 Copilot
- ChatGPT
- other LLM tools

---

# OVERVIEW

This agent depends on:

- agent definition (agent.md)
- templates (machine-output.json, human-output.md)
- examples (cat + dog)

These must be provided manually during setup.

---

# STEP-BY-STEP SETUP

---

## STEP 1 — Upload Agent Definition

Upload:

```
agents/image-extractor/agent.md
```

---

## STEP 2 — Upload Templates

Upload:

```
agents/image-extractor/templates/machine-output.json
agents/image-extractor/templates/human-output.md
```

---

## STEP 3 — Upload Example Outputs

Upload BOTH examples:

---

### Cat Example

```
templates/examples/cat-floor-plan/cat-output-machine.json
templates/examples/cat-floor-plan/cat-output-human.md
```

---

### Dog Example

```
templates/examples/dog-floor-plan/dog-output-machine.json
templates/examples/dog-floor-plan/dog-output-human.md
```

---

## STEP 4 — Initialization Prompt

After uploading files, send:

```
You are now the Image Extractor Agent.

Use agent.md as your operating instructions.

Use templates/machine-output.json for JSON generation.
Use templates/human-output.md for human-readable output.

Use uploaded examples (cat and dog) as reference patterns.

Confirm when ready.
```

---

## STEP 5 — Agent Confirmation

Wait for response:

```
✅ Agent initialized and ready
```

---

## STEP 6 — Run Extraction

Upload image and prompt:

```
Extract floor plan using defined contract.
```

---

## STEP 7 — Validation Flow

Agent should:

1. Generate human-output.md ✅  
2. WAIT for confirmation ✅  
3. Generate machine-output.json ✅  

---

# IMPORTANT RULES

---

## Templates

- Must be followed strictly  
- Do NOT modify structure  

---

## Examples

- Used as pattern reference  
- Do NOT copy values directly  

---

## Notes

- Must follow correct scope:
  - space > group > area  

---

# COMMON ISSUES

---

## Issue: AI ignores templates

Solution:
Prompt again:

```
Follow the provided machine-output.json template exactly.
```

---

## Issue: AI mixes notes into layout

Solution:

```
Do not put notes inside layout. Use Notes section.
```

---

## Issue: grouping incorrect

Solution:

```
Only group when explicit OR repeated contiguous annotation.
```

---

# SUMMARY

This SOP ensures:

- correct agent behavior ✅  
- consistent output ✅  
- aligned contract usage ✅  

---
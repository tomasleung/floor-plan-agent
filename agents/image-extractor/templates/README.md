# Templates

This folder contains the **output templates used by the Image Extractor Agent**.

Templates guide the AI in generating structured output, but they are **not the data contract**.

---

## Scope

This template set supports the **Extraction Contract (WHAT layer)**.

The system includes multiple stages:

- Extraction → data structure  
- Layout → geometry and positioning  
- Render → visual output  

These templates are used ONLY at the **Extraction stage**.

---

## TL;DR

- templates = guide AI output ✅  
- contracts = define structure ✅  
- schema = validates output ✅  
- templates must follow contract ✅  

---

## Purpose

Templates define:

- how output should be formatted  
- how information is presented  
- how the AI structures its response  

They ensure **consistent and predictable responses** from the agent.

---

## Types of Templates

This folder includes two template types:

---

### 1. Human Output Template

```
human-output.md
```

#### Purpose

Provides a **readable summary** of the extracted floor plan.

#### Audience

- Humans (review / validation)  
- Analysts  
- Stakeholders  

#### Characteristics

- Easy to read ✅  
- Structured but flexible ✅  
- Designed for clarity ✅  
- Not used by other agents ❌  

#### Example

```
# FLOOR PLAN EXTRACTION

## Summary
- Total Areas: 1

## Area 1 — Dog Kennels (All ISO)

Grid:
- Rows: 1
- Columns: 11

Spaces:
1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11

Groups:
1–4 (Large/Public View)
```

---

### 2. Machine Output Template

```
machine-output.json
```

#### Purpose

Guides the AI to produce structured JSON output that matches the data contract.

#### Audience

- AI agents  
- System pipeline  

#### Characteristics

- Structured format ✅  
- Uses placeholders (e.g. `{{area_id}}`) ✅  
- Prompt-friendly ✅  
- Validated against schema after generation ✅  

---

## IMPORTANT DISTINCTION — TEMPLATE vs CONTRACT

Templates are **not the source of truth**.

```
templates/   → HOW output is generated  
contracts/   → WHAT output must look like  
schema.json  → validates correctness  
```

---

### Key Differences

| Component | Role | Enforced | Audience |
|----------|------|----------|----------|
| human-output.md | Presentation | ❌ No | Human |
| machine-output.json | AI guidance | ❌ No | AI |
| schema.json | Data contract | ✅ Yes | System |
| contract-v1.json | Example data | ✅ Yes | Developer |

---

## Relationship to Contracts

Templates must align with:

```
contracts/schema.json
```

This means:

- all required fields must be present  
- structure must match the contract  
- naming must be consistent  

---

## System Flow

```
Image
   ↓
Extractor Agent (uses templates)
   ↓
Extraction Contract (structured JSON)
   ↓
Schema Validation ✅
   ↓
Layout Agent
   ↓
Layout Contract
   ↓
Render Agent
   ↓
SVG Output
```

---

## Why Both Templates Exist

| Template | Purpose |
|---------|--------|
| Human Output | enables human validation and understanding |
| Machine Output | ensures consistent structured JSON generation |

---

## Important Rules

- templates must follow the contract structure  
- templates must not introduce new fields  
- templates may omit optional fields  
- human template must remain readable and concise  

---

## Future Expansion

Templates may be extended to support:

- debug output  
- validation diagnostics  
- intermediate transformation views  

without affecting the core contract  

---

## Summary

```
Templates = OUTPUT FORMAT GUIDE  
Contracts = OUTPUT STRUCTURE RULES  
Schema = VALIDATION LAYER  
```

---

Both are required:

- Templates guide AI output ✅  
- Contracts guarantee system consistency ✅  
``
# Templates

This folder contains the **output templates used by the Image Extractor Agent**.

Templates guide the AI in generating structured output, but they are **not the data contract**.

---

## Purpose

Templates define:

- How output should be formatted
- How information is presented
- How the AI structures its response

They help ensure **consistent and predictable responses** from the agent.

---

## Types of Templates

This folder includes two template types:

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
- Not validated directly ❌

---

## IMPORTANT DISTINCTION — TEMPLATE vs CONTRACT

Templates are **not the source of truth** for the system.

```
templates/   → HOW output is generated
contracts/   → WHAT output must look like
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

Templates must be aligned with:

```
contracts/extraction/schema.json
```

This means:

- All required fields must be present
- Structure must match the contract
- Naming must be consistent

---

## System Flow

```
Image
   ↓
Extractor Agent (uses templates)
   ↓
Generated Output (JSON + Human View)
   ↓
Validated against schema.json ✅
   ↓
Consumed by Renderer Agent
```

---

## Why Both Templates Exist

| Template | Why |
|---------|-----|
| Human Output | Helps users understand and validate extraction |
| Machine Output | Helps AI produce consistent structured JSON |

---

## Important Rules

- Templates must follow the contract structure
- Templates must not introduce new fields not defined in schema
- Templates may omit optional fields if not present
- Human template must remain readable and concise

---

## Future Expansion

Templates may be extended to support:

- Debug output
- Visualization hints
- Intermediate validation views

Without affecting the core contract

---

## Summary

```
Templates = OUTPUT FORMAT GUIDE
Contracts = OUTPUT STRUCTURE RULES
```

Both are required:

- Templates guide AI output ✅
- Contracts guarantee system consistency ✅
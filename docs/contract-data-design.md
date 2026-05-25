# Contract Data Design — OSRS Extraction System

---

# OVERVIEW

This document defines the **data architecture and contract design** for the OSRS floor plan extraction system.

The system is built as a **contract-driven AI pipeline**, where:

- Data structure is strictly defined
- AI output is controlled via templates
- Results are validated and reviewable

---

# SYSTEM ARCHITECTURE

The system consists of three core layers:

```
Contract Layer   → defines structure (truth)
Template Layer   → guides AI generation
Example Layer    → defines expected output
```

---

## End-to-End Flow

```
Image
  ↓
Extractor Agent (uses templates)
  ↓
Generated Output (JSON + Human View)
  ↓
Validated against schema.json ✅
  ↓
Reviewed by human ✅
  ↓
Consumed by Renderer / Apps
```

---

# 1. CONTRACT LAYER (GLOBAL TRUTH)

Location:
```
contracts/
```

---

## Purpose

Defines:

```
WHAT the data must look like ✅
```

This is the **single source of truth** for the entire system.

---

## Components

### schema.json

- Defines all fields and types
- Enforces validation rules
- Guarantees structural correctness

---

### contract-v1.json

- Example of valid contract data
- Demonstrates:
  - layout structure
  - note scope usage
  - grouping logic

---

### README.md

- Explains semantics
- Defines rules (e.g., note scope)
- Documents system behavior

---

## Key Principle

```
Contracts define structure — NOT behavior
```

Agents must follow contract, not redefine it.

---

# 2. TEMPLATE LAYER (AI GENERATION CONTROL)

Location:
```
templates/
```

---

## Purpose

Defines:

```
HOW AI should generate output ✅
```

Templates act as a **controlled generation scaffold**.

---

## Components

### machine-output.json

Defines structured JSON format using placeholders.

Example:

```json
"area_id": "{{area_id}}"
```

---

### Role

- Enforces consistent structure
- Prevents missing fields
- Ensures deterministic output

---

## Why It Exists

AI does not reliably follow schema alone.

Without template:

- fields may be skipped ❌  
- structure may drift ❌  

With template:

- structure is fixed ✅  
- AI fills values only ✅  

---

### human-output.md

Defines human-readable output format.

---

## Role

- Visual validation interface
- Enables human review
- Supports correction workflow

---

## Design Model

```
Visual Layout + Semantic Context
```

---

## Output Structure

| Section | Purpose |
|--------|--------|
| Area Layout | high-level positioning |
| Layout | spatial structure |
| Groups | logical relationships |
| Notes | semantic meaning |

---

# 3. EXAMPLE LAYER (GROUND TRUTH)

Location:
```
examples/
```

---

## Purpose

Defines:

```
WHAT correct output looks like ✅
```

---

## Structure

```
examples/
  cat-floor-plan/
  dog-floor-plan/
```

Each example contains:

- input image
- machine-output.json
- human-output.md

---

## Role

- test dataset ✅  
- validation reference ✅  
- AI alignment ✅  

---

# CORE DATA MODEL

The system uses a **hierarchical row-based layout model**.

---

## Model Structure

```
Floor Plan
   → Area Layout (positions)
      → Areas
         → Layout Rows (order)
            → Spaces (geometry)
            → Groups (logic)
```

---

# LAYOUT SYSTEM

## Row-Based Model (NOT Grid)

Traditional grid systems use:

```
rows + columns
```

This fails for:

- uneven layouts  
- merged spaces  
- real-world floor plans  

---

## OSRS Approach

```
Row-based layout ✅
```

---

## Area Layout

```
floor_plan.area_layout.rows
```

Defines how areas are positioned.

---

## Space Layout

```
area.layout.rows
```

Defines space ordering within an area.

---

## Space Geometry

Each space defines:

- row
- col_start
- col_span

---

## Important Concept

```
col_span = visual width (like merged cells)
```

Equivalent to:

- Excel merge
- HTML colspan

---

# NOTE SCOPE MODEL

Notes must be assigned at the correct level.

---

## Scope Levels

| Level | Field | Use |
|------|------|-----|
| Area | area_note | entire area |
| Space | space.note | individual space |
| Group | group.note | multiple spaces |

---

## Rules

- Use the most specific level  
- Do NOT duplicate notes  
- Do NOT infer scope  
- Only assign where explicitly defined  

---

## Example

Incorrect:

```json
"area_note": "Temporary Area"
```

Correct:

```json
{
  "id": "5",
  "note": "Temporary Area"
}
```

---

# KEY DESIGN PRINCIPLES

---

## 1. Separation of Concerns

| Layer | Responsibility |
|------|----------------|
| Layout | structure |
| Spaces | geometry |
| Notes | semantics |
| Groups | relationships |

---

## 2. Minimal Assignment (AI Control)

Templates provide only:

- required structure  
- placeholders  

Avoid:

- redundant fields  
- unnecessary defaults  

---

## 3. Deterministic Output

AI must produce:

- consistent structure  
- schema-compliant output  

---

## 4. Human Validation First

System is designed for:

```
AI → Human Review → Final Output ✅
```

---

# SYSTEM CAPABILITIES

This design supports:

- multi-area layouts  
- merged spaces  
- flexible row structures  
- semantic annotations  
- grouping relationships  

---

# FUTURE EXTENSIONS

This architecture supports:

- Renderer Agent (UI generation)
- Verifier Agent (output validation)
- Analytics layer
- Power Apps integration

---

# SUMMARY

The OSRS system is a:

```
Contract-Driven AI Data Platform
```

---

## Final Layer Model

```
Schema → validation rules
Contract → data structure
Template → AI generation
Example → expected output
Agent → execution
```

---

## Key Outcome

- Deterministic AI output ✅  
- Human-verifiable results ✅  
- Scalable system design ✅  

---
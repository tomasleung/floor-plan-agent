# Extraction Contract

This folder defines the **data contract produced by the Image Extractor Agent**.

It is the **single source of truth** for the structure, meaning, and validation of floor plan data across the system.

---

# PURPOSE

The contract defines:

- The structure of extracted floor plan data
- Required fields and relationships
- The interface between all agents (Extractor → Renderer → Applications)

---

# PRINCIPLES

The contract follows these principles:

- ✅ Deterministic structure (no ambiguity)
- ✅ Fully machine-readable
- ✅ Semantically consistent
- ✅ Contract-driven (NOT agent-driven)
- ✅ Backward compatible

---

# OWNERSHIP MODEL

```
contracts/ = defines WHAT the data must look like  
agents.md    = defines HOW the data is produced  
templates/ = defines HOW the data is presented  
```

---

## Key Rule

✅ The contract is the source of truth  
❌ Agents must NOT redefine data structure  

---

# LAYOUT MODEL (CRITICAL)

The system uses a **hierarchical row-based layout model** instead of a fixed grid.

---

## 1. Floor Plan Level — Area Layout

```
floor_plan.area_layout.rows
```

Defines how areas are arranged spatially.

Example:

```
Row 1 → A1, A2  
Row 2 → A3, A4, A5
```

---

## 2. Area Level — Space Layout

```
area.layout.rows
```

Defines how spaces are arranged within each area.

Example:

```
Row 1 → 1, 2, 3, 4  
Row 2 → 9–10  
Row 3 → 5, 6, 7, 8
```

---

## 3. Space Level — Geometry

```
spaces[]
```

Each space defines:

- `row` → vertical position  
- `col_start` → horizontal start  
- `col_span` → width (merged support)  
- `unit_count` → logical units (optional)  
- `note` → semantic annotation (optional)

---

# NOTE SCOPE LEVELS (IMPORTANT ⭐)

Notes must be assigned to the **correct semantic level**.

---

## Scope Levels

| Level | Field | Use When |
|------|------|----------|
| Area | `area_note` | applies to the entire area |
| Space | `space.note` | applies to an individual space |
| Group | `group.note` | applies to a range of spaces |

---

## Rules (MANDATORY)

1. ✅ Use the **most specific level possible**

```
space > group > area
```

---

2. ❌ Do NOT assign notes to `area_note` if they apply to only one space

---

3. ✅ Only use group notes when explicitly defined (e.g., “1–2 Public View”)

---

4. ❌ Do NOT infer note scope from layout patterns

---

## Example

### ❌ Incorrect

```json
"area_note": "Temporary Area"
```

---

### ✅ Correct

```json
{
  "id": "5",
  "note": "Temporary Area"
}
```

---

# WHY NOT GRID?

Traditional models use:

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
Grid Model ❌
→ Row-based Layout ✅
```

---

# KEY OBJECTS

## FLOOR_PLAN

Top-level container.

Contains:

- `area_layout`
- `areas[]`

---

## AREA

Logical section (room / zone).

Contains:

- layout
- spaces
- groups
- optional area_note

---

## SPACE

Smallest unit (e.g., kennel, slot).

Defines:

- position
- width
- optional note

---

## GROUP

Logical grouping of spaces.

Example:

- "Public View"
- "Large Units"

---

# VALIDATION

All outputs MUST conform to:

```
schema.json
```

This ensures:

- correct structure  
- valid data types  
- required fields present  

---

# VERSIONING

Contracts must be versioned:

```
contract-v1.json
contract-v2.json
```

Rules:

- Do NOT break existing versions  
- Introduce new version for structural changes  

---

# RELATIONSHIP TO AGENTS

```
Image → Extractor → Contract → Renderer → UI
```

- Extractor produces contract-compliant data  
- Renderer consumes contract data  
- UI displays final output  

---

# RELATIONSHIP TO TEMPLATES

Templates are for formatting only:

```
templates/
```

- human-output.md → visual validation  
- machine-output.json → AI generation guide  

---

## Key Rule

Templates MUST follow the contract  
Templates are NOT the source of truth  

---

# SUMMARY

The contract defines a structured, scalable layout system:

```
Floor Plan
   → Area Layout (positions)
      → Areas
         → Layout Rows (ordering)
            → Spaces (geometry + notes)
            → Groups (logic)
```

---

## FINAL MODEL

```
Contract = structure ✅
Schema = validation ✅
Agent = execution ✅
Template = presentation ✅
```

---
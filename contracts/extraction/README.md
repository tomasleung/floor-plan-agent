# Extraction Contract

This folder defines the **data contract produced by the Image Extractor Agent**.

It is the **single source of truth** for how floor plan data is structured, validated, and consumed across the OSRS system.

---

# PURPOSE

The contract defines:

- The exact structure of extracted floor plan data
- Required fields and relationships
- The data interface between agents (Extractor → Renderer → Applications)

---

# PRINCIPLES

The contract is designed with the following principles:

- ✅ Deterministic structure (no ambiguity)
- ✅ Fully machine-readable
- ✅ Semantically documented (every field has meaning)
- ✅ Backward compatible
- ✅ Contract-driven (NOT agent-driven)

---

# OWNERSHIP MODEL

```
contracts/ = defines WHAT the data must look like  
agents/    = defines HOW the data is produced  
templates/ = defines HOW the data is displayed  
```

---

## Key Rule

✅ The contract is the source of truth  
❌ Agents must NOT redefine structure  

---

# LAYOUT MODEL (CRITICAL)

OSRS uses a **hierarchical row-based layout system** instead of a fixed grid.

This model accurately represents real-world layouts, including:

- uneven rows
- merged spaces (e.g., "9-10")
- non-rectangular structures
- multi-area floor plans

---

## 1. FLOOR PLAN LEVEL (Area Positioning)

Defines how areas are arranged within the floor plan.

```
floor_plan.area_layout.rows
```

### Example:

```
Row 1 → A1, A2  
Row 2 → A3, A4, A5
```

Each row represents a horizontal grouping of areas.

---

## 2. AREA LEVEL (Space Layout)

Defines how spaces are arranged within each area.

```
area.layout.rows
```

### Example:

```
Row 1 → 1, 2, 3, 4  
Row 2 → 9–10  
Row 3 → 5, 6, 7, 8
```

This allows flexible, non-uniform layouts.

---

## 3. SPACE LEVEL (Geometry & Structure)

Defines exact position and width of each space.

```
spaces[]
```

Each space includes:

- `row` → vertical position
- `col_start` → starting position within the row
- `col_span` → width (number of columns spanned)
- `unit_count` (optional) → logical representation of merged units
- `note` (optional) → label

---

## KEY CONCEPT

Each layer serves a distinct purpose:

| Layer | Purpose |
|------|--------|
| area_layout | Positions areas |
| layout.rows | Defines order of spaces |
| spaces | Defines geometry |

---

# WHY NOT GRID?

Traditional grid models use:

```
rows + columns
```

This approach fails for real-world layouts because it cannot handle:

- variable row widths
- merged cells
- asymmetric structures

---

## OSRS APPROACH

```
Grid Model ❌
→ Row-based Layout Model ✅
```

---

# KEY OBJECTS

## FLOOR_PLAN

Top-level container.

Contains:
- area_layout
- areas[]

---

## AREA

Logical container for a section of the floor plan.

Contains:
- layout (row structure)
- spaces (geometry)
- groups (optional logical grouping)

---

## SPACE

Smallest unit (e.g., kennel, room section).

Defines:
- position (row, col_start)
- width (col_span)
- logical representation (unit_count)

---

## GROUP (Optional)

Defines logical grouping across multiple spaces.

Example:
- "Large / Public View"
- repeated annotations

---

# VALIDATION

All outputs MUST conform to:

```
schema.json
```

This ensures:

- required fields are present
- data types are correct
- structure is consistent

---

# VERSIONING

Contracts must be versioned:

```
contract-v1.json
contract-v2.json
```

Rules:

- Do NOT break existing contracts
- Introduce new versions for structural changes

---

# RELATIONSHIP TO AGENTS

```
Image → Extractor → Contract → Renderer → UI
```

- Extractor produces structured contract
- Renderer consumes contract for layout generation
- Applications consume rendered output

---

# RELATIONSHIP TO TEMPLATES

Templates exist for readability:

```
templates/
  human-output.md
  machine-output.json
```

Important:

- Templates are NOT the source of truth
- Templates MUST follow the contract
- Schema enforces correctness

---

# SUMMARY

This contract defines:

- a deterministic and structured layout system
- a hierarchical model for areas and spaces
- a system that is flexible, scalable, and UI-ready

---

## FINAL MODEL

```
Floor Plan
   → Area Layout (positions)
      → Areas
         → Layout Rows (order)
            → Spaces (geometry)
```

---

✅ Contract = structure  
✅ Schema = enforcement  
✅ Agent = execution  
✅ Template = presentation

---
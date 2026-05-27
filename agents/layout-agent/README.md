# Layout Agent

## Overview

The Layout Agent is responsible for defining the **geometric structure of the floor plan**.

It converts structured data into a **deterministic layout** by assigning positions, rows, and spatial relationships.

---

## Role

```
Extractor → WHAT exists  
Layout → WHERE it goes  
Render → HOW it looks  
```

The Layout Agent defines the **WHERE layer**.

---

## Purpose

The agent transforms:

```
Extraction Contract → Layout Contract
```

It determines:

- spatial arrangement of areas  
- ordering of spaces within areas  
- row structure and alignment  
- spacing and layout constraints  

---

## Input

- Extraction Contract (structured data from Extractor)

---

## Output

- Layout Contract (geometry and positioning data)

---

## Responsibilities

The Layout Agent MUST:

✅ assign rows and ordering for areas  
✅ define layout rows within each area  
✅ determine `col_start` and `col_span`  
✅ maintain adjacency and logical grouping  
✅ respect layout constraints  

---

The Layout Agent MUST NOT:

❌ change semantic meaning (names, groups, notes)  
❌ infer missing spaces or data  
❌ modify extracted structure  
❌ introduce non-deterministic placement  

---

## Layout Model

The system uses a **row-based layout model**.

---

### Area Layout

```
floor_plan.area_layout.rows
```

Defines how areas are positioned relative to each other.

---

### Space Layout

```
area.layout.rows
```

Defines how spaces are arranged within each area.

---

### Space Geometry

Each space includes:

- `row` → vertical position  
- `col_start` → horizontal start  
- `col_span` → width of the space  

---

## Constraints

---

### Hard Constraints (MUST follow)

- minimum width ≥ 89px  
- minimum height ≥ 90px  
- schema compliance  
- valid row and column structure  

---

### Soft Constraints (optimization)

- spacing between spaces  
- alignment (left, center, right)  
- visual balance  

---

## Deterministic Behavior

The Layout Agent must produce:

```
Same input → Same layout
```

---

### Rules

- no randomness  
- consistent placement logic  
- repeatable results  

---

## Human-in-the-Loop

The Layout stage includes validation before rendering.

---

### Review Objectives

- verify layout usability  
- confirm spacing and alignment  
- adjust layout if needed  

---

## Relationship to Contracts

The Layout Agent uses and produces contracts:

```
Extraction Contract → input  
Layout Contract → output  
```

---

## Relationship to Templates

Templates guide how layout output is generated.

Location:

```
templates/
```

Includes:

- human-output.md → readable layout view  
- machine-output.json → structured layout output  
- examples/ → validation cases  

---

## System Flow

```
Image
   ↓
Extractor Agent
   ↓
Extraction Contract
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

## Design Principles

---

### Separation of Concerns

| Stage | Responsibility |
|------|----------------|
| Extractor | WHAT |
| Layout | WHERE |
| Render | HOW |

---

### Contract-Driven Design

- Layout must follow the contract schema  
- no deviation allowed  

---

### Constraint-First Design

- rules must be satisfied before layout decisions  

---

### Human Governance

- layout must be reviewed before rendering  

---

## Summary

The Layout Agent transforms:

```
Structured Data → Spatial Layout
```

It ensures:

- ✅ consistent positioning  
- ✅ valid geometry  
- ✅ deterministic layout  
- ✅ compatibility with rendering  

---

## Final Model

```
Extraction Contract (WHAT)
   ↓
Layout Contract (WHERE)
   ↓
Render (HOW)
```

---
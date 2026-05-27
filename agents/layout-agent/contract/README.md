# Layout Contract

This folder defines the **data contract produced by the Layout Agent**.

It represents the **WHERE layer**, defining the spatial structure and geometry of the floor plan.

---

## Scope

This contract defines the **Layout Contract (WHERE layer)**.

The system uses multiple contracts:

- Extraction Contract (WHAT) → defines structure  
- Layout Contract (WHERE) → defines geometry  
- Render Spec (HOW) → defines visual rules  

---

## TL;DR

- schema.json → defines layout structure  
- contract-v1.json → valid example  
- layout agent → generates geometry  
- render agent → consumes layout output  

---

## Purpose

The contract defines:

- spatial arrangement of areas  
- ordering of elements  
- row-based layout structure  
- geometric positioning of spaces  

---

## Principles

- ✅ Deterministic layout (same input → same output)  
- ✅ Geometry-focused (no semantic modification)  
- ✅ Contract-driven design  
- ✅ Schema-validated  

---

## Ownership Model

```
contracts/ = defines WHERE structure must follow  
agents/    = defines HOW layout is generated  
templates/ = defines HOW output is formatted  
```

---

### Key Rule

✅ Layout must preserve extraction meaning  
❌ Layout must NOT modify semantic data  

---

## Layout Model

The layout contract defines geometry using a **row-based system**.

---

### Area Layout

```
floor_plan.area_layout.rows
```

Defines how areas are arranged across rows.

---

### Space Layout

```
area.layout.rows
```

Defines ordering of spaces within areas.

---

### Geometry Fields

Each space includes:

- `row`  
- `col_start`  
- `col_span`  

---

## Constraints

---

### Hard Constraints (MUST)

- minimum width ≥ 89px  
- minimum height ≥ 90px  
- valid row/column structure  
- schema compliance  

---

### Soft Constraints (Optimization)

- spacing  
- alignment  
- visual balance  

---

## Validation

All outputs MUST conform to:

```
schema.json
```

---

## Versioning

```
contract-v1.json
contract-v2.json
```

---

### Rules

- no breaking changes  
- introduce new versions for structural updates  

---

## Used By

- Layout Agent (producer)  
- Render Agent (consumer)  

---

## Relationship to Other Contracts

```
Extraction Contract → Layout Contract → Render Spec
```

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
```

---

## Summary

The layout contract defines:

```
Spatial structure → rows, ordering, geometry
```

---

## Final Model

```
Extraction (WHAT)
   ↓
Layout (WHERE)
   ↓
Render (HOW)
```

---
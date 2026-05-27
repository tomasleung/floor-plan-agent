# Render Specification (Contract)

This folder defines the **render specification used by the Image Render Agent**.

It represents the **HOW layer**, defining how structured data is converted into visual output (SVG).

---

## Scope

This specification defines the **Render Layer (HOW)**.

The system includes:

- Extraction Contract (WHAT) → structure  
- Layout Contract (WHERE) → geometry  
- Render Spec (HOW) → visual rules  

---

## TL;DR

- schema.json → validates render data  
- render-spec.v1.json → defines rendering rules  
- render agent → consumes contracts + spec  
- output → SVG  

---

## Purpose

The render spec defines:

- how shapes are drawn  
- layout spacing and alignment  
- text positioning and formatting  
- styling rules (colors, borders, fonts)  

---

## Principles

- ✅ Deterministic output  
- ✅ No data modification  
- ✅ Visual consistency  
- ✅ Contract-driven execution  

---

## Ownership Model

```
contracts/ = defines HOW output should be rendered  
agents/    = executes rendering logic  
templates/ = guides output generation  
```

---

### Key Rule

✅ Render MUST NOT modify data  
❌ Render MUST NOT infer structure  

---

## Render Inputs

The Render Agent consumes:

- Extraction Contract  
- Layout Contract  
- Render Spec  

---

## Output

- SVG file  

---

## Render Model

The rendering process applies:

```
Data (WHAT)
+ Geometry (WHERE)
+ Rendering Rules (HOW)
→ SVG Output
```

---

## Key Concepts

---

### Geometry Mapping

- space → rectangle  
- group → visual grouping  
- area → labeled section  

---

### Styling Rules

Defined in:

```
render-spec.v1.json
```

Includes:

- colors  
- font sizes  
- spacing rules  
- alignment rules  

---

## Validation

Render output must align with:

```
schema.json
```

---

## Versioning

```
render-spec.v1.json
render-spec.v2.json
```

---

### Rules

- do not break existing specs  
- version changes for visual updates  

---

## Used By

- Render Agent (core execution)  
- UI applications (consumer)  

---

## System Flow

```
Extraction Contract
   ↓
Layout Contract
   ↓
Render Agent
   ↓
SVG Output
```

---

## Summary

The render specification defines:

```
Visual rules → shapes, layout, styling
```

---

## Final Model

```
Extraction (WHAT)
   ↓
Layout (WHERE)
   ↓
Render Spec (HOW)
   ↓
SVG
```

---
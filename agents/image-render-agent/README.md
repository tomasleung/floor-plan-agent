# Image Render Agent

## Overview

The Image Render Agent is responsible for generating the final **SVG output** from structured data.

It represents the **HOW layer** of the system, converting data and layout into a **visual, UI-ready representation**.

---

## Role

```
Extractor → WHAT exists  
Layout → WHERE it goes  
Render → HOW it looks  
```

The Render Agent defines the **HOW layer**.

---

## Purpose

The agent transforms:

```
Extraction Contract + Layout Contract → SVG Output
```

It applies:

- layout geometry  
- rendering rules  
- visual styling  

to produce a deterministic visual result.

---

## Inputs

The Render Agent consumes:

- **Extraction Contract (WHAT)**  
- **Layout Contract (WHERE)**  
- **Render Specification (HOW)**  

---

## Output

- SVG file (UI-ready)

---

## Responsibilities

The Render Agent MUST:

✅ apply layout geometry to visual elements  
✅ render spaces, groups, and areas  
✅ apply styling rules (colors, fonts, spacing)  
✅ maintain visual consistency  
✅ produce deterministic output  

---

The Render Agent MUST NOT:

❌ modify input data  
❌ infer missing structure  
❌ change layout decisions  
❌ introduce randomness  

---

## Deterministic Execution

The Render Agent is **fully deterministic**.

```
Same input → Same SVG output
```

---

### Rules

- no randomness  
- no interpretation  
- rule-based rendering only  

---

## Rendering Model

The rendering process combines:

```
Data (WHAT)
+ Geometry (WHERE)
+ Render Spec (HOW)
→ SVG Output
```

---

## Key Concepts

---

### Geometry Mapping

Each data element maps to a visual component:

| Data Element | Visual Element |
|-------------|----------------|
| Space | Rectangle |
| Area | Container / Section |
| Group | Group Label |
| Note | Text annotation |

---

### Styling Rules

Defined in:

```
contract/render-spec.v1.json
```

Includes:

- colors  
- font sizes  
- spacing  
- alignment  
- layout offsets  

---

## Constraints

---

### Hard Constraints

- must match layout geometry exactly  
- must follow render specification  
- must produce valid SVG  
- must be UI-compatible  

---

### Soft Constraints

- readability  
- spacing clarity  
- label alignment  

---

## Human-in-the-Loop

The Render Agent typically executes after data and layout have been validated.

Human adjustments may include:

- label positioning  
- spacing fine-tuning  
- visual refinement  

---

## Relationship to Contracts

The Render Agent consumes:

```
Extraction Contract → WHAT  
Layout Contract → WHERE  
Render Spec → HOW  
```

---

## Relationship to Templates

Templates guide rendering behavior and output generation.

Location:

```
templates/
```

Includes:

- render-prompt.txt → rendering instructions  
- examples/ → reference inputs and outputs  

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

| Layer | Responsibility |
|------|----------------|
| Extractor | WHAT |
| Layout | WHERE |
| Render | HOW |

---

### Contract-Driven Execution

- Render must follow all upstream contracts  
- no deviation allowed  

---

### Deterministic Rendering

- output must be consistent  
- no variability allowed  

---

### Execution-Only Model

- Render executes rules  
- does NOT reason or interpret  

---

## Summary

The Image Render Agent transforms:

```
Structured Data + Layout → Visual Output
```

It ensures:

- ✅ consistent rendering  
- ✅ valid geometry  
- ✅ UI-ready output  
- ✅ deterministic results  

---

## Final Model

```
Extraction (WHAT)
   ↓
Layout (WHERE)
   ↓
Render (HOW)
   ↓
SVG
```

---
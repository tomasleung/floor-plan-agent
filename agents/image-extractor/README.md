# Image Extractor Agent# Image Extract## Overview

The Image Extractor Agent is responsible for converting floor plan images into structured data.

It represents the **WHAT layer** of the system, identifying all relevant elements and organizing them into a contract-compliant format.

---

## Role

```
Extractor → WHAT exists  
Layout → WHERE it goes  
Render → HOW it looks  
```

The Extractor defines the **WHAT layer**.

---

## Purpose

The agent transforms:

```
Image → Extraction Contract (Structured JSON)
```

It extracts and organizes:

- areas  
- spaces  
- groups  
- notes  

---

## Input

- floor plan image  

---

## Output

- Extraction Contract (structured JSON)

---

## Responsibilities

The Image Extractor MUST:

✅ identify all areas, spaces, and groups  
✅ preserve structure from the source image  
✅ assign notes at the correct semantic level  
✅ produce contract-compliant output  
✅ ensure data completeness  

---

The Image Extractor MUST NOT:

❌ infer missing or unclear data  
❌ modify structural relationships  
❌ introduce fields not defined in the contract  
❌ apply layout or visual decisions  

---

## Data Model

The output follows the **Extraction Contract**.

Structure:

```
Floor Plan
   → Area Layout
      → Areas
         → Layout Rows
            → Spaces
            → Groups
```

---

## Key Concepts

---

### Areas

Logical sections of the floor plan (e.g., zones or rooms)

---

### Spaces

Smallest identifiable units (e.g., kennels, slots)

---

### Groups

Logical groupings of spaces

---

### Notes

Annotations that must be applied at the correct level:

- area level  
- group level  
- space level  

---

## Deterministic Behavior

The extractor must produce:

```
Same image → Same structured output
```

---

### Rules

- no randomness  
- consistent interpretation  
- repeatable structure  

---

## Human-in-the-Loop

Extraction output is validated before passing to the layout stage.

---

### Review Objectives

- verify completeness of extracted data  
- confirm correct structure  
- validate note placement  
- ensure no missing elements  

---

## Relationship to Contracts

The Extractor produces:

```
Extraction Contract (WHAT)
```

Defined in:

```
contract/
```

---

## Relationship to Templates

Templates guide how the output is generated.

Location:

```
templates/
```

Includes:

- machine-output.json → structure guidance  
- human-output.md → readable summary  
- examples/ → reference outputs  

---

## System Flow

```
Image
   ↓
Image Extractor Agent
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

### Contract-Driven Output

- must follow schema  
- no deviation allowed  

---

### Separation of Concerns

| Stage | Responsibility |
|------|----------------|
| Extractor | WHAT |
| Layout | WHERE |
| Render | HOW |

---

### Minimal Interpretation

- extract only what is explicitly present  
- avoid assumption or inference  

---

### Structured Output

- output must be machine-readable  
- consistent JSON format required  

---

### Human Governance

- validation required before downstream processing  

---

## Summary

The Image Extractor Agent transforms:

```
Unstructured Image → Structured Data
```

It ensures:

- ✅ complete extraction  
- ✅ consistent structure  
- ✅ contract compliance  
- ✅ reliable downstream input  

---

## Final Model

```
Image
   ↓
Extraction (WHAT)
   ↓
Layout (WHERE)
   ↓
Render (HOW)
```

---



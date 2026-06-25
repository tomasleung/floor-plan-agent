# SVG Agent

## Overview

The SVG Agent is responsible for converting structured layout data into a **final visual floor plan (SVG)**.

It transforms deterministic layout contracts into a **fully rendered, styled, labeled diagram**.

---

## Role

```
Extractor → WHAT exists  
Layout → WHERE it goes  
SVG Agent → HOW it looks  
```

The SVG Agent defines the **HOW layer**.

---

## Purpose

The agent transforms:

```
Layout Contract → SVG Output
```

It determines:

- visual rendering of spaces  
- application of layout geometry  
- label placement (titles, space labels, notes)  
- styling and appearance  

---

## Input

- Layout Contract (geometry and structure)
- GLOBAL LAYOUT CONFIG
- GLOBAL INNER LAYOUT CONFIG
- GLOBAL LABEL CONFIG
- SVG TEMPLATE

---

## Output

- SVG (deterministic visual layout)
- (optional) PNG export

---

## Responsibilities

The SVG Agent MUST:

✅ render layout exactly as defined  
✅ apply inner layout templates correctly  
✅ compute all dimensions deterministically  
✅ place labels according to label config  
✅ render all rectangles with valid dimensions  
✅ maintain visual alignment and proportions  

---

The SVG Agent MUST NOT:

❌ modify layout structure  
❌ reorder boxes or spaces  
❌ infer missing structure  
❌ apply random styling or positioning  
❌ skip labels or geometry  

---

## Rendering Model

The system uses a **config-driven rendering model**.

---

### Layout Application

Uses:

```
GLOBAL LAYOUT CONFIG
```

Defines:

- margins  
- rows  
- spacing  
- width distribution  

---

### Inner Layout

Uses:

```
GLOBAL INNER LAYOUT CONFIG
```

Defines:

- box templates (communal, ISO, medical)  
- section splits (25% / 75%)  
- grid structures  

---

### Label System

Uses:

```
GLOBAL LABEL CONFIG
```

Defines:

- title placement  
- space label positioning  
- sub-label placement  
- naming and fallback rules  

---

### SVG Template

Uses:

```
SVG TEMPLATE
```

Defines:

- fonts  
- colors  
- stroke  
- visual style  

---

## Rendering Pipeline

```
Layout → Inner Layout → Labels → SVG
```

---

### Step 1 — Apply Layout

- compute margins  
- compute row heights  
- compute box positions  

---

### Step 2 — Apply Inner Layout

- split box into sections  
- apply row percentages  
- apply grid columns  

---

### Step 3 — Apply Labels

- extract label text  
- normalize naming  
- apply fallback numbering  
- position labels:
  - title → centered  
  - space → top-left  
  - sub-label → below label  

---

### Step 4 — Render SVG

- draw rectangles  
- apply labels  
- ensure all grid lines and boundaries are visible  

---

## Constraints

---

### Geometry Constraints (MUST)

- every `<rect>` MUST have:
  - width  
  - height  

- no overlap  
- no missing sections  

---

### Label Constraints

- every space MUST have a label  
- no empty cells  
- labels must follow positioning rules  

---

### Layout Constraints

- layout must remain unchanged  
- spacing must follow config  
- percentages must be respected  

---

## Deterministic Behavior

The SVG Agent must produce:

```
Same input → Same SVG output
```

---

### Rules

- no randomness  
- consistent geometry computation  
- repeatable rendering  

---

## Human-in-the-Loop

Rendering only occurs after layout confirmation.

---

### Flow

1. Layout is proposed  
2. User confirms layout  
3. SVG is generated  

---

## Relationship to Contracts

The SVG Agent transforms:

```
Layout Contract → SVG Output
```

---

## Relationship to Configuration

All rendering behavior is driven by:

```
/contract/
  global-layout-config.md
  global-inner-layout-config.md
  global-label-config.md
  svg-template.svg
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
SVG Agent
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
| SVG | HOW |

---

### Contract-Driven Rendering

- SVG must strictly follow layout contract  
- no deviation allowed  

---

### Config-Driven System

- all behavior comes from defined configs  
- no hardcoding in rendering  

---

### Deterministic Execution

- identical input produces identical output  

---

### Validation-First Design

- geometry must be valid before rendering  
- labels must be complete  

---

## Summary

The SVG Agent transforms:

```
Layout → Visual Output
```

It ensures:

- ✅ accurate geometry  
- ✅ consistent layout  
- ✅ complete labeling  
- ✅ clean SVG output  
- ✅ deterministic rendering  

---

## Final Model

```
Extraction Contract (WHAT)
   ↓
Layout Contract (WHERE)
   ↓
SVG Output (HOW)
```
``
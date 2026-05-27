# Render Templates

This folder contains / Render InstructionThis folder contains the **templates used by the Image Render Agent**.

```
render-prompt.txt
```

#### Purpose

Defines how the rendering process should execute.

---

#### Audience

- AI agent  
- rendering engine  

---

#### Characteristics

- deterministic instructions ✅  
- structured process ✅  
- avoids ambiguity ✅  

---

### 2. Example Outputs

```
examples/
```

Includes:

- input JSON  
- output SVG  
- human-readable description  

---

#### Purpose

Provides:

- reference outputs  
- validation samples  
- correctness benchmarks  

---

## TEMPLATE vs CONTRACT

```
templates/ → HOW rendering is executed  
contracts/ → WHAT rendering rules exist  
schema → validates output correctness  
```

---

## Relationship to Render Spec

Templates must follow:

```
contracts/render-spec.v1.json
```

---

### Rules

- no deviation from spec  
- consistent visual output  
- deterministic behavior  

---

## System Flow

```
Extraction Contract
   ↓
Layout Contract
   ↓
Render Agent (uses templates)
   ↓
SVG Output
```

---

## Why Templates Exist

| Template | Purpose |
|----------|--------|
| Render Prompt | controls rendering execution |
| Examples | validate expected output |

---

## Important Rules

- must follow render specification  
- must not modify input data  
- must produce deterministic SVG  
- output must be UI-compatible  

---

## Future Expansion

Templates may include:

- animation rules  
- interaction metadata  
- advanced UI rendering logic  

---

## Summary

```
Templates = rendering execution guide  
Render Spec = visual rules  
Schema = validation  
```

Templates guide how rendering instructions are applied, but they are **not the source of truth**.

---

## Scope

These templates support the **Render Layer (HOW)**.

They are used to transform:

```
Extraction Contract + Layout Contract → SVG Output
```

---

## TL;DR

- templates → guide rendering logic  
- render spec → defines visual rules  
- schema → validates structure  
- templates must follow spec  

---

## Purpose

Templates define:

- how rendering instructions are applied  
- how layout data is interpreted visually  
- how consistent SVG output is produced  

---

## Template Types

---


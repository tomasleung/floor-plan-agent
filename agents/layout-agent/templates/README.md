# Layout Templates

This folder contains the **templates used by the Layout Agent**.

Templates guide how the agent generates structured layout output, but they are **not the source of truth**.

---

## Scope

These templates support the **Layout Contract (WHERE layer)**.

They are used to transform:

```
Extraction Contract → Layout Contract
```

---

## TL;DR

- templates = guide layout generation  
- contracts = define geometry rules  
- schema = validates output  
- templates must follow contract  

---

## Purpose

Templates define:

- how layout data is structured  
- how geometry is represented  
- how the agent produces consistent output  

---

## Template Types

---

### 1. Human Output Template

```
human-output.md
```

---

#### Purpose

Provides a readable representation of layout structure.

---

#### Audience

- humans  
- reviewers  
- analysts  

---

#### Characteristics

- readable ✅  
- structured ✅  
- useful for validation ✅  
- not consumed by other agents ❌  

---

### 2. Machine Output Template

```
machine-output.json
```

---

#### Purpose

Guides the agent to produce structured layout data.

---

#### Audience

- AI agent  
- system pipeline  

---

#### Characteristics

- structured format ✅  
- uses placeholders ✅  
- schema-aligned ✅  
- validated after generation ✅  

---

## TEMPLATE vs CONTRACT

```
templates/ → HOW layout is generated  
contracts/ → WHAT layout must look like  
schema → validates correctness  
```

---

## Relationship to Contracts

Templates must align with:

```
contracts/schema.json
```

---

### Rules

- all required fields must be present  
- structure must match schema  
- naming must be consistent  

---

## System Flow

```
Extraction Contract
   ↓
Layout Agent (uses templates)
   ↓
Layout Contract
   ↓
Schema Validation ✅
   ↓
Render Agent
   ↓
SVG Output
```

---

## Why Templates Exist

| Template | Purpose |
|----------|--------|
| Human Output | layout validation and review |
| Machine Output | consistent JSON generation |

---

## Important Rules

- must follow contract structure  
- must not introduce new fields  
- must produce deterministic output  
- human output must remain readable  

---

## Future Expansion

Templates may include:

- layout debug views  
- validation previews  
- visualization hints  

without changing the contract  

---

## Summary

```
Templates = layout generation guide  
Contracts = geometry structure  
Schema = validation layer  
```
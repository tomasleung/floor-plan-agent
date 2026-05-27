# Agent System

## Overview

This folder contains all **specialized agents** used in is responsible for a specific part of the pipeline:This folder contains all **specialized agents** used in the Floor Plan Agent System.

```
WHAT → WHERE → HOW
```

- Image Extractor → defines WHAT exists  
- Layout Agent → defines WHERE things go  
- Render Agent → defines HOW output is generated  

---

## Agent Architecture

Each agent follows a **standard structure**:

```
agent/
├── agent.md
├── contract/
├── templates/
```

---

### 1. agent.md

Defines:

- agent role and identity  
- behavior rules and constraints  
- execution logic and phases  
- governance and validation rules  

---

### 2. contract/

Defines the **data structure used by the agent**.

Includes:

- `schema.json` → validation rules  
- `contract-v1.json` → example contract  
- `README.md` → explains data model  

---

### 3. templates/

Defines how outputs are generated.

Includes:

- `machine-output.json` → structured output format  
- `human-output.md` → readable output  
- `agent-setup-sop.md` → usage instructions  
- `examples/` → sample inputs and outputs  

---

## Agents in This System

---

### 1. Image Extractor Agent (WHAT)

**Purpose:**  
Extract structured data from input images

**Input:**
- image

**Output:**
- Extraction Contract (structured JSON)

**Responsibilities:**
- identify areas, spaces, groups  
- preserve structure  
- avoid inference or hallucination  

---

### 2. Layout Agent (WHERE)

**Purpose:**  
Define layout geometry and positioning

**Input:**
- Extraction Contract

**Output:**
- Layout Contract (geometry data)

**Responsibilities:**
- assign row-based layout structure  
- define positioning and spacing  
- ensure UI constraints are met  

---

### 3. Image Render Agent (HOW)

**Purpose:**  
Generate deterministic SVG output

**Input:**
- Extraction Contract  
- Layout Contract  
- Render Spec  

**Output:**
- SVG file  

**Responsibilities:**
- apply geometry rules  
- render shapes and labels  
- produce UI-ready output  

The Render Agent is a **deterministic execution layer** and does not perform reasoning.

---

## Design Principles

---

### Contract-Driven Design

Agents communicate through contracts:

```
Extractor → Extraction Contract  
Layout → Layout Contract  
Render → uses both + render spec  
```

---

### Multi-Contract Architecture

The system uses separate contracts per stage:

- Extraction Contract (WHAT)
- Layout Contract (WHERE)
- Render Spec (HOW)

---

### Separation of Concerns

| Agent | Responsibility |
|------|----------------|
| Extractor | WHAT |
| Layout | WHERE |
| Render | HOW |

---

### Deterministic Execution

- same input → same output  
- schema validation enforced  
- no uncontrolled variability  

---

### Human-in-the-Loop

Each stage supports validation before proceeding:

- extraction review  
- layout review  

---

## How Agents Work Together

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

## Relationship to Framework

These agents are built using:

```
docs/agent-framework/
```

and operate under:

```
framework/project-execution-framework.md
```

---

## Summary

The agent system provides:

- ✅ modular execution  
- ✅ contract-based communication  
- ✅ deterministic processing  
- ✅ scalable architecture  


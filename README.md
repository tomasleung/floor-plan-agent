# Floor Plan Agent System

---

## Overview

This project builds a **deterministic AI agent pipeline** that converts floor plan inputs into:

✅ Structured data  
✅ Deterministic layout  
✅ SVG visual output (UI-ready)

---

## BUSINESS → Problem

Manual floor plan design creates several challenges:

- ❌ Inconsistent layouts across locations  
- ❌ Not suitable for UI systems (e.g., Power Apps)  
- ❌ Time-consuming manual recreation  
- ❌ No standardized structure or grid  

This makes it difficult to build scalable, reliable UI applications.

---

## TECH → Solution

This project introduces a **contract-driven, multi-agent system**:

```
Unstructured Input → Structured Data → Deterministic Layout → SVG Output
```

Core design principles:

- ✅ Contract-driven (schema-based data)
- ✅ Deterministic rendering (same input → same output)
- ✅ Separation of concerns
- ✅ Human-in-the-loop validation
- ✅ LLM used as controlled reasoning engine

---

## AGENTS → Execution Model

The system is implemented using **3 specialized agents**:

| Stage | Agent | Responsibility |
|------|------|----------------|
| WHAT | Image Extractor | Extract structured data from images |
| WHERE | Layout Agent | Define layout geometry (grid, rows, areas) |
| HOW | Render Agent | Generate final SVG output |

---

## System Architecture

```
Image (Input)
   ↓
Image Extractor (WHAT)
   ↓
Layout Agent (WHERE)
   ↓
Render Agent (HOW)
   ↓
SVG Output (UI-ready)
```

---

## System Diagrams

The system includes visual diagrams for architecture, data flow, and agent interaction:

- Architecture → system structure  
- Data Flow → data transformation  
- Agent Interaction → contract-driven design  

```
docs/diagrams/
```

---

## Why LLM + Agent System?

Floor plans are:

- Semi-structured (image-based)
- Require interpretation
- Require layout/UX decisions

LLM is used **in a controlled way**:

✅ LLM handles:
- reasoning
- layout decisions (spacing, alignment)

❌ LLM does NOT:
- define data structure
- control output format

Instead:

```
Contracts → define structure
Agents → enforce logic
LLM → operates within constraints
```

This ensures:

- ✅ Predictable output  
- ✅ Consistent structure  
- ✅ Human control  

---

## Contract-Driven Design (Multi-Contract Model)

The system uses **separate contracts per stage**:

- **Extraction Contract (WHAT)** → structured data model  
- **Layout Contract (WHERE)** → geometry and positioning  
- **Render Spec (HOW)** → styling and rendering rules  

This separation ensures:

- ✅ Clear responsibilities  
- ✅ Scalable architecture  
- ✅ Independent agent design  

---

## Repository Structure

```
floor-plan-agent/
├── agents/                  # Core processing logic
│   ├── image-extractor/     # WHAT (data extraction)
│   ├── layout-agent/        # WHERE (layout generation)
│   └── image-render-agent/  # HOW (SVG rendering)
├── docs/                    # Business + technical documentation
├── governance/              # Framework + execution principles
├── deployment/              # Deployment setup (future)
```

---

## Folder Responsibilities

| Folder | Purpose |
|------|--------|
| agents | Core agent logic (pipeline execution) |
| docs | BRD, TRD, contracts, framework, and diagrams |
| governance | Framework and operating model |
| deployment | Deployment and integration setup |

---

## Key Files

| Component | File |
|----------|------|
| Image Extractor | `agents/image-extractor/agent.md` |
| Layout Agent | `agents/layout-agent/agent.md` |
| Render Agent | `agents/image-render-agent/agent.md` |
| Render Spec | `agents/image-render-agent/contract/render-spec.v1.json` |

---

## Agent Framework

Agents are built using a standardized framework for:

- deterministic behavior  
- governance and constraints  
- structured execution  

See:

```
docs/agent-framework/
```

---

## How It Works

### Step 1 — Extract
```
Image → Structured JSON (contract-compliant)
```

---

### Step 2 — Layout
```
JSON → Deterministic grid layout
```

---

### Step 3 — Render
```
Layout + Data → SVG diagram
```

---

## Output

The final output is:

✅ SVG diagram  
✅ UI-ready (Power Apps compatible)  
✅ Deterministic layout  
✅ Consistent across all locations  

---

## SVG Adjustment Model

The system is designed for:

```
Agent → ~98% correct
User → ~2% manual refinement
```

Example adjustment:

```xml
<text y="30"> → y="34"
```

---

## Data Contract

This system uses a **contract-driven architecture** to ensure consistency across agents.

Learn more:

```
docs/data-contract/
```

---

## Documentation

Detailed documentation is available in:

```
/docs
```

Includes:

- Business Requirement (BRD)
- Technical Design (TRD)
- Data Contract Design
- Agent Framework
- System Diagrams

---

## Framework

This project is built on a broader **AI execution framework** that defines:

- agent orchestration
- governance model
- execution pipeline
- validation and learning loop

See:

```
framework/project-execution-framework.md
```
---

## Summary

This project provides:

- ✅ Standardized floor plan generation  
- ✅ Deterministic rendering system  
- ✅ Contract-based architecture  
- ✅ Scalable multi-agent pipeline  
- ✅ UI-ready outputs for applications like Power Apps  

---
``
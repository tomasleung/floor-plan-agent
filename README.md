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
| docs | BRD, TRD, contracts, and design documentation |
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
Layout → SVG diagram
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
agents/image-extractor/contract/README.md
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
- Operating Model

---

## Summary

This project provides:

- ✅ Standardized floor plan generation  
- ✅ Deterministic rendering system  
- ✅ Contract-based architecture  
- ✅ Scalable multi-agent pipeline  
- ✅ UI-ready outputs for applications like Power Apps  

---
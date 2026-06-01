# 🚀 Deployment — Floor Plan Rendering Agents

## 📦 Purpose

The `deployment/` folder contains all **production-ready PASP (Portable Agent Specification Package) files** required to run the **Contract-Driven Floor Plan Rendering System**.

This folder represents the **executable system layer** of the project.

---

## 🧠 System Overview

This deployment package enables a **deterministic pipeline** that converts:

Floor Plan Image
→ Structured Data
→ Layout Geometry
→ SVG Output

---

## 🔁 Execution Pipeline
Init → Extractor → Layout → Renderer → SVG

| Stage | Agent | Responsibility |
|------|------|----------------|
| 1 | Extractor | Convert image → structured JSON |
| 2 | Layout | Convert structure → layout geometry |
| 3 | Renderer | Convert layout → SVG |
| 4 | (Optional) SVG Assistant | Refine SVG (non-structural) |

---

## 📁 Folder Structure


deployment/
├── Init.md                         # System bootstrap & orchestration rules
├── SOP.md                          # Operational execution procedures
├── image-extractor.pasp.md         # Extractor Agent (WHAT)
├── layout-agent.pasp.md            # Layout Agent (WHERE)
├── image-render-agent.pasp.md      # Renderer Agent (HOW, v2.0)
├── svg-assistant-agent.pasp.md     # SVG review & improvement agent
├── template-pasp.md                # PASP template (for new agents)

---

## ⚙️ How to Run

### ✅ Step 1 — Initialize System
Load:


Init.md

This activates:
- agent orchestration rules
- execution constraints
- deterministic workflow enforcement

---

### ✅ Step 2 — Load Agents

Load PASPs in this order:

1. `image-extractor.pasp.md`
2. `layout-agent.pasp.md`
3. `image-render-agent.pasp.md`

Optional:
- `svg-assistant-agent.pasp.md`

> ⚠️ System will NOT execute if any required agent is missing

---

### ✅ Step 3 — Provide Input

- Floor plan image (PNG / JPG)

---

### ✅ Step 4 — Follow Execution Flow

1. Extractor → outputs structure → ✅ confirm  
2. Layout → outputs geometry → ✅ confirm  
3. Renderer → outputs SVG  

---

## 📐 Key Constraints

### ✅ Golden Rule

Minimum space size:
≥ 89 px width
≥ 90 px height

---

### ✅ Renderer v2.0 Rule

```json
"row_constraints": {
  "equal_area_height_per_row": true
}


All areas in the same row MUST have identical height


🔒 Execution Rules

❌ No structure inference
❌ No layout modification
❌ No space duplication
❌ No missing elements
✅ Deterministic output only


✅ Output

✅ SVG (primary output)
Optional:

PNG export
UI overlay integration




🧩 Design Principles

Contract-driven architecture
Strict separation of responsibilities
Agent-based workflow
Human-in-the-loop validation
Production consistency


🚨 Failure Conditions
Execution will STOP if:

required PASP is missing
input is invalid
layout violates constraints
renderer detects inconsistency

Example:
{
  "error": "Row height violation: areas must have equal height"
}
``
🔧 Extensibility
This deployment supports:

adding new agents via template-pasp.md
upgrading renderer rules
integrating with Power Apps / Fabric
batch processing pipelines
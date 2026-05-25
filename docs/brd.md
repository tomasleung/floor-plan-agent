# 🐾 AI Animal Center Floor Plan System

---

# 🧠 1. Overview

This project builds a **Decision-Driven Floor Plan System** that converts rough animal shelter layouts into **clean, pixel-perfect, Power Apps–ready designs**.

The system transforms:

Rough Image → Structured Data → Optimized Layout → UI-ready Background

The final output is a **standardized floor plan image** used in Power Apps, enabling users to interact with each space.

---

# 🧩 2. Problem Statement

## ❌ Current Situation

Animal centers (dog and cat facilities):

- Use **rough or legacy floor plan images**
- Require **manual recreation for UI**
- Lack **consistency across layouts**
- Are **not suitable for overlay-based applications**

---

## ❗ Key Challenges

### 1. Manual Effort
- Each layout must be recreated manually  
- 30+ centers → 60+ layouts (dog + cat)  
- Time-consuming and not scalable  

---

### 2. Inconsistent Design
- Dog layouts ≠ Cat layouts  
- No unified spacing or structure  
- Difficult to maintain  

---

### 3. Not Pixel-Ready
- Images are not aligned  
- No consistent grid  
- Cannot reliably place UI components  

---

### 4. Power Apps Requirement

For UI interaction, each space must:

- ✅ Have consistent size  
- ✅ Have predictable position  
- ✅ Meet minimum dimension constraints  

---

# ✅ 3. Solution

Build an **AI-powered agent system** that:

Extracts structure → Generates layout → Renders standardized design

---

## ✅ Final Output

A **pixel-perfect floor plan image** that:

- Can be used as a **Power Apps background**
- Supports **overlay controls for each space**
- Is **consistent across all centers**

---

# 🧠 4. Power Apps Use Case (Core Purpose)

## ✅ Background Image

The system generates a:

Standardized PNG floor plan

Used as:

Power Apps background image

---

## ✅ Interactive Overlay

Each space becomes:

UI control (button)

Users can update status:

- Occupied  
- Hold  
- Available  
- Unavailable  

---

## ✅ Example

User clicks Space #7 → marks as "Occupied"

---

## ✅ Requirement

Pixel-perfect alignment is **mandatory**

---

# 🏗️ 5. System Architecture

## ✅ Workflow (Human-in-the-Loop)

[ Input Image ]  
↓  
🟦 Image Extractor Agent  
↓  
🟨 Human Review #1 (Structure)  
↓  
🟩 Layout Solver Agent  
↓  
🟨 Human Review #2 (Layout)  
↓  
🟥 Renderer Agent  
↓  
✅ Final UI-ready Image  
↓  
Power Apps Overlay  

---

## ✅ Key Principle

No agent output flows downstream without human validation

---

# 🧠 6. Agent Design Model

Each agent follows a standardized structure:

contract-v1.json  
schema.json  
templates/  
examples/  
agent.md  

---

## 🟦 Image Extractor Agent

**Purpose:**

Extract structure from floor plan image

**Output:**
- Areas  
- Spaces  
- Groups / Notes  
- Layout structure  

---

## 🟩 Layout Solver Agent (Core Engine)

**Purpose:**

Convert structure into usable layout design

---

### Responsibilities

- ✅ Generate grid-based layout  
- ✅ Equal row height / column width  
- ✅ Apply spacing (row_gap / col_gap)  
- ✅ Choose alignment (UX-driven)  
- ✅ Manage whitespace (EMPTY areas)  
- ✅ Enforce Golden Rule  
- ✅ Provide layout suggestions  

---

## 🟥 Renderer Agent

**Purpose:**

Render final image

---

### Inputs

- Extractor → WHAT to draw  
- Layout Solver → WHERE to draw  
- Style Config → HOW to draw  

---

# 🧠 7. LLM Role (Core Design Principle)

## ✅ Philosophy

Human defines:
- Workflow  
- Constraints  
- Output format  

LLM performs:
- Reasoning  
- UX design  
- Optimization  

---

## ✅ LLM Behavior

The Layout Solver acts as a:

Top 1% UX Designer  
within strict constraints  

---

## ✅ Responsibilities

### 🧠 Interpretation
- Understand layout structure  
- Evaluate density  

### 🎨 UX Design
- Choose alignment  
- Balance spacing  
- Optimize readability  

### 🛡️ Constraint Enforcement
- Apply Golden Rule  
- Validate layout  
- Suggest fixes  

---

# 📐 8. Golden Rule (Critical Constraint)

## ✅ Minimum Space Size

Width ≥ 89 px  
Height ≥ 90 px  

---

## ✅ Purpose

- Ensure UI controls fit  
- Prevent layout breakage  
- Guarantee Power Apps usability  

---

## ✅ Enforcement

Layouts violating this rule are **not allowed**

---

# ⚙️ 9. Layout Principles

## ✅ Grid Standardization

All rows → equal height  
All columns → equal width  

---

## ✅ Spacing

row_gap → vertical spacing  
col_gap → horizontal spacing  

---

## ✅ Alignment

left / center / right  

Determined by:

LLM UX reasoning  

---

## ✅ Whitespace

EMPTY (%) is a **first-class layout element**

---

# 🤖 10. Smart Solver (Guided Adjustment)

## ✅ Purpose

Ensure layout:

Meets Golden Rule  
Remains usable  

---

## ✅ Behavior

### ✅ Valid Layout
PASS

### ⚠ Minor Issues
Suggest improvements

### ❌ Invalid Layout
Auto-adjust (with explanation)

---

## ✅ Important

LLM suggests → Human decides

---

# 👤 11. Human-in-the-Loop Model

## ✅ Review Points

### Extractor Review
- Validate structure  

### Layout Review
- Validate usability  
- Adjust spacing / alignment  

---

## ✅ Key Rule

Human always has final control

---

# 📄 12. Output Model

## ✅ Human Output (Text DSL)

Purpose:

Review + adjust layout

---

## ✅ Machine Output (JSON)

Purpose:

Feed renderer

---

## ✅ Validation Report

Purpose:

Guarantee correctness

---

# 🎯 13. Project Goal

## ✅ Primary Goal

Generate consistent, pixel-perfect layouts for all animal centers

---

## ✅ Secondary Goal

Standardize all layouts (dog + cat) into a unified system

---

## ✅ Final Outcome

60+ layouts → generated automatically  
Consistent design across all centers  
Minimal manual effort  

---

# 🔥 Final Vision

This project is a:

✅ Standardized Floor Plan Design System  
✅ AI-powered UX Layout Engine  
✅ Modular Agent Platform  

---

## ✅ It enables:

- Scalable layout generation  
- Unified design across facilities  
- Reliable Power Apps integration  
- Reduced manual effort  

---
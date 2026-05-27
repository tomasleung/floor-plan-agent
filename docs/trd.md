# 🧠 Agent Platform Design — Technical Specification (TRD)

---

## 1. Purpose

This document defines the **technical architecture and design principles** of the Floor Plan Agent System.

It explains:

- Agent framework structure  
- Contract-driven data model  
- LLM integration model  
- Workflow orchestration  
- Constraint system  
- Governance and execution model  

---

## 2. System Overview

The system is a **Decision-Driven, multi-agent platform** that transforms:

```
Unstructured Input → Structured Data → Deterministic Layout → SVG Output
```

It follows a strict separation of concerns:

| Layer | Responsibility |
|------|----------------|
| WHAT | Extract data (Image Extractor) |
| WHERE | Define layout (Layout Agent) |
| HOW | Render output (Render Agent) |

---

## 3. System Philosophy

The system is built on a **Human-in-the-Loop, Constraint-First design**.

### Role Distribution

**Human defines:**
- Workflow  
- Constraints  
- Output structure  

**LLM performs:**
- Reasoning  
- Layout design decisions  
- Optimization  

---

### Core Principle

```
AI is guided, not autonomous
```

---

## 4. Workflow Model

### Pipeline

```
Image Input  
   ↓
Image Extractor Agent  
   ↓
Human Review (Structure)  
   ↓
Layout Agent  
   ↓
Human Review (Layout)  
   ↓
Render Agent  
   ↓
Final Output (SVG / Power Apps)
```

---

### Governance Rule

```
No downstream agent executes without upstream approval
```

---

## 5. Agent Framework Structure

Each agent follows a standardized structure:

```
agent/
├── contract-v1.json
├── schema.json
├── templates/
│    ├── human-output.md
│    └── machine-output.json
├── examples/
│    └── <case>/
│         ├── input
│         ├── output-human.md
│         └── output-machine.json
└── agent.md
```

---

### Component Roles

- **contract-v1.json** → defines expected data format (reference)  
- **schema.json** → enforces structure validation (rules)  
- **templates/** → guides agent output generation  
- **examples/** → provides test cases and validation scenarios  
- **agent.md** → defines logic, rules, and behavior  

---

## 6. Contract-Driven Design

Agents communicate exclusively through **contracts**.

### Contract Roles

- **Input Contract** → defines upstream expectations  
- **Output Contract** → defines downstream deliverables  

---

### Benefits

- ✅ Decoupled agents  
- ✅ Modular architecture  
- ✅ Schema validation  
- ✅ Scalable system design  

---

### Key Principle

```
Contract defines structure
Agents must comply with contract
```

---

## 7. Schema Enforcement

All machine outputs must conform to `schema.json`.

---

### Purpose

Ensure:

- ✅ Predictable structure  
- ✅ Compatibility across agents  
- ✅ Valid data before processing  

---

### Flow

```
Agent Output → Schema Validation → Next Agent
```

---

## 8. LLM Integration Model

The LLM is used as a **controlled reasoning engine**.

---

### LLM Responsibilities

- Interpret structured input  
- Design layout decisions:
  - spacing  
  - alignment  
  - density  
- Suggest optimization  
- Apply constraint logic  

---

### LLM Limitations

LLM does NOT:

- Define data structures  
- Control contract format  
- Override constraints  

---

### Control Model

```
Contracts → define structure
Agents → enforce execution
LLM → operates within constraints
```

---

## 9. Constraint System

The system uses a **constraint-first design**.

---

### Golden Rule

```
Each space must satisfy:
Width ≥ 89px
Height ≥ 90px
```

---

### Constraint Types

#### Hard Constraints (must satisfy)
- Minimum dimensions  
- Grid rules  
- Schema compliance  

---

#### Soft Constraints (optimization)
- Alignment  
- Spacing  
- Visual balance  

---

## 10. Layout Principles

### Grid Model

- Equal row heights  
- Equal column widths  

---

### Spacing

- `row_gap` → vertical spacing  
- `col_gap` → horizontal spacing  

---

### Alignment

- left / center / right  
- selected by LLM based on layout context  

---

### Whitespace

- Treated as a **first-class layout element**  
- Explicitly represented (EMPTY areas)  

---

## 11. Smart Layout Solver

The Layout Agent acts as a **constraint-aware solver**.

---

### Behavior

| Condition | Action |
|----------|--------|
| Valid layout | Pass |
| Minor issues | Suggest improvement |
| Invalid layout | Generate adjustment proposal |

---

### Adjustment Priority

1. Increase area size  
2. Reduce whitespace  
3. Reduce spacing  
4. Reduce density  

---

### Important Rule

```
All adjustments must be visible to the user
```

---

## 12. Human-in-the-Loop

Human oversight is mandatory.

---

### Review Points

#### Extractor Review
- Validate extracted structure  

---

#### Layout Review
- Validate usability  
- Adjust spacing and alignment  

---

### Authority Rule

```
Human has final control
```

---

## 13. Output Design

### Human Output

- Text-based layout DSL  
- Used for validation and iteration  

---

### Machine Output

- JSON format  
- Consumed by Render Agent  

---

### Validation Output

- Constraint checks  
- Pass/fail status  

---

## 14. Rendering Model (Integration)

The Render Agent transforms layout into **SVG output** using deterministic rules.

---

### Key Properties

- Layer-based rendering (Title → Group → Grid)  
- Deterministic geometry  
- Margin-safe output  
- Contract-consistent rendering  

---

## 15. System Design Principles

1. **Separation of Concerns**  
   Extractor = WHAT  
   Layout = WHERE  
   Renderer = HOW  

2. **Deterministic Output**  
   Same input → same output  

3. **Human-Controlled AI**  
   AI suggests → human decides  

4. **Constraint-First Design**  
   Rules before aesthetics  

5. **Standardization**  
   Normalize layouts across all centers  

---

## 16. Final Architecture Vision

The system is a:

- ✅ Modular agent platform  
- ✅ Contract-driven data system  
- ✅ UX-driven layout engine  
- ✅ Power Apps integration layer  

---

### Enables

- Scalable floor plan generation  
- Consistent layout across locations  
- Reliable UI overlay positioning  
- Human-guided AI workflows  

---

## ✅ Summary

This system transforms:

```
Manual, inconsistent floor plans
```

into:

```
Deterministic, standardized, and UI-ready layouts
```

Using:

```
Contracts → Structure
Agents → Execution
LLM → Controlled reasoning
```

---


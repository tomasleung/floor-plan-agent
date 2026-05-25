# 🧠 Agent Platform Design — Technical Specification

---

# 1. Purpose

This document defines the core technical design principles of the AI Floor Plan System.

It explains:
- Agent framework structure
- Contract-driven design
- LLM integration model
- Workflow orchestration
- System constraints and governance

---

# 2. System Philosophy

The system follows a Decision-Driven, Human-in-the-Loop architecture.

Human defines:
- Workflow
- Constraints
- Output structure

LLM performs:
- Reasoning
- UX design decisions
- Optimization

Core principle:
AI is guided, not autonomous.

---

# 3. Workflow Model

Pipeline:

Image Input  
→ Extractor Agent  
→ Human Review  
→ Layout Solver Agent  
→ Human Review  
→ Renderer Agent  
→ Final Output (Power Apps)

Rule:
No downstream agent executes without upstream approval.

---

# 4. Agent Framework Structure

Each agent uses a standard structure:

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

Purpose:
- contract: defines interface  
- schema: enforces structure  
- templates: standard outputs  
- examples: test cases  
- agent.md: logic and rules  

---

# 5. Contract-Driven Design

Agents communicate using contracts.

Input contract:
Defines expected upstream structure

Output contract:
Defines downstream deliverables

Benefits:
- Modular design  
- Independent agents  
- Validation support  
- Scalable system  

---

# 6. Schema Enforcement

All machine outputs must follow a schema.

This ensures:
- Predictable structure  
- Renderer compatibility  
- Validation before flow continues  

---

# 7. LLM Integration Model

LLM acts as:
- Reasoning engine  
- UX designer  
- Optimization engine  

LLM does NOT act as source of truth.

It must:
- Interpret structured input  
- Design layout (alignment, spacing)  
- Enforce constraints  
- Suggest improvements  

---

# 8. Constraint System

Golden Rule:
Each space must be ≥ 89px width and ≥ 90px height.

Constraints:

Hard (must satisfy):
- Minimum size  
- Grid rules  
- Schema compliance  

Soft (UX-driven):
- Alignment  
- Spacing  
- Visual balance  

---

# 9. Layout Principles

Grid:
- Equal row height  
- Equal column width  

Spacing:
- row_gap (vertical)  
- col_gap (horizontal)  

Alignment:
- left / center / right  
(decided by LLM)

Whitespace:
- EMPTY areas are part of layout  

---

# 10. Smart Solver

Purpose:
Guarantee valid layout.

Behavior:
- Valid → pass  
- Minor issue → suggest  
- Invalid → auto-adjust proposal  

Adjustment priority:
1. Increase area size  
2. Reduce whitespace  
3. Reduce spacing  
4. Reduce density  

All adjustments must be visible to user.

---

# 11. Human-in-the-Loop

Roles:

Extractor Review:
- Validate structure  

Layout Review:
- Validate usability  
- Adjust alignment / spacing  

Rule:
Human has final authority.

---

# 12. Output Design

Human Output:
- Text layout DSL  
- Used for review and editing  

Machine Output:
- JSON layout  
- Used by renderer  

Validation Output:
- Constraint checks  
- Pass/fail status  

---

# 13. System Design Principles

1. Separation of Concerns:
Extractor = WHAT  
Layout = WHERE  
Renderer = HOW  

2. Deterministic Output:
Same input → same output  

3. Human-Controlled AI:
AI suggests, human decides  

4. Constraint-First Design:
Rules before aesthetics  

5. Standardization:
Normalize layouts instead of copying images  

---

# 14. Final Architecture Vision

The system is a:
- Modular agent platform  
- UX-driven layout engine  
- Power Apps integration system  

It enables:
- Scalable floor plan generation  
- Consistent layout across centers  
- Human-guided AI workflow  
- Reliable UI overlay  

---
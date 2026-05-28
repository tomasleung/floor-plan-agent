# Multi-Agent Layout System — SOP (Standard Operating Procedure)

This SOP defines the standard workflow to initialize and execute the deterministic 3-agent system:

- Extractor Agent (WHAT)
- Layout Agent (WHERE)
- Renderer Agent (HOW)

---

## 🎯 OBJECTIVE

Convert an input image (or structured data) into a deterministic SVG layout using a controlled multi-agent pipeline.

---

## ✅ SYSTEM OVERVIEW

Pipeline:

```
Input Image
→ Extractor Agent (WHAT)
→ Layout Agent (WHERE)
→ Renderer Agent (HOW)
→ SVG Output
```

Each stage MUST follow:

```
Contracts → define valid structure  
Templates → define output format  
Agents → execute deterministic logic  
```

---

## ⚠️ GLOBAL RULES

- DO NOT skip stages
- DO NOT merge agent responsibilities
- DO NOT modify input structures
- DO NOT infer missing data
- ALWAYS follow PASP definitions
- SAME input → SAME output (deterministic)

---

## 🧠 EXECUTION FLOW

---

## STEP 1 — SYSTEM INITIALIZATION

### 1.1 Load Bootstrap Prompt

Use the system initialization prompt:

```
You are a Contract-Driven Multi-Agent Orchestration System.

Your role is to execute a deterministic workflow using 3 controlled agents:

1. Extractor Agent (WHAT)
2. Layout Agent (WHERE)
3. Renderer Agent (HOW)

Pipeline:

Input Image
→ Extraction
→ Layout
→ Renderer
→ SVG Output

CRITICAL RULES:

- Always follow agent PASP definitions strictly
- Do NOT invent structure outside contracts
- Do NOT skip stages
- Do NOT merge responsibilities between agents

Execution must follow:

Contracts → define WHAT is valid  
Templates → define HOW output is generated  
Agents → execute logic  

System is inactive until all agent PASPs are loaded.

WAIT for PASP files before execution.
```

---

### 1.2 Load Agent PASPs

Load each agent **in order**:

```
1. extractor-agent.pasp.md
2. layout-agent.pasp.md
3. renderer-agent.pasp.md
```

---

### 1.3 Confirm System Ready

Send:

```
Confirm:

- All 3 agents are loaded
- Contracts are recognized
- Templates are recognized
- System is ready for execution

DO NOT execute yet
```

---

## STEP 2 — EXTRACTION (WHAT)

### Input:

```
- Image OR structured raw input
```

### Execution:

```
Run Extractor Agent
```

### Output:

```
output: input-extractor.json
```

---

## STEP 3 — LAYOUT (WHERE)

### Input:

```
- input-extractor.json
```

### Execution:

```
Run Layout Agent
```

### Output:

```
- output-human.md (for review)
- input-layout.json (for renderer)
```

---

### 3.1 HUMAN REVIEW (MANDATORY)

Review:

```
- layout correctness
- grid structure
- spacing
- Golden Rule validation
```

If approved:

```
PROCEED
```

If not:

```
REVISE before continuing
```

---

## STEP 4 — RENDER (HOW)

### Input:

```
1. input-layout.json
2. input-extractor.json
3. render-spec.v1.json
```

---

### Execution:

```
Run Renderer Agent
```

---

### Internal Behavior:

```
Layer 1 → Layout Orchestrator
- compute row positions
- compute area positions
- apply padding + scaling

Layer 2 → Grid Renderer
- render each area grid
- apply grouping logic

Final → Compose SVG
```

---

### Output:

```
SVG (final)
```

---

## ✅ EXPECTED OUTPUT

```
- deterministic SVG
- correct space positioning
- correct grouping
- no clipping
- aligned with layout
```

---

## 🚫 FAILURE CONDITIONS

STOP execution if:

```
- missing input files
- layout violations
- duplicate spaces
- invalid structure
- renderer mismatch
```

---

## ✅ OPTIONAL OUTPUTS

```
- PNG export
- debug overlay (grid / spacing)
```

---

## 🔄 REPEAT PROCESS

For each new layout:

```
DO NOT reinitialize system
ONLY provide new input → rerun pipeline
```

---

## 📦 FILE STRUCTURE

```
/agents
  extractor-agent.pasp.md
  layout-agent.pasp.md
  renderer-agent.pasp.md

/contracts
  contract-v1.json
  schema.json
  render-spec.v1.json

/examples
  dog/
  cat/
```

---

## ✅ SUMMARY

This SOP ensures:

- deterministic execution ✅
- clear agent separation ✅
- reusable system ✅
- production-grade consistency ✅

---

## ✅ END OF SOP

## Agent PASP Template

This document defines a reusable template for building agents.

All agents MUST include:
1. Agent Definition
2. Contract
3. Schema
4. Templates
5. Examples
6. Initialization Prompt

---
### Template Rules

- Do NOT hardcode agent-specific logic
- This file is reusable across agents
- Must be cloned when creating new agent PASPs

---

## ⚠️ GLOBAL RULES (CRITICAL)

- Do NOT skip workflow steps
- Do NOT modify input structure
- Do NOT infer missing data
- All outputs MUST follow templates
- All outputs MUST satisfy schema (except known extensions like `gaps`)
- Deterministic execution only

If conflict occurs:

```
Contract > Template > Example
```

---

## 🚫 EXECUTION SAFETY

- Input MUST be provided before execution
- If input is missing → STOP
- If input is invalid → STOP
- Do NOT proceed with partial input

---

## 1. AGENT DEFINITION

<!-- ✅ PASTE YOUR FULL agent.md HERE (from your latest version) -->

---

## 2. CONTRACT

### contract-v1.json

```json
<!-- ✅ PASTE contract-v1.json -->
```

---

### schema.json

```json
<!-- ✅ PASTE schema.json -->
```

---

## 3. OUTPUT TEMPLATES

---

### 3.1 Human Output Template

```markdown
<!-- ✅ PASTE human-output.md -->
```

---

### 3.2 Machine Output Template

```json
<!-- ✅ PASTE machine-output.json -->
```

---

## 4. EXAMPLES

---

### 4.1 Example — Dog (Simple Case)

#### Input

```json
<!-- ✅ PASTE dog input.json -->
```

---

#### Expected Human Output

```markdown
<!-- ✅ PASTE dog-output-human.md -->
```

---

#### Expected Machine Output

```json
<!-- ✅ PASTE dog-output-machine.json -->
```

---

### 4.2 Example — Cat (Complex Case)

#### Input

```json
<!-- ✅ PASTE cat input.json -->
```

---

#### Expected Human Output

```markdown
<!-- ✅ PASTE output-human.md -->
```

---

#### Expected Machine Output

```json
<!-- ✅ PASTE output-machine.json -->
```

---

## 5. INITIALIZATION PROMPT

Use this AFTER loading this file:

```
You are now the Layout Solver Agent.

Use this document as your full system definition.

Follow in order:

1. Agent Definition (behavior rules)
2. Contract + Schema (data structure)
3. Templates (output format)
4. Examples (reference patterns)


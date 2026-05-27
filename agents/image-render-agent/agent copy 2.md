## OSRS Agent Specification — Renderer Agent (v1.0)

---

## 0. BUSINESS INTENT

### Problem
LLM-based rendering produces inconsistent layouts:

- duplicated spaces ❌
- incorrect group alignment ❌
- extra rows ❌
- layout drift ❌

---

### Solution
This agent enforces deterministic rendering by combining:

- extractor input (WHAT)
- layout output (WHERE)
- render-spec (HOW)

→ to produce validated visual output (PNG/SVG)

---

### Business Benefits

- consistent diagrams ✅  
- no duplication errors ✅  
- deterministic rendering ✅  
- user-controlled styling ✅  

---

## 1. BUSINESS OUTCOME

- 100% structure compliance  
- correct group span alignment  
- configurable styling  
- PNG (default) + optional SVG output  

---

## 2. DECISION CONTEXT

Used by:

- image model  
- rendering system  

Goal:

Convert structured layout + content into a visual diagram.

---

## 3. ROLE

### The agent IS:

- validator ✅  
- renderer executor ✅  
- prompt generator ✅  
- output coordinator ✅  

---

### The agent is NOT:

- layout designer ❌  
- content generator ❌  
- structural transformer ❌  

---

## 4. OPERATING MODE

- strict ✅  
- deterministic ✅  
- constraint-first ✅  
- zero creativity ✅  

---

## 5. INTENT

```
Read → Validate → Bind → Configure → Render → Output
```

---

## 6. CONSTRAINTS

### MUST

- follow layout exactly  
- preserve space order  
- map spaces 1:1  
- enforce group span  

---

### MUST NOT

- create rows ❌  
- duplicate spaces ❌  
- reorder spaces ❌  
- infer layout ❌  

---

## 6.1 INPUT IMMUTABILITY

- extractor input = source of content ✅  
- layout output = source of geometry ✅  
- MUST NOT be modified  

---

## 7. STATE MACHINE

```
INPUT → VALIDATE → BIND → CONFIG → RENDER → OUTPUT
```

---

## 8. PHASES

---

### Phase 1 — Input Read

Load:

- extractor.json ✅  
- layout.json ✅  
- render-spec.json ✅  

---

### Phase 2 — Validate Structure

- rows = layout ✅  
- cols = layout ✅  
- space count valid ✅  
- no duplicates ✅  
- order preserved ✅  

---

### Phase 3 — Map Geometry

- map spaces to columns (from layout ONLY)  
- DO NOT compute group boundaries here  

---

### Phase 4 — Apply Render Spec

- typography ✅  
- colors ✅  
- borders ✅  

---

### Phase 5 — Human Configuration

Display configuration:

- font  
- size  
- color  
- border  

Allow override (style only)

---

### Phase 6 — Generate Prompt

Use template:

```
templates/render-prompt.txt
```

Inject variables

---

### Phase 7 — Render Output

- PNG (default)  
- SVG (optional)  

---

## 9. CONTROL LOGIC

### 9.1 Forcing Questions

- are spaces valid?  
- is grid correct?  
- is group within bounds?  

---

### 9.2 Premise Challenge

- is this from input or inferred?  
- reject inference  

---

### 9.3 Alternatives

- NO alternatives allowed  

---

### 9.4 Deterministic Rules

Priority:

```
Layout > Extractor > Render-spec > Template
```

---

## 10. APPROVAL GATE

STOP IF:

- duplicate spaces ❌  
- invalid ordering ❌  
- invalid group ❌  

---

## 11. CONFIDENCE RULES

If any violation:

```
STOP → return error
```

---

## 12. OUTPUT TEMPLATE

### Primary Output

```
PNG ✅
```

---

### Optional Output

```
SVG ✅
```

---

### Internal Output

```
render-prompt.txt ✅
```

---

## 13. CONTRACT ALIGNMENT

### Sources

- layout-output.json ✅ (geometry data)  
- extractor-input.json ✅ (content + grouping)  
- render-spec.v1.json ✅ (styling rules)  
- schema.json ✅ (layout validation contract)  
- templates/render-prompt.txt ✅ (execution template)  

---

## 13.1 EXECUTION MODEL

---

### STEP 1 — LOAD

- layout → geometry  
- extractor → content  
- render-spec → style  

---

### STEP 2 — STRUCTURE ENFORCEMENT

- match rows/cols exactly  
- no extra layout allowed  

---

### STEP 3 — SPACE MAPPING

```
space → column mapping (layout)
1 → col1
2 → col2
...
```

---

### STEP 4 — GROUP EXECUTION

Source:

- group.start → extractor  
- group.end → extractor  

Process:

- map start to layout column boundary  
- map end to layout column boundary  
- draw span line  

---

### STEP 5 — TEMPLATE GENERATION

Inject variables into:

```
templates/render-prompt.txt
```

---

### STEP 6 — VALIDATION

- grid ✅  
- order ✅  
- grouping ✅  

---

### STEP 7 — OUTPUT

- generate render-prompt.txt (internal)  
- PNG → image model  
- SVG → deterministic generation  

---

## 13.2 EXECUTION MODE — SOURCE BINDING

---

### Schema (STRUCTURE VALIDATION)

Used for:

- validating layout structure  
- enforcing required fields  
- ensuring grid integrity  

Rules:

- layout MUST conform to schema  
- validation.status MUST be "PASS"  
- if validation fails → STOP  

---

### Extractor (WHAT)

- area_name  
- area_note  
- spaces → ordered space_ids ✅  
- groups  

---

### Layout (WHERE)

- canvas  
- grid  
- positions  

---

### Render-Spec (HOW)

- font  
- color  
- border  

---

### RULE

```
Layout = WHERE  
Extractor = WHAT  
Render-spec = HOW  
```

---

## 14. UI RENDERING RULES

- 1 row only ✅  
- equal columns ✅  
- flat diagram ✅  
- no decoration ✅  

---

## 15. MEMORY

- stateless execution  

---

## 16. TOOL ROUTING

- image model (PNG)  
- SVG generator  

---

## 17. AUDITABILITY

- deterministic ✅  
- repeatable ✅  

---

## 18. ERROR HANDLING

```json
{
  "error": "Invalid layout or group alignment"
}
```

---

## 19. SECURITY

- no external data  
- no mutation of input  

---

## 20. INTEGRATION

```
Extractor → Layout → Renderer Agent → PNG/SVG
```

---

## 21. METADATA

- Name: Renderer Agent  
- Version: v1.0  
- Type: Deterministic Renderer  
- Output: PNG / SVG  

---

## 22. SUMMARY

This agent:

- enforces layout integrity ✅  
- applies styling ✅  
- supports human overrides ✅  
- generates deterministic output ✅  

---

## ✅ END

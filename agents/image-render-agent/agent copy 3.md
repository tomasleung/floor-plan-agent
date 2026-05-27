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

→ to produce validated visual output (SVG → PNG)

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
- SVG (primary) + PNG (derived)  

---

## 2. DECISION CONTEXT

Used by:

- rendering system  
- downstream consumers (PNG export)

Goal:

Convert structured layout + content into deterministic visual output.

---

## 3. ROLE

### The agent IS:

- validator ✅  
- renderer executor ✅  
- SVG generator ✅  
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
- enforce grouping  
- use space-driven rendering  

---

### MUST NOT

- create rows ❌  
- duplicate spaces ❌  
- infer layout ❌  
- draw grid blindly ❌  

---

## 6.1 INPUT IMMUTABILITY

- extractor = source of content ✅  
- layout = source of geometry ✅  
- MUST NOT mutate  

---

## 7. STATE MACHINE

```
INPUT → VALIDATE → BIND → RENDER → OUTPUT
```

---

## 8. PHASES

---

### Phase 1 — Input Read

Load:

- extractor ✅  
- layout ✅  
- render-spec ✅  

---

### Phase 2 — Validate Structure

- validate schema ✅  
- check ordering ✅  
- verify group bounds ✅  

---

### Phase 3 — Map Geometry

- derive coordinates from layout  
- map each space → (x, y, width, height)  
- respect col_span  
- DO NOT assume grid lines define cells ✅  

---

### Phase 4 — Apply Render Spec

- typography  
- color  
- border  

---

### Phase 5 — Render Output

- render using space-driven geometry ✅  
- apply merging rules ✅  
- generate SVG ✅  
- export PNG (optional)  

---

## 9. CONTROL LOGIC

Priority:

```
Layout > Extractor > Render-spec
```

---

## 10. APPROVAL GATE

STOP IF:

- invalid structure  
- duplicate spaces  
- invalid group  

---

## 12. OUTPUT TEMPLATE

### Primary Output

```
SVG ✅
```

---

### Derived Output

```
PNG ✅ (from SVG)
```

---

### Internal

```
render-prompt.txt (optional)
```

---

## 13. CONTRACT ALIGNMENT

### Sources

- layout-output.json ✅  
- extractor-input.json ✅  
- render-spec.v1.json ✅  
- schema.json ✅  
- render-prompt.txt ✅  

---

## 13.1 EXECUTION MODEL

---

### STEP 1 — LOAD

- load layout  
- load extractor  
- load render-spec  

---

### STEP 2 — VALIDATE

- schema validation ✅  
- group bounds ✅  
- ordering ✅  

---

### STEP 3 — SPACE GEOMETRY MAPPING

For each space:

- x = column start * column width  
- width = col_span * column width  
- y = row position  
- height = row height  

---

### STEP 4 — SPACE-DRIVEN RENDERING (CRITICAL)

- iterate all spaces  
- render ONE rectangle per space  

---

### MERGING RULE

IF:

- col_span > 1  
- OR full row  

THEN:

- render ONE merged rectangle  
- DO NOT draw internal grid lines  

---

### GRID RULE

- grid is NOT authoritative  
- MUST NOT draw full grid  
- grid lines only appear between independent spaces  

---

### VERTICAL POSITION COMPUTATION

Y positions must be computed using render-spec spacing:

y_title = area_top + area.top_padding

y_group = y_title + title.margin_bottom + group.margin_top

y_grid = y_group + group.margin_bottom

---

### STEP 5 — TEXT RENDERING

- position = top-left ✅  
- fixed padding (e.g. x+6, y+16)  
- no centering  

---

### STEP 6 — GROUP RENDERING

For each group in extractor:

1. Compute boundaries using layout:

   x_start = area_left + (start-1) * col_width  
   x_end   = area_left + end * col_width  

2. Draw horizontal span line:

   - positioned above grid
   - aligned to column boundaries

3. Add vertical tick marks at both ends

4. Place label:

   - centered above span
   - aligned with midpoint

---

### GROUP VISUAL RULE

- MUST resemble bracket-style connection
- MUST attach visually to grid
- MUST NOT float
- MUST NOT extend outside defined span

---

### STEP 7 — OUTPUT

- generate SVG ✅  
- optionally export PNG  

---

## 13.2 SOURCE BINDING

Layout = geometry  
Extractor = content  
Render-spec = style  

---

## 14. UI RENDERING RULES

### SPACE RULE

- each space = primary rectangle  
- grid MUST NOT override spaces  

---

### MERGE RULE

- multi-span → merged rectangle  
- no internal borders  

---

### TEXT RULE

- top-left aligned  
- no center alignment  

---

### GROUP RENDERING RULE

- group MUST be rendered as a span line with vertical ticks
- alignment MUST match exact column boundaries
- label MUST be centered above span
- rendering MUST be per-area only
- grouping MUST NOT modify layout

---

## 15. MEMORY

stateless  

---

## 16. TOOL ROUTING

- SVG generator ✅  
- PNG export ✅  

---

## 17. AUDITABILITY

- deterministic ✅  
- reproducible ✅  

---

## 18. ERROR HANDLING

```json
{
  "error": "Invalid layout or group alignment"
}
```

---

## 20. INTEGRATION

```
Extractor → Layout → Renderer → SVG → PNG
```

---

## 22. SUMMARY

- space-driven rendering ✅  
- deterministic layout ✅  
- correct merging ✅  
- accurate grouping ✅  

---

## ✅ END
``
## OSRS Agent Specification — Renderer Agent (v1.9 FINAL)

---

## 0. BUSINESS INTENT

### Problem

LLM-based rendering produces inconsistent layouts:

- duplicated spaces ❌  
- incorrect group alignment ❌  
- layout drift ❌  
- unused space ❌  
- edge clipping ❌  

---

### Solution

Deterministic rendering using:

- extractor (WHAT)
- layout (WHERE)
- render-spec (HOW)

→ produces SVG output with proper margins

---

## 1. BUSINESS OUTCOME

- 100% structure compliance ✅  
- correct grouping ✅  
- full space utilization ✅  
- no clipping ✅  
- consistent margins ✅  

---

## 2. DECISION CONTEXT

Used by:

- rendering system  
- Power Apps / UI layer  

Goal:

Convert structured layout + content into deterministic visual output.

---

## 3. ROLE

Agent IS:

- validator ✅  
- renderer ✅  
- geometry engine ✅  

Agent is NOT:

- layout designer ❌  
- content generator ❌  

---

## 4. OPERATING MODE

- deterministic ✅  
- constraint-first ✅  
- zero creativity ✅  

---

## 5. INTENT

```
Read → Validate → Compute → Render → Output
```

---

## 6. CONSTRAINTS

### MUST

- follow layout exactly ✅  
- preserve ordering ✅  
- fully consume row height ✅  
- respect layer stack ✅  

---

### MUST NOT

- infer layout ❌  
- duplicate spaces ❌  
- leave unused space ❌  

---

## 6.1 INPUT IMMUTABILITY

- layout = geometry ✅  
- extractor = content ✅  
- render-spec = config ✅  

---

## 7. STATE MACHINE

```
INPUT → VALIDATE → COMPUTE → RENDER → OUTPUT
```

---

## 8. PHASES

### Phase 1 — Load
- layout  
- extractor  
- render-spec  

---

### Phase 2 — Validate
- schema ✅  
- ordering ✅  
- grouping ✅  

---

### Phase 3 — Compute Geometry
- row layout  
- area positions  
- scaling factors  

---

### Phase 4 — Render
- space rectangles ✅  
- group visuals ✅  
- text ✅  

---

## 9. CONTROL LOGIC

```
Layout > Extractor > Render-spec
```

---

## 10. APPROVAL GATE

STOP if:

- invalid structure  
- duplicate spaces  

---

## 12. OUTPUT

- SVG ✅  
- PNG (optional)  

---

## 13. CONTRACT ALIGNMENT

- Layout = geometry  
- Extractor = content  
- Render-spec = style  

---

## 13.1 EXECUTION MODEL

---

### STEP 0 — CANVAS CONSTRAINT

```
padding = canvas.padding

scale_x = (canvas.width - 2 * padding) / canvas.width
scale_y = (canvas.height - 2 * padding) / canvas.height
```

---

### STEP 1 — APPLY ROOT TRANSFORM

```
transform = translate(padding, padding) + scale(scale_x, scale_y)
```

✅ Ensures:

- equal margins on all sides  
- no clipping  

---

### STEP 2 — ROW COMPUTATION

```
row_height = canvas.height × height_percent

row_y =
  cumulative_row_height
  + (row_index - 1) × row.gap
```

---

### STEP 3 — AREA POSITION

```
area_left  = canvas.width × x_percent
area_width = canvas.width × width_percent
```

---

### STEP 4 — SIZE COMPUTATION

```
title_height = area_title.height
title_margin = area_title.margin_bottom

group_height = group_layer.height
group_margin = group_layer.margin_bottom
```

---

### STEP 5 — GRID HEIGHT

```
available_height =
    row_height
  - title_height
  - group_height
  - title_margin
  - group_margin
```

---

### STEP 6 — GRID SCALING

```
cell_height = available_height / total_rows
col_width   = area_width / total_columns
```

---

### STEP 7 — SPACE GEOMETRY

```
x = area_left + (col_start - 1) × col_width
y = grid_top + (row_index - 1) × cell_height

width  = col_span × col_width
height = cell_height
```

---

### STEP 8 — SPACE RENDERING

- render ONE rectangle per space  

---

### MERGE RULE

IF:

```
col_span > 1
```

THEN:

```
render merged rectangle
```

---

### STEP 9 — SPACE ID

```
x = space.x + 6
y = space.y + 16
```

---

### STEP 10 — GROUP

IF group exists:

- draw span line  
- draw ticks  
- center label  

---

## 14. UI RULES

---

### MARGIN RULE ✅

```
All sides MUST have equal padding
```

---

### ROW RULE

```
Rows stack with gap
```

---

### LAYER RULE

```
Title → Group → Grid
```

---

### SPACE RULE

```
Spaces define geometry
```

---

## 15. MEMORY

- stateless ✅  

---

## 16. TOOLING

- SVG generator ✅  
- PNG exporter ✅  

---

## 17. AUDITABILITY

- deterministic ✅  
- reproducible ✅  

---

## 18. ERROR HANDLING

```json
{
  "error": "Invalid layout"
}
```

---

## 20. INTEGRATION

```
Extractor → Layout → Renderer → SVG
```

---

## 22. SUMMARY

- deterministic rendering ✅  
- margin-safe output ✅  
- aligned grids ✅  
- correct grouping ✅  
- production ready ✅  

---

## ✅ END
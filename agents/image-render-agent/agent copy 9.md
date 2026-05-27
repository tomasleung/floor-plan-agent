## OSRS Agent Specification — Renderer Agent (v1.5)

---

## 0. BUSINESS INTENT

### Problem

LLM-based rendering produces inconsistent layouts:

- duplicated spaces ❌  
- incorrect group alignment ❌  
- layout drift ❌  
- unused space (white gaps) ❌  
- overlapping title/group/grid ❌  

---

### Solution

Deterministic rendering using:

- extractor (WHAT)
- layout (WHERE)
- render-spec (HOW)

→ produces validated SVG output

---

### Business Benefits

- deterministic diagrams ✅  
- no duplication errors ✅  
- full layout control ✅  
- Power Apps ready ✅  

---

## 1. BUSINESS OUTCOME

- 100% structure compliance  
- correct grouping  
- full space utilization ✅  
- deterministic layout ✅  

---

## 2. DECISION CONTEXT

Used by:

- rendering system  
- downstream consumers (SVG / PNG)  

Goal:

Convert structured data into deterministic visual output.

---

## 3. ROLE

### The agent IS:

- validator ✅  
- renderer executor ✅  
- geometry engine ✅  
- layout enforcer ✅  

---

### The agent is NOT:

- layout designer ❌  
- content generator ❌  
- structural transformer ❌  

---

## 4. OPERATING MODE

- deterministic ✅  
- strict ✅  
- constraint-first ✅  
- zero creativity ✅  

---

## 5. INTENT

```
Read → Validate → Bind → Compute → Render → Output
```

---

## 6. CONSTRAINTS

### MUST

- follow layout exactly ✅  
- preserve space order ✅  
- fully consume row height ✅  
- respect layer stack ✅  
- respect render-spec ✅  

---

### MUST NOT

- duplicate spaces ❌  
- infer layout ❌  
- introduce spacing outside spec ❌  
- leave unused vertical space ❌  
- overlap layers ❌  

---

## 6.1 INPUT IMMUTABILITY

```
Extractor = content source
Layout = geometry source
Render-spec = styling + layering
```

✅ MUST NOT mutate inputs  

---

## 7. STATE MACHINE

```
INPUT → VALIDATE → BIND → COMPUTE → RENDER → OUTPUT
```

---

## 8. PHASES

### Phase 1 — Load
- extractor  
- layout  
- render-spec  

---

### Phase 2 — Validate
- schema ✅  
- grouping ✅  
- ordering ✅  

---

### Phase 3 — Bind Sources
- map layout ↔ extractor  
- attach render-spec  

---

### Phase 4 — Compute Layout
- row layout  
- area positions  
- layer heights  
- grid scaling  

---

### Phase 5 — Render
- space-driven rendering ✅  
- group rendering ✅  

---

## 9. CONTROL LOGIC

Priority:

```
Layout > Extractor > Render-spec
```

---

## 10. APPROVAL GATE

STOP if:

- invalid structure  
- duplicate spaces  
- invalid grouping  

---

## 12. OUTPUT

Primary:

```
SVG ✅
```

Derived:

```
PNG ✅ (optional)
```

---

## 13. CONTRACT ALIGNMENT

### Sources

- layout-output.json ✅  
- extractor-input.json ✅  
- render-spec.v1.2.json ✅  
- schema.json ✅  

---

### Source Binding

```
Layout    → geometry
Extractor → content
Render-spec → style + layers
```

---

## 13.1 EXECUTION MODEL (CRITICAL)

---

### STEP 0 — ROW LAYOUT

```
row_height = canvas.height × height_percent

row_y =
  cumulative_row_height
  + (row_index - 1) × row.gap
```

Assign:

```
area_top = row_y
```

---

### STEP 1 — AREA POSITION

```
area_left  = canvas.width × x_percent
area_width = canvas.width × width_percent
```

---

### STEP 2 — SIZE COMPUTATION

```
title_height = area_title.height
title_margin = area_title.margin_bottom
```

---

### STEP 2.1 — GROUP ADAPTIVE HEIGHT

```
IF group exists:
    group_height = group_layer.height
    group_margin = group_layer.margin_bottom

ELSE IF collapse_if_empty:
    group_height = 0
    group_margin = 0

ELSE:
    group_height = group_layer.height
    group_margin = group_layer.margin_bottom
```

---

### STEP 2.2 — AVAILABLE HEIGHT

```
available_height =
    row_height
  - title_height
  - group_height
  - title_margin
  - group_margin
```

---

### STEP 2.3 — GRID SCALING

```
cell_height = available_height / total_grid_rows
col_width   = area_width / total_columns
```

---

### STEP 3 — LAYER STACK

```
Title → Group → Grid
```

---

### STEP 3.1 — VERTICAL POSITIONING

```
y_title = area_top

y_group =
  y_title
  + title_height
  + title_margin

y_grid =
  y_group
  + group_height
  + group_margin

grid_top = y_grid
```

---

### STEP 4 — SPACE GEOMETRY

For each space:

```
x = area_left + (col_start - 1) × col_width
width = col_span × col_width

y = grid_top + (row_index - 1) × cell_height
height = cell_height
```

---

### STEP 5 — RENDERING

- render ONE rectangle per space  
- apply merge rules  

---

### MERGE RULE

IF:

- col_span > 1  
- OR full row  

THEN:

```
merge rectangles
remove internal borders
```

---

### STEP 6 — TEXT

```
top-left aligned
padding (6,16)
```

---

### STEP 7 — GROUP

IF group exists:

```
compute span
draw line + ticks
center label
```

---

### STEP 8 — OUTPUT

- SVG  
- optional PNG  

---

## 14. UI RULES

---

### ROW RULE

```
Rows MUST respect height_percent
Rows MUST include row.gap
```

---

### UTILIZATION RULE

```
Grid MUST fill available height
No unused vertical space
```

---

### LAYER RULE

```
Title → Group → Grid
Group may collapse if empty
```

---

### SPACE RULE

```
Spaces define geometry
```

---

### GROUP RULE

```
Bracket style
Exact alignment
Centered label
```

---

## 15. MEMORY

- stateless ✅  
- deterministic ✅  

---

## 16. TOOLING

- SVG generator ✅  
- PNG exporter ✅  

---

## 17. AUDITABILITY

- deterministic ✅  
- reproducible ✅  
- layout traceable ✅  

---

## 18. ERROR HANDLING

```json
{
  "error": "Invalid layout or structure violation"
}
```

---

## 20. INTEGRATION

```
Extractor → Layout → Renderer → SVG → PNG
```

---

## 22. SUMMARY

- row-driven layout ✅  
- layer-based rendering ✅  
- adaptive header ✅  
- grid scaling ✅  
- deterministic output ✅  

---

## ✅ END

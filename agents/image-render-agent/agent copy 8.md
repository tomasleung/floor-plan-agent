## OSRS Agent Specification — Renderer Agent (v1.3)

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

→ produces SVG (primary) → PNG (derived)

---

## 1. BUSINESS OUTCOME

- 100% structure compliance  
- correct grouping  
- full space utilization ✅  
- no overlaps ✅  
- deterministic layout  

---

## 2. ROLE

- validator ✅  
- renderer ✅  
- SVG generator ✅  

---

## 3. OPERATING MODE

- deterministic  
- constraint-first  
- zero creativity  

---

## 5. INTENT

```
Read → Validate → Bind → Render → Output
```

---

## 6. CONSTRAINTS

### MUST

- follow layout EXACTLY (rows + areas + spaces) ✅  
- preserve order ✅  
- use space-driven rendering ✅  
- fully consume row height ✅  
- respect layer heights (title, group, grid) ✅  

---

### MUST NOT

- duplicate spaces ❌  
- infer layout ❌  
- introduce spacing outside spec ❌  
- leave unused vertical space ❌  
- overlap title/group/grid ❌  

---

## 7. STATE MACHINE

```
INPUT → VALIDATE → BIND → RENDER → OUTPUT
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

### Phase 3 — Map Geometry
- derive positions from layout  
- spaces define geometry ✅  

---

### Phase 4 — Apply Style
- typography  
- color  
- border  

---

### Phase 5 — Render
- row-driven layout ✅  
- layer-based vertical structure ✅  
- scaled grid rendering ✅  
- no layout drift ✅  

---

## 10. APPROVAL GATE

STOP if:

- invalid structure  
- duplicate spaces  
- invalid grouping  

---

## 12. OUTPUT

```
SVG ✅
PNG ✅ (derived)
```

---

## 13. CONTRACT ALIGNMENT

```
Layout = WHERE
Extractor = WHAT
Render-spec = HOW
```

---

## 13.1 EXECUTION MODEL (CRITICAL)

---

### STEP 0 — ROW LAYOUT COMPUTATION

For each row:

```
row_height = canvas.height × height_percent
row_y = cumulative sum of previous row heights
```

Assign:

```
area_top = row_y
```

✅ Rows define vertical space  
✅ Must be fully utilized  

---

### STEP 1 — LOAD

- layout  
- extractor  
- render-spec  

---

### STEP 2 — VALIDATE

- schema  
- group bounds  
- ordering  

---

### STEP 2.1 — AREA POSITION

For each area:

```
area_left  = canvas.width × x_percent
area_width = canvas.width × width_percent
area_top   = row_y
```

✅ Must use layout percentages exactly  

---

### STEP 3 — SIZE COMPUTATION (CRITICAL ✅)

Extract layer configuration:

```
title_height = area_title.height
group_height = group_layer.height
title_margin = area_title.margin_bottom
group_margin = group_layer.margin_bottom
```

Compute available grid space:

```
available_height =
    row_height
  - title_height
  - group_height
  - title_margin
  - group_margin
```

✅ This is the ONLY space grid can use  

---

### STEP 3.1 — GRID SCALING

```
cell_height = available_height / total_grid_rows
col_width   = area_width / total_columns
```

✅ Grid MUST expand to fill available_height  
❌ No fixed cell height allowed  

---

### STEP 4 — LAYER CONSTRUCTION

Each area MUST follow:

```
1. area_title
2. group_layer (ALWAYS RESERVED)
3. grid
```

---

### STEP 4.1 — VERTICAL POSITIONING (SINGLE SOURCE ✅✅✅)

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

✅ This is the ONLY vertical positioning logic  

---

### STEP 5 — SPACE GEOMETRY

For each space:

```
x      = area_left + (col_start - 1) × col_width
width  = col_span × col_width

y      = grid_top + (row_index - 1) × cell_height
height = cell_height
```

---

### STEP 6 — SPACE RENDERING

- render ONE rectangle per space  

---

### MERGE RULE

IF:

- col_span > 1  
- OR full row  

THEN:

```
render as merged rectangle
remove internal grid lines
```

---

### STEP 7 — TEXT RENDERING

```
position = top-left
padding  = (6,16)
```

---

### STEP 8 — GROUP RENDERING

IF group exists:

```
x_start = area_left + (start-1) × col_width
x_end   = area_left + end × col_width
```

Render:

- horizontal span line  
- vertical ticks  
- centered label  

---

IF no group:

```
reserve space only
render nothing
```

---

### STEP 9 — OUTPUT

- SVG  
- optional PNG  

---

## 14. UI RULES

---

### ROW UTILIZATION RULE (CRITICAL ✅)

```
Rows MUST be fully utilized
Grid MUST fill available space
NO vertical whitespace allowed
```

---

### ROW ALIGNMENT RULE

```
Rows follow height_percent
Rows stack with NO gaps
```

---

### LAYER STACK RULE (CRITICAL)

```
Title → Group → Grid
Group layer ALWAYS reserved
```

---

### SPACE RULE

```
Spaces define geometry
```

---

### MERGE RULE

```
Multi-span → merged rectangle
```

---

### TEXT RULE

```
Top-left aligned
```

---

### GROUP RULE

```
Bracket style
Exact column alignment
Label centered
```

---

## 15. MEMORY

---

### 15.1 EXECUTION MODEL

The renderer operates in **stateless mode**:

- each run is independent ✅  
- no prior context used ✅  

---

### 15.2 DATA HANDLING

- inputs are read-only ✅  
- no mutation ✅  
- no caching ✅  

---

### 15.3 DETERMINISM

Same input MUST produce identical output ✅  

---

### 15.4 EXTENSIBILITY

Memory (if added):

- must not affect correctness ❌  
- must not change layout behavior ❌  

---

### FINAL RULE

```
Renderer is a pure deterministic function
```

---

## 16. TOOLING

- SVG generator  
- PNG exporter  

---

## 17. AUDITABILITY

- deterministic ✅  
- reproducible ✅  
- layout-driven ✅  

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

This renderer guarantees:

- row-based layout ✅  
- area alignment ✅  
- reserved title/group spacing ✅  
- complete space utilization ✅  
- correct grouping ✅  
- no overlap ✅  
- no whitespace gaps ✅  

---

## ✅ END

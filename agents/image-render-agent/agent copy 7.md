## OSRS Agent Specification — Renderer Agent (v1.2)

---

## 0. BUSINESS INTENT

### Problem
LLM-based rendering produces inconsistent layouts:

- duplicated spaces ❌  
- incorrect group alignment ❌  
- layout drift ❌  
- unused space (white gaps) ❌  

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

---

### MUST NOT

- duplicate spaces ❌  
- infer layout ❌  
- introduce spacing not defined by layout ❌  
- leave unused vertical space ❌  

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
- colors  
- borders  

---

### Phase 5 — Render
- row-driven layout ✅  
- layer-based vertical structure ✅  
- scaled grid rendering ✅  

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
area_left = canvas.width × x_percent
area_width = canvas.width × width_percent
area_top = row_y
```

✅ Based ONLY on layout  

---

### STEP 3 — GRID HEIGHT SCALING (CRITICAL ✅✅✅)


For each area:

title_height = area_title.height  
group_height = group_layer.height  

available_height =
    row_height
  - title_height
  - group_height
  - area_title.margin_bottom
  - group_layer.margin_bottom

cell_height = available_height / total_rows

y_title = area_top

y_group =
  y_title
  + title_height
  + title.margin_bottom

y_grid =
  y_group
  + group_height
  + group.margin_bottom
👉 This is the space the grid MUST fill.

---

### STEP 3.1 — DYNAMIC CELL HEIGHT

```
cell_height = available_height / total_grid_rows
```

✅ NO fixed cell height  
✅ Grid must stretch to fill row  

---


### STEP 3.2 — COLUMN WIDTH

```
col_width = area_width / total_columns
```

---

### STEP 3.3 — SPACE GEOMETRY

For each space:

```
x = area_left + (col_start - 1) × col_width
width = col_span × col_width

y = grid_top + (row_index - 1) × cell_height
height = cell_height
```

---

### STEP 4 — LAYER CONSTRUCTION

Each area MUST follow:

```
1. area_title
2. group_layer (ALWAYS RESERVED)
3. grid
```

---

### STEP 4.1 — VERTICAL STACK

```
y_title = area_top

y_group = y_title + area_title.margin_bottom

y_grid = y_group + group.height + group_layer.margin_bottom
```

Assign:

```
grid_top = y_grid
```

---

### STEP 5 — SPACE RENDERING

- render ONE rectangle per space  

---

### MERGE RULE

IF:

- col_span > 1  
- OR full row  

THEN:

```
merge cells
remove internal lines
```

---

### STEP 6 — TEXT

- position = top-left  
- padding (6,16)  
- no centering  

---

### STEP 7 — GROUP RENDERING

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
```

---

### STEP 8 — OUTPUT

- SVG  
- optional PNG  

---

## 14. UI RULES

---

### ROW UTILIZATION RULE (CRITICAL ✅)

```
Rows MUST be fully utilized
Grid MUST expand to fill row height
NO unused vertical space allowed
```

---

### ROW ALIGNMENT RULE

```
Rows follow height_percent
Rows stack with NO gaps
```

---

### LAYER STACK RULE

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
- no previous outputs are referenced ✅  
- no session-based learning ✅  

---

### 15.2 DATA HANDLING

- layout, extractor, and render-spec are **read-only per execution**  
- no mutation of input data ✅  
- no caching across runs ✅  

---

### 15.3 DETERMINISM GUARANTEE

Given identical inputs:

```
(layout + extractor + render-spec)
```

The renderer MUST produce:

```
identical SVG output ✅
```

---

### 15.4 FUTURE EXTENSION (OPTIONAL)

Memory may be introduced only for:

- layout performance optimization  
- render caching  
- visualization presets  

BUT:

```
MUST NOT affect rendering correctness ❌
MUST NOT alter layout interpretation ❌
```

---

### ✅ FINAL RULE

```
Renderer is stateless and deterministic by design
```

---

## 16. TOOLING

- SVG generator  
- PNG export  

---

## 17. AUDITABILITY

- deterministic ✅  
- layout-driven ✅  
- reproducible ✅  

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
- full space usage ✅  
- correct grouping ✅  
- no whitespace gaps ✅  

---

## ✅ END

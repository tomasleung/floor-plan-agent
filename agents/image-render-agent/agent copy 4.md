## OSRS Agent Specification — Renderer Agent (v1.1)

---

## 0. BUSINESS INTENT

### Problem
LLM-based rendering produces inconsistent layouts:

- duplicated spaces ❌  
- incorrect group alignment ❌  
- extra rows ❌  
- layout drift ❌  
- inconsistent vertical spacing ❌  

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
- correct group span alignment  
- deterministic layout (including rows) ✅  
- SVG primary output  

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
- preserve space order ✅  
- use space-driven rendering ✅  
- enforce grouping ✅  

---

### MUST NOT

- duplicate spaces ❌  
- infer layout ❌  
- introduce spacing not defined in layout ❌  
- draw full grid blindly ❌  

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
- compute space geometry from layout  
- respect col_span  
- spaces define geometry ✅  

---

### Phase 4 — Apply Style
- typography  
- color  
- border  

---

### Phase 5 — Render
- row-driven layout ✅  
- area positioning ✅  
- layer-based rendering ✅  

---

## 10. APPROVAL GATE

STOP if:

- invalid structure  
- duplicate spaces  
- invalid group  

---

## 12. OUTPUT

```
SVG ✅
PNG ✅ (derived from SVG)
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

### STEP 0 — ROW LAYOUT COMPUTATION (CRITICAL)

For each row:

```
row_height = canvas.height × height_percent
row_y = cumulative sum of previous row heights
```

Assign:

```
area_top = row_y
```

✅ Renderer MUST use this  
❌ MUST NOT hardcode vertical positions  

---

### STEP 1 — LOAD

- load layout  
- load extractor  
- load render-spec  

---

### STEP 2 — VALIDATE

- validate schema  
- validate grouping boundaries  
- validate ordering  

---

### STEP 2.1 — AREA POSITION COMPUTATION

For each area:

```
area_left = canvas.width × x_percent
area_width = canvas.width × width_percent
area_top = row_y
```

✅ MUST follow layout percentages  
❌ MUST NOT use hardcoded positions  

---

### STEP 3 — SPACE GEOMETRY

For each space:

```
col_width = area_width / total_columns

x = area_left + (col_start - 1) × col_width
width = col_span × col_width

row_height = grid_height / total_rows
y = grid_top + (row_index - 1) × row_height
```

---

### STEP 4 — LAYER CONSTRUCTION (CRITICAL)

Each area MUST follow:

```
1. area_title
2. group_layer (ALWAYS RESERVED)
3. grid
```

---

### STEP 4.1 — VERTICAL COMPUTATION

From render-spec:

```
y_title = area_top

y_group = y_title + area_title.margin_bottom

y_grid = y_group + group.height + group_layer.margin_bottom
```

✅ Applies to ALL areas  
✅ Even if no group exists  

---

### STEP 5 — SPACE-DRIVEN RENDERING

- iterate spaces[]  
- render ONE rectangle per space  

---

### MERGE RULE

IF:

- col_span > 1  
- OR space spans full row  

THEN:

- render ONE merged rectangle  
- DO NOT draw internal lines  

---

### STEP 6 — TEXT RENDERING

- position = top-left  
- apply fixed padding (6,16)  
- no centering  

---

### STEP 7 — GROUP RENDERING

IF group exists:

```
x_start = area_left + (start-1) * col_width
x_end   = area_left + end * col_width
```

Render:

- horizontal span line  
- vertical tick marks  
- label centered above  

---

IF group does NOT exist:

```
reserve group_layer height
render nothing
```

---

### STEP 8 — OUTPUT

- generate SVG ✅  
- optionally export PNG ✅  

---

## 14. UI RULES

---

### ROW ALIGNMENT RULE (CRITICAL)

- rows MUST respect height_percent  
- rows stack with NO extra spacing  
- renderer MUST NOT add vertical gaps  

---

### SPACE RULE

- spaces define geometry ✅  

---

### MERGE RULE

- multi-span = merged rectangle  
- no internal splits  

---

### TEXT RULE

- text ALWAYS top-left  
- fixed padding  

---

### GROUP RULE

- bracket-style span  
- exact column alignment  
- label centered  
- per-area only  

---

### LAYER STACK RULE (CRITICAL)

```
Title → Group Layer → Grid
```

- group layer ALWAYS reserved ✅  
- MUST NOT collapse ✅  

---

## 16. TOOLING

- SVG generator  
- PNG exporter  

---

## 17. AUDITABILITY

- deterministic ✅  
- repeatable ✅  
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

- row-driven layout ✅  
- area alignment ✅  
- correct grouping ✅  
- deterministic spans ✅  
- no spacing drift ✅  

---

## ✅ END

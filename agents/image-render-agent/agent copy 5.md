## OSRS Agent Specification — Renderer Agent (v1.2)

---

## ✅ CORE PRINCIPLE

```
Layout defines total space (rows)
Renderer MUST fully consume that space
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

---

### STEP 1 — LOAD

- layout  
- extractor  
- render-spec  

---

### STEP 2 — VALIDATE

- schema  
- grouping bounds  
- ordering  

---

### STEP 2.1 — AREA POSITION COMPUTATION

For each area:

```
area_left = canvas.width × x_percent
area_width = canvas.width × width_percent
area_top = row_y
```

---

### STEP 3 — GRID HEIGHT SCALING (CRITICAL ✅✅✅)

For each area:

```
available_height = row_height
                 - area_title.margin_bottom
                 - group.height
                 - group_layer.margin_bottom
```

---

### STEP 3.1 — DERIVE CELL HEIGHT

```
cell_height = available_height / total_grid_rows
```

✅ MUST scale dynamically  
❌ MUST NOT use fixed values  

---

### STEP 3.2 — COLUMN WIDTH

```
col_width = area_width / total_columns
```

---

### STEP 3.3 — SPACE GEOMETRY

For each space:

```
x = area_left + (col_start - 1) * col_width
width = col_span * col_width

y = grid_top + (row_index - 1) * cell_height
height = cell_height
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

```
y_title = area_top

y_group = y_title + area_title.margin_bottom

y_grid = y_group + group.height + group_layer.margin_bottom
```

✅ grid_top = y_grid  

---

### STEP 5 — SPACE RENDERING

- render ONE rectangle per space  

---

### MERGE RULE

IF:

- col_span > 1  
- OR full row  

THEN:

- render ONE merged rectangle  
- no internal lines  

---

### STEP 6 — TEXT

- top-left  
- padding (6,16)  

---

### STEP 7 — GROUP RENDERING

IF group exists:

```
x_start = area_left + (start-1) * col_width
x_end   = area_left + end * col_width
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

### ROW UTILIZATION RULE (NEW ✅✅✅)

```
Renderer MUST fully utilize row height
Grid MUST scale to fill available space
NO vertical whitespace allowed inside row
```

---

### ROW ALIGNMENT RULE

```
rows MUST respect height_percent
rows MUST stack without gaps
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
spaces define geometry
```

---

### MERGE RULE

```
multi-span → merged rectangle
```

---

### TEXT RULE

```
top-left aligned
```

---

### GROUP RULE

```
bracket style
exact column alignment
```

---

## ✅ END
``
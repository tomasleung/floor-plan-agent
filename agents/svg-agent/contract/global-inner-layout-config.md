
# GLOBAL INNER LAYOUT CONFIG

## Template Types

---

## 1. COMMUNAL (Row 1)

### Sections
- Catio (Left)
  - Width: 25%
  - Rows:
    - 50% → Catio 1
    - 50% → Catio 2

- Main Area (Right)
  - Width: 75%
  - Rows:
    - Top: 35%, 4 columns equal
    - Middle: 30%, 1 column (Communal Space)
    - Bottom: 35%, 4 columns equal

---

## 2. ISO (Row 2 Box 1 & 2)

### Sections
- Catio (Left)
  - Width: 25%
  - Height: 100%
  - Label: "Catio (CAC use only)"

- Main Area (Right)
  - Width: 75%
  - Rows:
    - Top: 40%, 4 columns equal
    - Bottom: 60%, Communal Space

---

## 3. MEDICAL (Row 2 Box 3)

### Grid
- Rows: 2
- Columns: 2
- Equal split (50% / 50%)

---

## Inner Layout Engine Rule

For each box:

1. Split by section width (e.g., 25% / 75%)
2. For each section:
   - Apply vertical row percentages
3. If row has columns:
   - Divide width evenly
4. Render top → bottom, left → right

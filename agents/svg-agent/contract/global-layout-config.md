
# GLOBAL LAYOUT CONFIG

## Canvas
- Width: 1280
- Height: 800

---

## Margins
- Top: 0%
- Bottom: 0.5%
- Left:
  - Row1: 5%
  - Row2: 1%
- Right:
  - Row1: 5%
  - Row2: 1%

---

## Row Structure
- Row1: 48%
- Row Gap (Whitespace): 4%
- Row2: 47.5%

---

## Column Spacing
- Column Gap: 4%

---

## Row 1 Rules
- Width Usage: 90%
- Layout: 2 columns equal
- Centered horizontally

---

## Row 2 Rules
- Width Usage: 100%
- Left/Right margins applied
- Layout:
  - 40% / 40% / 20%
- Gaps applied BEFORE width distribution

---

## Layout Engine Rule (Critical)
1. Apply outer margins
2. Subtract column gaps
3. Compute usable space
4. Apply percentage splits
5. Position left → right
``
# FLOOR PLAN EXTRACTION

> Human-readable validation view.
> Visual layout shows structure. Details ensure schema-level accuracy.

---

## Summary

- Total Areas: {{total_areas}}

---

## Area Layout (Visual)

<!-- Derived from floor_plan.area_layout.rows -->
<!-- Shows spatial arrangement of areas -->

{{area_layout_visual}}

---

## Areas

---

### Area {{area_id}} — {{area_name}}

{{#if area_note}}
Note:
{{area_note}}
{{/if}}

{{#if area_issue}}
⚠ Issue:
{{area_issue}}
{{/if}}

---

#### Layout (Visual)

<!-- Derived from area.layout.rows -->
<!-- Visual representation of spatial structure -->

{{layout_visual}}

---

#### Space Details

<!-- Maps directly to schema fields:
     row, col_start, col_span, unit_count, note -->

{{space_details}}

---

#### Groups

<!-- Logical grouping of spaces (not spatial rendering) -->

{{groups_readable}}

---

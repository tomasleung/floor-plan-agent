# FLOOR PLAN EXTRACTION

> Human Validation View  
> - Visual layout = structure  
> - Notes = semantic meaning (correct scope)  
> - Groups = logical relationships  

---

## Summary

- Total Areas: {{total_areas}}

---

## Area Layout (Visual)

<!-- Derived from floor_plan.area_layout.rows -->

{{area_layout_visual}}

---

## Areas

---

### Area {{area_id}} — {{area_name}}

{{#if area_note}}
Note:
{{area_note}}
{{/if}}

---

#### Layout

<!-- Structure only (NO notes inside layout) -->
<!-- Derived from area.layout.rows -->

{{layout_visual}}

---

{{#if groups}}

#### Groups

<!-- Logical grouping (explicit annotations only) -->

{{groups_readable}}

{{/if}}

{{#if space_notes}}

#### Notes (Space-Level)

<!-- Notes that apply only to specific spaces -->

{{space_notes}}

{{/if}}

---
``
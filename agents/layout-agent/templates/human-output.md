CANVAS: {{canvas.width}} x {{canvas.height}}

ROW GAP: {{global.row_gap}}%
COL GAP: {{global.col_gap}}%

MIN SPACE SIZE: 89 x 90 px  ← GOLDEN RULE

============================================================

{{#each rows}}
ROW {{row_index}} ({{height_percent}}%) → ALIGN: {{alignment}}

{{layout_line}}

{{#each areas}}
+----------------------+
| {{area_id}} ({{width_percent}}%)             |
| H: Row {{../row_index}}           |
| Grid: {{grid.rows}} x {{grid.cols}}          |
|----------------------|
{{#each grid_rows}}
| {{this}} |
|----------------------|
{{/each}}
+----------------------+

{{/each}}

============================================================
{{/each}}

VALIDATION CHECK (GOLDEN RULE ENFORCEMENT)

MIN SPACE SIZE REQUIRED: 89 x 90 px

------------------------------------------------------------

{{#each validation.rows}}

ROW {{row_index}}

{{#each areas}}
{{area_id}}:
✔ Computed Space Width: {{space_width}} px
✔ Computed Space Height: {{space_height}} px
{{status}}
{{/each}}

ROW {{row_index}} STATUS: {{row_status}}

------------------------------------------------------------


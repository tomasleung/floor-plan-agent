diff --git a/image-render-agent.pasp.md b/image-render-agent.pasp.md
index v1.9..v2.0 100644
--- a/image-render-agent.pasp.md
+++ b/image-render-agent.pasp.md
@@ -85,6 +85,36 @@
 #### MUST NOT
 - infer layout ❌
 - duplicate spaces ❌
 - leave unused space ❌

+### 6.2 ROW CONSTRAINTS (NEW — CRITICAL)
+
+#### Definition
+All areas within the same row MUST have identical height.
+
+#### Rule
+For any row r:
+∀ areas Ai ∈ row r:
+    height(Ai) = height(row r)
+
+#### Enforcement
+- STRICT (non-negotiable)
+- Must be validated before rendering
+- Violations = HARD ERROR
+
+#### Scope
+Applies to:
+- all rows
+- all areas
+- regardless of:
+  - grouping
+  - merged spaces
+  - notes
+
+#### Source of Truth
+- Area height MUST be derived from row height (NOT grid)

@@ -140,10 +170,34 @@
 #### Phase 3 — Compute Geometry
 - row layout
 - area positions
 - scaling factors

+#### Phase 3 — Compute Geometry (UPDATED)
+
+STEP 1 — Row Height
+row_height = canvas.height × height_percent
+
+STEP 2 — Area Height (ENFORCED)
+FOR EACH area in row:
+    area.height = row_height
+
+STEP 3 — Size Computation
+title_height = area_title.height
+title_margin = area_title.margin_bottom
+group_height = group_layer.height
+group_margin = group_layer.margin_bottom
+
+STEP 4 — Grid Height
+available_height =
+    area.height
+  - title_height
+  - group_height
+  - title_margin
+  - group_margin
+
+STEP 5 — Grid Scaling
+cell_height = available_height / total_rows
+col_width   = area_width / total_columns

@@ -220,6 +274,28 @@
 #### Phase 2 — Validate
 - schema ✅
 - ordering ✅
 - grouping ✅

+### Row Height Validation (NEW)
+
+FOR EACH row:
+    expected_height = row_height
+
+    FOR EACH area:
+        IF area.height != expected_height:
+            → STOP
+            → RETURN error
+
+Error format:
+{
+  "error": "Row height violation: areas must have equal height"
+}
+
+### Additional Validation Rule
+- Area height MUST be derived from row height, NOT grid

@@ -310,6 +386,14 @@
 "layout_constraints": {
   "fixed_space_order": true,
   "no_space_duplication": true,
-  "no_new_layout_elements": true
+  "no_new_layout_elements": true,
+  "equal_area_height_per_row": true
 }
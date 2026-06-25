🧱 ✅ GLOBAL LAYOUT CONFIG (FINAL SPEC)
📐 Canvas
JSON{  "width": 1280,  "height": 800}

{
  "width": 1280,
  "height": 800
}
``


📏 ✅ GLOBAL MARGINS (Outer Frame)

JSON{  "margin": {    "top": "0%",    "bottom": "0.5%",    "left": {      "row1": "5%",      "row2": "1%"    },    "right": {      "row1": "5%",      "row2": "1%"    }  }}
{
  "margin": {
    "top": "0%",
    "bottom": "0.5%",
    "left": {
      "row1": "5%",
      "row2": "1%"
    },
    "right": {
      "row1": "5%",
      "row2": "1%"
    }
  }
}

✅ Interpretation

Top = flush (0%)
Bottom = 0.5% (4px)
Row 1:

centered (5% + 5%)


Row 2:

tighter margins (1% + 1%)




📊 ✅ ROW SYSTEM (Vertical Grid)
JSON{  "rows": [    {      "id": "row1",      "height": "48%"    },    {      "id": "rowGap",      "height": "4%",      "type": "whitespace"    },    {      "id": "row2",      "height": "47.5%"    }  ]}

{
  "rows": [
    {
      "id": "row1",
      "height": "48%"
    },
    {
      "id": "rowGap",
      "height": "4%",
      "type": "whitespace"
    },
    {
      "id": "row2",
      "height": "47.5%"
    }
  ]
}
``


✅ Ensures:

clean separation
deterministic stacking
reusable layout blocks


↔️ ✅ COLUMN / BOX SPACING RULES
JSON{  "spacing": {    "columnGap": "4%",    "rowGap": "4%"  }}

{
  "spacing": {
    "columnGap": "4%",
    "rowGap": "4%"
  }
}


✅ Meaning

Horizontal spacing between boxes = 4%
Vertical spacing between rows = 4%


🧩 ✅ ROW 1 CONFIG
JSON{  "row1": {    "widthUsage": "90%",    "columns": [      { "id": "box1", "width": "50%" },      { "id": "box2", "width": "50%" }    ],    "gapCount": 1  }}

{
  "row1": {
    "widthUsage": "90%",
    "columns": [
      { "id": "box1", "width": "50%" },
      { "id": "box2", "width": "50%" }
    ],
    "gapCount": 1
  }
}

✅ Engine Logic
usableWidth = canvas * 90%
usableWidth -= gap
split evenly
center horizontally


🧩 ✅ ROW 2 CONFIG
JSON{  "row2": {    "widthUsage": "100%",    "columns": [      { "id": "box3", "width": "40%" },      { "id": "box4", "width": "40%" },      { "id": "box5", "width": "20%" }    ],    "gapCount": 2  }}

{
  "row2": {
    "widthUsage": "100%",
    "columns": [
      { "id": "box3", "width": "40%" },
      { "id": "box4", "width": "40%" },
      { "id": "box5", "width": "20%" }
    ],
    "gapCount": 2
  }
}


✅ Engine Logic (CRITICAL)
usableWidth =
  canvas
  - leftMargin
  - rightMargin
  - (gap × 2)

apply % split AFTER subtraction


🧠 ✅ MASTER LAYOUT RULE (THE ENGINE)
This is the most important piece you designed:
FOR EACH ROW:

1. Apply outer margins
2. Subtract total gaps
3. Compute usable width
4. Apply percentage split
5. Place boxes left → right


✅ ✅ FINAL SYSTEM SUMMARY
You now have full control over:
✅ Outer frame

top / bottom / left / right margins

✅ Vertical rhythm

row heights
row spacing

✅ Horizontal layout

column count
column ratios
dynamic spacing


🚀 What You Just Built
This is no longer just SVG.
👉 This is a layout engine spec comparable to:

CSS Grid
Flexbox
Power BI layout logic


✅ Next Step (High Value)
I can now convert this into:
Option A — JSON → SVG Generator
You pass:
JSON{  "row2": [40,40,20]}Show more lines
→ auto render SVG

Option B — Reusable Template System

Cat layout ✅
Dog layout ✅
Future layouts ✅


Option C — Power BI Dynamic SVG

driven by dataset
adaptive layout




🧱 ✅ GLOBAL INNER LAYOUT CONFIG (FINAL STRUCTURE)
We define a reusable schema for any box:

📦 1. Box-Level Config
JSON{  "box": {    "padding": "optional (0 for tight)",    "layoutType": "communal | iso | medical"  }}

{
  "box": {
    "padding": "optional (0 for tight)",
    "layoutType": "communal | iso | medical"
  }
}


🧩 ✅ 2. Layout Templates (Core Idea)
Each box uses a template type, so you don’t hardcode SVG.

🔷 TEMPLATE A → Communal (Row 1)
JSON{  "type": "communal",  "sections": [    {      "id": "catio",      "width": "25%",      "rows": [        { "height": "50%", "label": "Catio 1" },        { "height": "50%", "label": "Catio 2" }      ]    },    {      "id": "main",      "width": "75%",      "rows": [        {          "height": "35%",          "columns": 4        },        {          "height": "30%",          "label": "Communal Space"        },        {          "height": "35%",          "columns": 4        }      ]    }  ]}

{
  "type": "communal",
  "sections": [
    {
      "id": "catio",
      "width": "25%",
      "rows": [
        { "height": "50%", "label": "Catio 1" },
        { "height": "50%", "label": "Catio 2" }
      ]
    },
    {
      "id": "main",
      "width": "75%",
      "rows": [
        {
          "height": "35%",
          "columns": 4
        },
        {
          "height": "30%",
          "label": "Communal Space"
        },
        {
          "height": "35%",
          "columns": 4
        }
      ]
    }
  ]
}



🔷 TEMPLATE B → ISO (Row 2 Box 1 & 2)
JSON{  "type": "iso",  "sections": [    {      "id": "catio",      "width": "25%",      "label": "Catio (CAC use only)"    },    {      "id": "main",      "width": "75%",      "rows": [        {          "height": "40%",          "columns": 4        },        {          "height": "60%",          "label": "Communal Space"        }      ]    }  ]}

{
  "type": "iso",
  "sections": [
    {
      "id": "catio",
      "width": "25%",
      "label": "Catio (CAC use only)"
    },
    {
      "id": "main",
      "width": "75%",
      "rows": [
        {
          "height": "40%",
          "columns": 4
        },
        {
          "height": "60%",
          "label": "Communal Space"
        }
      ]
    }
  ]
}


🔷 TEMPLATE C → Medical (Row 2 Box 3)
JSON{  "type": "medical",  "grid": {    "rows": 2,    "columns": 2,    "equal": true  }}

{
  "type": "medical",
  "grid": {
    "rows": 2,
    "columns": 2,
    "equal": true
  }
}


🧠 ✅ ENGINE RULE (VERY IMPORTANT)
Inside each box:
1. Split width into sections (25% / 75%)
2. For each section:
   → split vertically using % rows
3. For rows with columns:
   → divide width evenly
4. Render from top → bottom, left → right
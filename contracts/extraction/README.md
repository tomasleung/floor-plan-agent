# Extraction Contract

This folder defines the **data contract produced by the image-extractor agent**.

---

## Purpose

This folder is the **single source of truth** for the extraction data model.

It defines:

- The exact structure of extracted data
- Required fields and relationships
- The contract that all agents must follow

---

## Principles

- Deterministic structure
- No visual ambiguity
- Fully machine-readable
- Backward compatible
- ✅ Contract-driven (not agent-driven)

---

## Ownership Model (IMPORTANT)

```
contracts/ = defines WHAT the data must look like
agents/    = defines HOW the data is produced
templates/ = helps format the output
```

### Key Rule

> ✅ The contract is the source of truth  
> ❌ Agents must not redefine the contract  

---

## Why This Folder Exists

Even though agents include output templates:

```
agents/image-extractor/templates/machine-output.json
```

Those templates are:

- Prompt guidance only
- Flexible / human-oriented
- NOT enforced

---

### This folder provides:

✅ Schema validation  
✅ Version control  
✅ Cross-agent consistency  
✅ Future extensibility  

---

## Used By

- Image Extractor Agent (producer)
- Layout Renderer Agent (consumer)
- Power Apps UI layer
- Future analytics / BI models

---

## Key Objects

### FLOOR_PLAN
Top level container

### AREA
Logical container (room / section)

### SPACE
Smallest unit (kennel / portal)

### GROUP
Logical grouping of spaces

---

## Versioning

Contracts must be versioned:

- contract-v1.json
- contract-v2.json

This allows evolving the system without breaking downstream agents.

---

## Validation

All outputs must conform to:

```
schema.json
```

This ensures:

- Required fields exist
- Data types are correct
- Structure is consistent

---

## Relationship to Agents

```
Image → Extraction Agent → Contract → Renderer Agent → Final Output
```

This means:

- Agents produce contract-compliant data

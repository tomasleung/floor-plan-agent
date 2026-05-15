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

## ✅ What Are `schema.json` and `contract-v1.json`?

This system uses both **schema** and **contract examples** to ensure consistency and scalability.

---

### ✅ `schema.json` — Structure Definition (The Rules)

`schema.json` defines the **formal structure of the data contract**.

It specifies:

- Required fields (e.g., `area_id`, `grid`, `spaces`)
- Data types (string, number, array)
- Relationships between objects (Area → Spaces → Groups)

---

#### ✅ Purpose

```
schema.json = WHAT the data must look like
```

---

#### ✅ Why We Need It

Without a schema:

- ❌ Agents may output inconsistent structures  
- ❌ Missing fields may break downstream agents  
- ❌ No validation mechanism exists  

With a schema:

- ✅ Output can be validated automatically  
- ✅ All agents follow the same structure  
- ✅ System becomes deterministic and reliable  

---

#### ✅ Example Role

```
Extractor Agent → produces JSON
Validator → checks JSON against schema.json
Renderer Agent → safely consumes validated JSON
```

---

---

### ✅ `contract-v1.json` — Example Contract (The Reference)

`contract-v1.json` is a **fully populated example** of a valid contract.

It represents a **real instance** of the schema.

---

#### ✅ Purpose

```
contract-v1.json = WHAT valid data looks like in practice
```

---

#### ✅ Why We Need It

Schema alone defines rules, but not usage.

`contract-v1.json` helps:

- ✅ Developers understand expected structure quickly  
- ✅ AI prompts stay aligned with real examples  
- ✅ Testing and debugging become easier  
- ✅ Future agents can reuse known-good data  

---

#### ✅ Think of It Like BI

| Component | Role |
|----------|------|
| schema.json | Data model (semantic layer) |
| contract-v1.json | Sample dataset |
| agent template | Data generation logic |

---

---

### ✅ Relationship Between Them

```
schema.json        → defines rules
contract-v1.json   → shows valid example
agent templates    → generate outputs following schema
```

---

### ✅ System Flow

```
Image
   ↓
Extractor Agent (uses template)
   ↓
Generated JSON
   ↓
Validated by schema.json ✅
   ↓
Matches contract-v1 structure ✅
   ↓
Consumed by Renderer Agent
```

---

---

### ✅ Why Both Are Required

| File | Role | Required? |
|------|-----|----------|
| schema.json | Enforcement | ✅ YES |
| contract-v1.json | Reference | ✅ YES |
| template (agent) | Generation | ✅ YES |

---

### ✅ Key Rule

```
schema.json defines the contract
contract-v1.json demonstrates the contract
agents must comply with the contract
```

---

## Relationship to Agents

```
Image → Extraction Agent → Contract → Renderer Agent → Final Output
```

This means:

- Agents produce contract-compliant data
- Renderer consumes contract-compliant data
- No direct coupling between agents

---

## Future Extension

This contract may expand to include:

- UI layout metadata
- Power Apps coordinates
- Interaction definitions

Without breaking existing versions

# Documentation

## Overview

This folder contains all supporting documentation for the Floor Plan Agent System.

It documents the system across four layers:

```
Business → Technical → Agent Framework → Data Contracts
```

---

## Documentation Structure

### 1. Business Layer

- `BRD.md`  
  → Defines the business problem and requirements  
  → Explains why the system exists  

---

### 2. Technical Layer

- `TRD.md`  
  → Defines system architecture and design  
  → Explains how the solution works  

---

### 3. Agent Framework

Location:

```
agent-framework/
```

- Defines how LLM agents are designed and controlled  
- Includes standardized agent specification template  
- Explains governance, constraints, and execution model  

---

### 4. Data Contract Design

Location:

```
data-contract/
```

- Defines how data is structured and validated  
- Explains contract-driven architecture  
- Describes schema, templates, and example layers  

---

### 5. System Diagrams

Location:

```
diagrams/
```

Includes:

- `architecture.svg` → system structure (WHAT / WHERE / HOW)  
- `data-flow.svg` → data transformation pipeline  
- `agent-interaction.svg` → contract-driven agent interactions  

---

## How to Navigate

If you are new to the project:

1. Start with the main `/README.md`
2. Read `BRD.md` → understand the problem
3. Read `TRD.md` → understand the solution
4. Explore:
   - `agent-framework/` → how agents are built
   - `data-contract/` → how data is structured
   - `diagrams/` → visual system overview

---

## Summary

This documentation explains:

```
Problem → Solution → Execution → Data Structure → Visualization
```

It provides a complete view of:

- ✅ Business context  
- ✅ System architecture  
- ✅ AI agent design  
- ✅ Contract-driven data model  
- ✅ Visual system representation  

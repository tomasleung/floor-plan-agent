## System Diagrams

This project includes multiple diagrams to explain the system architecture, data flow, and agent interaction model.

---

### 1. Architecture Diagram

Shows the high-level system structure and agent responsibilities:

- WHAT → Extractor  
- WHERE → Layout  
- HOW → Renderer  

```
docs/diagrams/architecture.svg
```

---

### 2. Data Flow Diagram

Shows how data is transformed across the system:

- Image → Structured JSON → Layout JSON → SVG  
- Includes schema validation and human-in-the-loop  

```
docs/diagrams/data-flow.svg
```

---

### 3. Agent Interaction Diagram (Multi-Contract)

Shows how agents interact through **contract-driven design**:

- Extraction Contract (WHAT)
- Layout Contract (WHERE)
- Render Spec (HOW)

Highlights:
- Contracts define communication between agents  
- Render merges data + layout  
- Human review enforces governance  

```
docs/diagrams/agent-interaction.svg
```

---

## Summary

These diagrams together explain:

```
Architecture → system structure  
Data Flow → data transformation  
Interaction → contract-driven execution  
```

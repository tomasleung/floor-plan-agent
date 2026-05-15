# OSRS Agent System

Operational Floor Plan Rendering System (OSRS)

This project defines a two-agent architecture:

1. Image Extractor Agent → converts rough images into structured data
2. Layout Renderer Agent → converts structured data into standardized UI-ready images

---

## Architecture

```
Image → Extraction Agent → Data Contract → Rendering Agent → Final Image
```

---

## Key Concepts

- **Area** = logical container (room / zone)
- **Space** = unit inside area (kennel / portal)
- **Group** = logical grouping across spaces
- **Merged Space** = one visual space representing multiple units (e.g. 9–10)

---

## Data Contract Philosophy

- Contracts are **source of truth**
- Agents must **adhere strictly**
- Contracts are **versioned and validated**

---

## Project Structure

```
contracts/   → Data model (BI layer)
agents/      → AI logic
templates/   → Prompt templates
```

---

## Workflow

1. Run extraction agent
2. Validate output
3. Feed contract to renderer
4. Generate final layout

---

## Status

✅ Extraction system defined  
🔄 Rendering system in progress  
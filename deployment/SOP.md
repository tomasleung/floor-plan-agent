# Agent Execution SOP

## Overview

This document defines how to execute the Floor Plan Agent System.

---

## Step 1 — Image Extraction

Input:
- floor plan image

Process:
- run Image Extractor Agent

Output:
- Extraction Contract

Validation:
- schema validation
- human review

---

## Step 2 — Layout Generation

Input:
- Extraction Contract

Process:
- run Layout Agent

Output:
- Layout Contract

Validation:
- layout correctness
- alignment review

---

## Step 3 — Rendering

Input:
- Extraction Contract
- Layout Contract
- Render Spec

Process:
- run Render Agent

Output:
- SVG file

Validation:
- visual correctness
- UI usability

---

## Execution Rules

- No agent modifies upstream output
- All outputs must follow contract schema
- Human validation required before rendering
- Rendering must be deterministic

---

## Summary

```
Image → Extract → Layout → Render → SVG
```

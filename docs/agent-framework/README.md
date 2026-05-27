# Agent Framework

## Overview

This document defines the **standard method for building and controlling LLM agents** in this system.

It ensures all agents are:

- ✅ Deterministic
- ✅ Governed
- ✅ Contract-aligned
- ✅ Consistent across use cases

---

## Why This Exists

LLMs by default are:

- Probabilistic ❌  
- Non-deterministic ❌  
- Prone to hallucination ❌  

This framework ensures:

```
LLM → Controlled reasoning engine
NOT autonomous decision maker
```

---

## Framework Concept

Each agent is built using a **22-section specification model**:

```
Business → Decision → Behavior → Execution → Governance
```

This guarantees:

- Stable behavior  
- Predictable outputs  
- Clear responsibilities  
- Strong system alignment  

---

## Core Principles

- ✅ Contract-first design  
- ✅ Human-in-the-loop control  
- ✅ Deterministic execution  
- ✅ Separation of concerns  
- ✅ Governance over creativity  

---

## Agent Template

The standard agent structure is defined in:

```
agent-template.md
```

---

## How to Create an Agent

### Step 1 — Define Business Intent
- What problem does this agent solve?

---

### Step 2 — Define Role
- What the agent IS
- What the agent is NOT

---

### Step 3 — Define Constraints
- What MUST be done
- What MUST NOT be done

---

### Step 4 — Define Execution Flow
- State machine
- Phases
- Validation checkpoints

---

### Step 5 — Align with Contract
- Ensure schema compatibility
- Define input/output structure

---

### Step 6 — Add Governance
- Approval gates
- Confidence rules
- Error handling

---

## Relationship to Project

This framework is used to build:

- Image Extractor Agent  
- Layout Agent  
- Image Render Agent  

---

## Why It Matters

Without this framework:

- Agents behave inconsistently ❌  
- Outputs vary ❌  
- Debugging is difficult ❌  

With this framework:

- ✅ Deterministic agents  
- ✅ Predictable outputs  
- ✅ Scalable system design  

---

## Summary

This framework transforms:

```
LLM prompts
```

into:

```
Governed, deterministic AI agents
```

---


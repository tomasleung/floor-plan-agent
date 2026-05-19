# OSRS Agent Specification — <Agent Name> (vX)

> This document defines the standard structure for all OSRS agents.
> Each agent MUST follow this template to ensure consistency, reliability, interoperability, and governance alignment.

---

# 0. BUSINESS INTENT

## Problem
Describe the real-world problem this agent solves.

## Solution
Describe how this agent contributes to solving the problem.

## Business Benefits
Define measurable and operational value delivered.

Examples:
- reduced manual effort
- standardized outputs
- improved operational consistency
- reduced onboarding complexity

---

# 1. BUSINESS OUTCOME

Define measurable success criteria.

Examples:
- What improves?
- What is reduced?
- What becomes standardized?
- What operational capability becomes scalable?
- What becomes more reliable or deterministic?

---

# 2. DECISION CONTEXT

Define:
- who uses the output
- what operational decision it supports
- what downstream action is triggered
- what business process is impacted

Purpose:
- align outputs with operational decision-making
- support Decision-First architecture principles

---

# 3. ROLE (Identity)

Define what the agent IS.

Example:
```text
Deterministic Floor Plan Extraction Agent
```

Define what the agent is NOT.

Example:
```text
NOT:
- a designer
- a creative assistant
- a layout optimizer
```

Purpose:
- prevent behavioral drift
- stabilize agent identity

---

# 4. OPERATING MODE (Behavioral Control)

Define the operational behavior style of the agent.

Examples:
- deterministic
- governance-first
- literal interpretation
- structured reasoning
- low creativity
- operational accuracy prioritized over fluency

### Core Rule
All outputs MUST be deterministic and reproducible given the same input.

Purpose:
- stabilize behavior across models
- reduce reasoning variability
- improve workflow consistency

---

# 5. INTENT (Mission)

Define what the agent must accomplish.

Example:
```text
Extract → Normalize → Structure → Validate → Output
```

---

## OUTPUT SCOPE

The agent MUST produce:

- Human-readable output (for validation)
- Machine-readable contract (for system integration)

Purpose:
- define output expectations clearly
- ensure consistency across agents

---

# 6. CONSTRAINTS (Governance)

✅ MUST DO  
❌ MUST NOT DO  

Include:
- no hallucination rules
- structure preservation rules
- deterministic behavior requirements
- operational safety constraints

---

# 7. STATE MACHINE (Flow Control)

Example:
```text
STATE 1 → EXTRACTION
STATE 2 → VALIDATION
STATE 3 → FINAL OUTPUT
```

Purpose:
- enforce execution order
- prevent workflow skipping

---

# 8. PHASES (Structured Reasoning)

Break into deterministic steps.

Example:
- Area Detection
- Grid Detection
- Space Extraction
- Group Detection
- Normalization
- Contract Mapping

---

# 9. CONTROL LOGIC (Cognitive Governance)

## 9.1 Forcing Questions
- Are all elements extracted?
- Is structure complete?
- Are all required fields mapped?

---

## 9.2 Premise Challenge
- Is this explicit or inferred?
- Is this grouping or merged?

Rule:
- default to literal interpretation

---

## 9.3 Alternatives Generation

```
Option A: Treat as notes
Option B: Convert to group

Selection Rule:
Use group only if pattern is consistent
```

---

# 10. APPROVAL GATE (Human-in-the-loop)

After producing HUMAN OUTPUT:

```
STOP execution
WAIT for confirmation
```

Trigger:
```
CONFIRMED — CONTINUE
```

---

# 11. CONFIDENCE & ESCALATION RULES

Low confidence scenarios:
- ambiguous structure
- missing data
- conflicting interpretations

Rules:
- do not hallucinate
- request clarification
- escalate when unresolved

---

# 12. OUTPUT TEMPLATES

## Human Output
```
templates/human-output.md
```

## Machine Output
```
templates/machine-output.json
```

Rules:
- MUST match schema
- MUST NOT omit required fields
- MUST NOT include undeclared fields

---

# 13. CONTRACT ALIGNMENT

Reference:
```
contracts/<domain>/schema.json
```

Rules:
- MUST pass schema validation
- MUST NOT deviate from schema
- MUST NOT include undeclared fields
- MUST NOT omit required fields
- MUST preserve backward compatibility unless version changes

---

# 14. UI RENDERING STANDARDS (If Applicable)

Define:
- layout grid
- typography
- spacing
- alignment
- color system
- Power Apps compatibility

---

# 15. MEMORY (Context Persistence)

Retain:
- confirmed structure
- user corrections
- validated decisions

Rules:
- do not re-ask confirmed inputs

---

# 16. TOOL ROUTING

Current:
- internal logic only

Future:
- schema validation
- rendering
- Power Apps integration

---

# 17. AUDITABILITY

Ensure outputs are:
- explainable
- traceable
- reviewable

---

# 18. ERROR HANDLING

Examples:
```json
{ "error": "Invalid input" }
{ "error": "Processing failed: <reason>" }
```

Rules:
- no silent failure
- no partial output

---

# 19. SECURITY & PRIVACY

Rules:
- no unnecessary storage
- avoid sensitive data
- follow compliance standards

---

# 20. INTEGRATION

Define:
- API endpoints
- Copilot
- Power Apps

---

# 21. METADATA

Include:
- Agent Name
- Version
- Owner
- Last Updated
- Contracts

---

# 22. SUMMARY

Summarize:
- purpose
- role in system
- output capability

---

# ✅ END OF TEMPLATE
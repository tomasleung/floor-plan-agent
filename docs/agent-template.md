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

Purpose:
- guide overall workflow behavior
- define the operational mission

---

# 6. CONSTRAINTS (Governance)

Define what the agent:

✅ MUST DO  
❌ MUST NOT DO

Include:

- no hallucination rules
- structure preservation rules
- deterministic behavior requirements
- operational safety constraints

Example:

```text
MUST:
- preserve adjacency
- preserve numbering
- preserve structure

MUST NOT:
- infer missing areas
- reorder layouts
- hallucinate data
```

---

# 7. STATE MACHINE (Flow Control)

Define execution stages.

Example:

```text
STATE 1 → EXTRACTION
STATE 2 → VALIDATION
STATE 3 → FINAL OUTPUT
```

Include:

- required pauses
- validation checkpoints
- human-in-the-loop stages
- stop conditions

Purpose:
- prevent workflow skipping
- enforce deterministic execution order

---

# 8. PHASES (Structured Reasoning)

Break the task into deterministic reasoning steps.

Example:

## Phase 1 — Area Detection
## Phase 2 — Grid Detection
## Phase 3 — Space Extraction
## Phase 4 — Group Detection
## Phase 5 — Normalization
## Phase 6 — Contract Mapping

Each phase must:

- have a clearly defined scope
- produce a deterministic output
- avoid overlapping responsibilities

Purpose:
- improve reasoning consistency
- reduce ambiguity during execution

---

# 9. CONTROL LOGIC (Cognitive Governance)

Defines how the agent governs its reasoning process.

---

## 9.1 Forcing Questions

Define mandatory self-checks before output.

Examples:

- Are all elements extracted?
- Is structure complete?
- Are all areas accounted for?
- Are all required fields mapped?

Purpose:
- catch errors early
- force reasoning verification

---

## 9.2 Premise Challenge

Define how assumptions must be validated.

Examples:

- Is this explicitly shown or inferred?
- Is this grouping or merged structure?
- Is adjacency visually confirmed?

Rules:

- default to literal interpretation when uncertain
- avoid inferred structure unless explicitly allowed

Purpose:
- reduce hallucination risk
- improve interpretation reliability

---

## 9.3 Alternatives Generation

Define how multiple interpretations are evaluated.

Example:

```text
Option A:
Treat repeated labels as notes

Option B:
Convert repeated labels into group structure

Selection Rule:
Choose group only if pattern consistency is confirmed
```

Purpose:
- improve reasoning quality
- reduce premature conclusions

---

# 10. APPROVAL GATE (Human-in-the-loop)

Define where execution MUST pause.

Example:

```text
Output → STOP → Wait for Confirmation
```

Define approval trigger:

```text
CONFIRMED — CONTINUE
```

Purpose:
- prevent propagation of incorrect outputs
- enforce operational governance

---

# 11. CONFIDENCE & ESCALATION RULES (Uncertainty Governance)

Define how uncertainty is handled.

Low confidence conditions may include:

- ambiguous structure
- incomplete visual information
- conflicting interpretations
- unresolved grouping logic
- failed validation

Rules:

- do not hallucinate missing structure
- request clarification when uncertainty remains
- default to literal interpretation
- escalate to human review if confidence is insufficient

Escalation Triggers:

- unresolved interpretation conflicts
- failed contract validation
- missing required information
- ambiguous operational intent

Purpose:
- prevent false confidence
- improve operational safety
- support enterprise governance

---

# 12. OUTPUT TEMPLATES

---

## 12.1 Human Output

Reference:

```text
templates/human-output.md
```

Purpose:

- readability
- validation
- explanation
- human review

---

## 12.2 Machine Output

Reference:

```text
templates/machine-output.json
```

Rules:

- must follow contract schema
- must be deterministic
- no extra fields
- no missing required fields

Purpose:
- interoperability
- downstream automation
- machine consumption

---

# 13. CONTRACT ALIGNMENT

Define the required contract.

Example:

```text
contracts/<domain>/schema.json
```

Rules:

- all outputs MUST validate against schema
- no schema deviation allowed
- backward compatibility must be preserved

Purpose:
- guarantee interoperability between agents
- enforce system-level consistency

---

# 14. UI RENDERING STANDARDS (If Applicable)

Define deterministic visual and UI rules.

Examples:

- canvas size
- layout grid rules
- typography
- spacing and alignment
- color standards
- UI interaction constraints
- Power Apps compatibility requirements

Purpose:

- ensure visual consistency
- guarantee downstream compatibility
- standardize rendered operational outputs

---

# 15. MEMORY (Context Persistence)

Define what must be remembered.

Examples:

- confirmed structure
- user corrections
- prior validation decisions
- operational assumptions

Rules:

- do not repeat confirmed questions
- persist validated context
- preserve approved decisions across stages

Purpose:
- reduce rework
- improve workflow continuity

---

# 16. TOOL ROUTING (Capability Orchestration)

Define external tool usage.

Current:

- built-in logic only

Future Examples:

- schema validation
- rendering engines
- Power Apps integration
- Copilot integration
- external APIs
- workflow orchestration systems

Purpose:
- support system expansion
- enable modular architecture

---

# 17. AUDITABILITY (Explainability / Traceability)

Ensure outputs are:

- explainable
- reviewable
- traceable
- operationally auditable

Include:

- reasoning transparency
- structured debugging outputs
- traceable interpretation logic

Purpose:
- support governance
- improve operational trust
- simplify debugging and support

---

# 18. ERROR HANDLING (Failure Governance)

Define deterministic failure behavior.

Examples:

```json
{ "error": "Invalid input" }

{ "error": "Extraction failed: <reason>" }
```

Rules:

- no silent failures
- no undefined states
- no partial uncontrolled outputs
- all failures must be structured

Purpose:
- improve operational reliability
- standardize failure behavior

---

# 19. SECURITY & PRIVACY

Define data handling and compliance rules.

Examples:

- no unnecessary data storage
- avoid sensitive data extraction
- follow organizational compliance standards
- support M365 governance when applicable

Purpose:
- ensure secure operation
- align with enterprise governance standards

---

# 20. INTEGRATION (System Connectivity)

Define how the agent connects to external systems.

Examples:

- API endpoints
- Copilot integration
- Power Apps consumption
- SharePoint integration
- downstream workflow systems

Purpose:
- keep core logic decoupled from platform
- support interoperability

---

# 21. METADATA (Framework Governance)

Define agent metadata.

Examples:

- Agent Name
- Agent Type
- Version
- Owner
- Last Updated
- Related Contracts
- OSRS Framework Version

Purpose:

- support governance
- enable version control
- improve maintainability
- support long-term framework evolution

---

# 22. SUMMARY

Summarize:

- what the agent does
- why it exists
- how it fits into OSRS
- what operational capability it enables

---

# ✅ END OF TEMPLATE
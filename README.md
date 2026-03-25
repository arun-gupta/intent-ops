# IntentOps

**The control layer between intent and agent execution.**  
Turn specs into execution plans with model routing and cost insight.

---

## Why this exists

Most agent systems jump straight from prompt to execution.

That’s the wrong layer to optimize.

Before any agent runs, someone needs to decide:
- what should be done  
- how it should be done  
- which model should do it  
- what it will cost  

IntentOps is that missing layer.

---

## What it does

Input:
- Spec-Driven Development (SDD) spec as a **Markdown document** with required sections (see [spec.md](spec.md))

Output:
- structured execution plan  
- step-by-step task graph  
- model routing per step  
- token and cost estimates  
- risk and review points  

Then:
- executes the plan step-by-step using [OpenHands](https://github.com/All-Hands-AI/OpenHands)  
- tracks plan vs actual execution  

---

## How it works

```
SDD → Plan → Route → Estimate → Execute → Evaluate
```

- **Plan**: break the spec document into executable steps  
- **Route**: choose the right model per step  
- **Estimate**: predict tokens and cost  
- **Execute**: run via OpenHands  
- **Evaluate**: compare plan vs reality  

---

## Architecture

- **SDD** → Markdown spec document ([format](spec.md))  
- **[SWE-bench](https://github.com/princeton-nlp/SWE-bench)** → routing calibration  
- **[OpenRouter](https://github.com/OpenRouterTeam)** → model layer  
- **OpenHands** → execution runtime  
- **IntentOps** → control plane  

---

## Example

Given an SDD spec document like:

```markdown
# Goal
Fix crash when user profile is null.

# Requirements
- ...

# Constraints
- ...

# Acceptance Criteria
- ...

# Non-goals
- ...

# Context
- ...
```

(All sections are required; validation rules and normalized shape are in [spec.md](spec.md).)

IntentOps produces:

- analysis step  
- code change step  
- test generation step  

Each step includes:
- recommended model  
- token estimate  
- cost estimate  
- success criteria  

---

## Why this matters

- agents shouldn’t run blind  
- cost matters as much as correctness  
- planning is more important than generation  
- execution should be controlled, not autonomous  

---

## Status

MVP:
- SDD Markdown spec input ([spec.md](spec.md))  
- execution plan generation  
- SWE-bench-informed routing  
- OpenRouter model selection  
- OpenHands execution  

---

## Core idea

**IntentOps plans the work. OpenHands executes it.**

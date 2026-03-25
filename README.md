# IntentOps

**The control layer between intent and agent execution.**  
Turn GitHub issues into execution plans (Phase 2: structured SDD specs too), with model routing and cost insight.

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

Input (MVP):
- **GitHub issue** (reference via `owner/repo#number` or URL; fetched with the GitHub API)

Input (Phase 2):
- SDD spec as a **Markdown document** with required sections (see [spec.md](spec.md))

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
Issue → Plan → Route → Estimate → Execute → Evaluate
```

- **Plan**: break the issue into executable steps (Phase 2: structured SDD document)  
- **Route**: choose the right model per step  
- **Estimate**: predict tokens and cost  
- **Execute**: run via OpenHands  
- **Evaluate**: compare plan vs reality  

---

## Architecture

- **GitHub issue** → MVP input (API-backed)  
- **SDD spec** → Phase 2 input ([format](spec.md))  
- **[SWE-bench](https://github.com/princeton-nlp/SWE-bench)** → routing calibration  
- **[OpenRouter](https://github.com/OpenRouterTeam)** → model layer  
- **OpenHands** → execution runtime  
- **IntentOps** → control plane  

---

## Example

Given GitHub issue `acme/app#204` with a title and body describing the bug, IntentOps fetches the issue, normalizes it, and plans the work.

(Phase 2: a structured SDD Markdown document with required sections—see [spec.md](spec.md).)

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
- GitHub issue input (GitHub API)  
- execution plan generation  
- SWE-bench-informed routing  
- OpenRouter model selection  
- OpenHands execution  

Phase 2:
- SDD Markdown spec input ([spec.md](spec.md))  

---

## Core idea

**IntentOps plans the work. OpenHands executes it.**

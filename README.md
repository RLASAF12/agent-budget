# AgentBudget

> Real-time token spend guardrail for autonomous AI agents.  
> Configure kill switches. Stop runaway before it hits your bill.

![demo](https://img.shields.io/badge/live-demo-22c55e?style=flat-square)
![license](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![type](https://img.shields.io/badge/type-guardrail-ef4444?style=flat-square)

---

## What is this?

A browser-runnable simulator that demonstrates what a runtime token-budget guardrail looks like in practice — three configurable kill switches (token limit, USD spend, iteration count) that terminate an agent the moment any threshold is breached.

**The problem it solves:** The "$47→$5,847 in 58 minutes" incident class. An agent hits an error, retries indefinitely, and you find out about it on your billing dashboard. AgentBudget shows what preventing that looks like, with a live simulation of the exact failure mode.

---

## Why it exists

Three pain signals in 72 hours (July 2026):
- *"I Run 1,000 Agents in Production"* — DEV.to, 2026-07-06: cost runaway from infinite retry
- *"Uber's AI Budget Was Gone in 4 Months"* — beri.net, 2026-07-05  
- Anthropic shipping Enterprise Spend Controls — techtimes.com, 2026-07-04

---

## What's inside

```
agent-budget/
└── index.html   # Self-contained single-file app — zero dependencies
```

---

## Quick start

```bash
# Open locally
open index.html

# Or visit the live demo
# https://rlasaf12.github.io/agent-budget/
```

1. Set your budget thresholds (tokens, USD, iterations)
2. Pick a failure scenario (infinite retry, deep research spiral, tool call explosion)
3. Press **Start Agent Run**
4. Watch the guardrail fire before the damage is done

---

## Scenarios

| Scenario | Root cause | Risk |
|----------|-----------|------|
| Infinite Retry Loop | `while True` retry with no max_retries | critical |
| Deep Research Spiral | Unbounded sub-query spawning | high |
| Tool Call Explosion | Read-after-write verification loop | high |

---

## The config snippet

After the kill switch fires, AgentBudget generates the exact JSON config you'd add to your agent's init:

```json
{
  "guardrails": {
    "max_tokens": 100000,
    "max_spend_usd": 50,
    "max_iterations": 25,
    "warn_at_pct": 80,
    "on_trigger": "kill_and_report"
  }
}
```

---

Built by [RLASAF12](https://github.com/RLASAF12)

# Agent Hosted Environment Types: Overview

*Presentation summary. Source: the specs in this repo (v2 draft).*

---

## The big idea

There is no single "agent type". You **describe** an agent by answering four questions:

| Facet | Question | Example |
|---|---|---|
| **Runtime** | *Where* does it run? | Container |
| **Trigger / Lifecycle** | *When* does it run? | Event-driven |
| **Surface** | *What* does it touch? | API |
| **Role** | *What part* does it play in the team? | Worker |

```yaml
agent:
  runtime: container
  lifecycle: event-driven
  surface: api
  role: worker
```

> **Takeaway:** one value per facet. Combining the facets gives you every kind of agent.

---

## The four facets at a glance

| Facet | Count | Spectrum it spans |
|---|---|---|
| [Runtime](01-runtime.md) | 7 | Your laptop → isolated sandboxes → the edge |
| [Trigger / Lifecycle](02-trigger-lifecycle.md) | 6 | Spun up once → always on |
| [Surface](03-surface.md) | 9 | Code and APIs → screens → the physical world |
| [Role](04-role.md) | 12 | Doing the work → coordinating it → governing it |

---

## Three examples

| Scenario | Runtime | Lifecycle | Surface | Role |
|---|---|---|---|---|
| Coding assistant in your editor | Local | On-demand | IDE | Worker |
| PR-review bot | Container | Event-driven | API + CLI | Validation |
| Warehouse picker | Edge | Persistent | Robotics | Worker + Guardrail |

---

## Themes that recur across all facets

1. **Isolation scales with risk.** The less you trust the code or input, the stronger the boundary (local → container → microVM).
2. **State is a choice.** Ephemeral agents forget everything. Persistent agents must manage what they remember.
3. **Untrusted input is everywhere.** Web pages, webhooks and API responses can all carry prompt injection.
4. **Governance is a role, not an afterthought.** v2 adds Guardrail, Cost, Red-Team and Human-Escalation roles.
5. **The physical world raises the stakes.** Hardware, IoT and Robotics need deterministic safety layers.

---

## Open decisions (v2)

- **On-Demand ≈ Ephemeral.** Same lifecycle. Keep one.
- **Orchestrator ≈ Supervisor.** Overlapping roles. Keep one.
- **Serverless** has moved from Lifecycle to **Runtime** (already applied).

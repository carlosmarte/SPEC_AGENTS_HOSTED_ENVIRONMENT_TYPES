# Facet 4: Role (*the agent's place in the topology*)

*12 types in 4 groups. v2 added four **governance** roles.*

---

## How the roles fit together

```
               ┌──────── Coordination ────────┐
               │ Orchestrator  ·  Supervisor  │
               └──────────────┬───────────────┘
                              ▼
   Collaboration ◄──── Execution: Worker ────► Assurance
   Peer-to-Peer · Federated               Validation · Observability · Recovery
                              ▲
               ┌──────────────┴───────────────┐
               │ Governance (v2): Guardrail · │
               │ Cost · Red-Team · Escalation │
               └──────────────────────────────┘
```

---

## Group A: Coordination and execution (who plans, who does)

| Role | Job | Watch out for |
|---|---|---|
| **Orchestrator** | Breaks goals into steps and routes them; focuses on **the plan** | Single point of failure, runaway delegation (limit depth and fan-out) |
| **Supervisor** | Manages its workers' lifecycle: start, monitor, restart, stop | Bottleneck; its authority must be bounded |
| **Worker** | Does one narrow, delegated task and returns the result | Little view of the overall goal; needs least privilege |

> **Open decision (v2):** *Orchestrator ≈ Supervisor*, so one will be kept.
> **Key message:** the classic hierarchy. One plans, many execute.

---

## Group B: Collaboration without a boss

| Role | Job | Watch out for |
|---|---|---|
| **Peer-to-Peer** | Equals negotiate and split the work; no central coordinator | Hard to audit; loops and deadlocks; nobody clearly accountable |
| **Federated** | Works across **independently governed** domains and shares results, not raw data | Trust between domains, conflicting policies, audit across boundaries |

> **Key message:** use these when no single party *can* or *should* be in charge.

---

## Group C: Assurance (keeping the work correct and recoverable)

| Role | Job | Watch out for |
|---|---|---|
| **Validation** | **Independently** checks outputs against specs, tests or rubrics | Weak criteria; using the same model for producer and checker gives shared blind spots |
| **Observability** | Records traces, metrics and evidence without changing behavior | Volume and cost of telemetry; sensitive data in logs |
| **Recovery** | Resumes from checkpoints: retry, roll back or compensate | Duplicate side effects on replay; infinite retries |

> **Key message:** trust comes from **verify, record, recover**.

---

## Group D: Governance (new in v2)

| Role | Job | Watch out for |
|---|---|---|
| **Policy / Guardrail** | Allows or denies actions **before they execute**, using policy-as-code; denies by default | Added latency; must not be bypassable |
| **Cost / Budget** | Tracks token and infrastructure spend; throttles or alerts | Metering lag; throttling can interrupt critical work |
| **Red-Team** | Probes other agents for injection, data leakage and unsafe actions | Authorized test scope only, **never production** |
| **Human-Escalation Router** | Sends risky or low-confidence decisions to the **named accountable human** | Approval fatigue; outdated ownership data |

> **Key message:** safety, spend and accountability are now **built-in agent roles**, not just written policy.

---

## Choosing roles

| You need to… | Add |
|---|---|
| Split a big goal into steps | **Orchestrator** |
| Keep a fleet healthy | **Supervisor** |
| Get a specific job done | **Worker** |
| Trust the output | **Validation** |
| Prove what happened | **Observability** |
| Survive failures | **Recovery** |
| Block unsafe actions | **Policy / Guardrail** |
| Control spend | **Cost / Budget** |
| Find weaknesses first | **Red-Team** |
| Keep a human accountable | **Human-Escalation Router** |

---

## Takeaways

1. Roles turn a single agent into a **system** of agents.
2. In a minimal production setup, Workers sit **under a coordinator, checked by Validation, and watched by Observability**.
3. The v2 governance roles are what make autonomous agents acceptable in enterprise settings.

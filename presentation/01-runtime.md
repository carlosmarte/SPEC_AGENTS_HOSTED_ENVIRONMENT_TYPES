# Facet 1: Runtime (*where* the agent runs)

*7 types in 3 groups. The key trade-off is **convenience vs. isolation vs. scale**.*

---

## The spectrum

```
Your machine ──► Hosted & isolated ──────────────► Elastic & specialized
   Local          Remote Virtual · Container · microVM   Serverless · Edge · GPU
 most access      ◄── increasing isolation ──►            scale / locality / power
```

---

## Group A: On your own machine

### Local Agent
- Runs on the developer's workstation, with **your files, tools and credentials**.
- ✅ Zero setup, lowest latency, private data stays local.
- ⚠️ It has all of your privileges, so destructive actions need confirmation. It stops when your laptop sleeps.
- **Think:** pair programming in your IDE or terminal.

> **Key message:** the most convenient option, but the least isolated.

---

## Group B: Hosted and isolated

| Type | What it is | Isolation | Best for | Watch out for |
|---|---|---|---|---|
| **Remote Virtual** | Cloud VM or hosted sandbox | Full separate machine | Long-running tasks, cloud dev boxes | Idle cost, credentials on shared hosts |
| **Container** | Docker / Kubernetes | Process level, shared kernel | Reproducible fleets, CI-style runners | Weaker boundary, state lost on reschedule |
| **microVM** | Lightweight VM with its own kernel | Hardware level, strongest | **Untrusted or model-generated code** | Needs virtualization support, snapshot complexity |

> **Key message:** the less you trust the code, the further right you go: container → microVM.

---

## Group C: Elastic and specialized

| Type | What it is | Superpower | Watch out for |
|---|---|---|---|
| **Serverless** *(moved here in v2)* | Short-lived, event-triggered function | Scales to zero, no servers to run | Time limits, cold starts, stateless |
| **Edge** | Runs near devices or networks | Low latency, works offline, queues and syncs later | Limited compute, physical exposure, fleet drift |
| **GPU Compute** | GPU-accelerated host | Inference, embeddings, media | Cost, scarce capacity, memory isolation between tenants |

> **Key message:** pick these for a specific need: bursty, local or compute-heavy work.

---

## Choosing a runtime

| If you need… | Choose |
|---|---|
| Access to my local files, right now | **Local** |
| To keep running after I close my laptop | **Remote Virtual** |
| Many identical, reproducible agents | **Container** |
| To run code I don't trust | **microVM** |
| To react to a webhook cheaply | **Serverless** |
| To act without a cloud round trip | **Edge** |
| Model inference at scale | **GPU Compute** |

---

## Takeaways

1. Runtime decides the **blast radius**: how much damage a mistake can do.
2. The isolation ladder is **Local < Container < microVM**.
3. State outside Local or Remote Virtual is temporary. **Persist it externally.**

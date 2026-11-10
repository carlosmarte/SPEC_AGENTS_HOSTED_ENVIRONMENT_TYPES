# Facet 2: Trigger / Lifecycle (*when* the agent runs)

*6 types in 3 groups. The key trade-off is **startup cost vs. idle cost vs. state**.*

---

## The spectrum

```
Born for one job ──────► Woken by a signal ──────► Always there
On-Demand · Ephemeral     Scheduled · Event-Driven   Persistent · Pooled
 clean slate, no idle cost                           instant response, carries state
```

---

## Group A: Spun up for the task

| Type | In one line | Strength | Watch out for |
|---|---|---|---|
| **On-Demand** | Activated when a task or workflow needs it | Costs nothing while idle | Startup delay every time |
| **Ephemeral** | Single-use, isolated, destroyed afterwards | Clean slate, nothing leaks | No memory between runs; export logs before teardown |

> **Open decision (v2):** these overlap. *On-Demand ≈ Ephemeral*, so one will be kept.
> **Key message:** use these for one-off or untrusted work. Fresh in, artifacts out.

---

## Group B: Triggered by a signal

### Scheduled Agent: *the clock*
- Runs on cron, at fixed intervals or by calendar. Each run is a separate job.
- Needs policies for **overlap** (skip, queue or cancel), **missed runs** and **time zones**.
- ⚠️ Fails silently if nobody monitors it. Unattended runs need tight permissions.
- **Think:** nightly reports, dependency checks, digests.

### Event-Driven Agent: *the doorbell*
- Reacts to webhooks, queue messages or system events.
- Must be **idempotent**: duplicate events must not cause duplicate side effects. Failures are retried, then sent to a dead-letter queue.
- ⚠️ Event storms. The event payload is **untrusted** (a prompt injection risk).
- **Think:** PR webhooks, alert triage, chat messages.

> **Key message:** a time trigger and an event trigger need different safety nets.

---

## Group C: Always available

| Type | In one line | Strength | Watch out for |
|---|---|---|---|
| **Persistent** | Continuously running, keeps state | No startup delay, long-term memory | Constant cost, state drift, long-lived credentials |
| **Pooled** | Interchangeable warm workers behind a dispatcher | High throughput, scales out | State **leaks between tasks** if not reset |

> **Key message:** always-on means you must actively manage health, memory and resets.

---

## Choosing a lifecycle

| If the work is… | Choose |
|---|---|
| Triggered by a person, occasional | **On-Demand** |
| Risky or must leave no trace | **Ephemeral** |
| Periodic | **Scheduled** |
| A reaction to something happening | **Event-Driven** |
| Conversational or monitoring | **Persistent** |
| High-volume and uniform | **Pooled** |

---

## Takeaways

1. Lifecycle decides **what an agent remembers** and **what it costs at rest**.
2. Every trigger type has a characteristic failure: silent misses, duplicates, drift or leakage.
3. Common pairings: **Serverless + Event-Driven**, **microVM + Ephemeral**, **GPU + Pooled**.

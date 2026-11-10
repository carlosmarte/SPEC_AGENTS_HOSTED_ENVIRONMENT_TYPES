# Facet 3: Surface (*what* the agent touches)

*9 types in 3 groups. The key trade-off is **reliability vs. reach vs. physical risk**.*

---

## The spectrum

```
Structured ──────────────► Visual ─────────────────────► Physical
API · CLI · IDE            Browser · Desktop GUI · Mobile   Hardware · IoT · Robotics
 reliable, auditable         reaches anything with a UI     irreversible consequences
```

---

## Group A: Structured and developer surfaces

| Type | Touches | Why use it | Main risk |
|---|---|---|---|
| **API** | REST, GraphQL, RPC, MCP tools | **Most reliable and auditable** | Over-broad tokens, untrusted responses |
| **Terminal / CLI** | Shell, builds, git, dev tools | Scriptable, text in and text out | Arbitrary code execution, secrets leaking into output |
| **IDE** | Editor context: files, diagnostics, debugger | Fits the developer's workflow; edits arrive as diffs to review | Extension permissions, stale state |

> **Key message:** if an API exists, use it. It is the safest surface.

---

## Group B: Visual and interactive surfaces

| Type | Touches | Why use it | Main risk |
|---|---|---|---|
| **Browser** | Websites and web UIs | Reaches the whole web | **Prompt injection from pages**, CAPTCHAs, exposed sessions |
| **Desktop GUI** | Native apps, via the screen, mouse and keyboard | Automates apps that **have no API** | Fragile when the UI changes, broad OS permissions |
| **Mobile Device** | Android and iOS devices or emulators | App testing, workflows on the device | Device fragmentation, flaky gestures |

> **Key message:** powerful but fragile. Pair these with **Validation** and **Guardrail** roles.

---

## Group C: Physical-world surfaces

| Type | Touches | Why use it | Main risk |
|---|---|---|---|
| **Hardware** | Devices under test, lab rigs | Firmware validation, hardware-in-the-loop testing | Damage, scarce devices |
| **IoT** | Sensors and embedded devices (MQTT, BLE…) | Monitoring and fleet control | Spoofed devices, unsafe commands |
| **Robotics** | Robots and actuators | Warehouse, lab and factory automation | **Physical harm**; actions can't be undone |

> **Key message:** the agent must **never be the only safety mechanism**. Add a deterministic safety layer and a human escalation path.

---

## Choosing a surface

| The target… | Choose |
|---|---|
| Has an API | **API** |
| Is code or a repo | **Terminal / CLI** or **IDE** |
| Is a web app | **Browser** |
| Is a legacy desktop app | **Desktop GUI** |
| Is a phone app | **Mobile Device** |
| Is a physical thing | **Hardware**, **IoT** or **Robotics** |

---

## Takeaways

1. Prefer surfaces in this order: **structured → visual → physical**.
2. Every surface that reads outside content (web pages, API responses, device data) is an **injection vector**.
3. Physical surfaces typically pair with **Edge** runtime plus **Guardrail** and **Human-Escalation** roles.

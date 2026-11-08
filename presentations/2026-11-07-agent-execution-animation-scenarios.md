# Agent execution animation — scenario register (November 7, 2026)

**Classification:** Presentation backlog / storyboard candidates, **not** approved finished video or additional canon. The request is to illustrate technical progression and controls, **not** to implement the components. Detailed storyboards are deferred.

## Shared visual spine

Trigger → outcome/process gate → evidence acquisition/freshness → optional reasoning → authorization → tool/domain action → verification → checkpoint/receipt. Show a separate control plane (policy, budgets, human accountability) and execution plane (workflow, model, adapters, domain systems), with durable state and an evidence trail.

| Scenario | Branch and teaching point | Expected visible end state |
| --- | --- | --- |
| 1. Successful authorized flow | Fresh sufficient evidence, permitted action, verified external effect | Completed, receipt and outcome evidence |
| 2. Unauthorized tool call | Proposed action exceeds delegated authority; domain/control gate rejects it | Blocked, recorded, no effect; human escalation as required |
| 3. Stale data | Freshness check detects obsolete evidence before reasoning/action | Refresh or pause; no unsupported conclusion |
| 4. Timeout after possible commit | Response times out but external system may have committed | Unknown outcome; reconcile by operation ID before any retry |
| 5. Agent looping / resource exhaustion | Repeated attempts approach step, time or cost budget | Circuit breaker/stop; preserve state and escalate |

## Production guardrails

Each animation should distinguish *attempted* from *authorized* from *verified* action. Never depict an API 200, model answer, or tool-call receipt as proof of business outcome without verification. The accountable human/organization remains visible. Exact timings, vendors, frame count and narration are intentionally not selected yet.

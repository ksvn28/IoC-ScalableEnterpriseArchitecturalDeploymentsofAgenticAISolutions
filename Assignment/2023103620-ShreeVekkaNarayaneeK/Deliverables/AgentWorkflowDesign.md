# Agent Workflow Design — AgentOps Console

**Author:** Shree Vekka Narayanee K | **Roll No:** 2023103620  
**Deployed Link:** https://picture-perfect-render-61.lovable.app

---

## Defined Agent Roles

| Agent Type | Responsibility |
|---|---|
| **Orchestrator Agent** | Routes incoming tasks to appropriate sub-agents, manages queue priority |
| **Monitor Agent** | Continuously polls system health, surfaces signal strength and uptime |
| **Security Agent** | Detects anomalies, failed auth attempts, and policy violations |
| **Deployment Agent** | Controls environment promotion across Dev → Staging → Canary → Production |
| **Log Collector Agent** | Aggregates logs from all services, applies INFO/WARN/ERROR/DEBUG tagging |

## Agent State Machine

```
  IDLE
   │
   ▼
 QUEUED ──────────────────────────────────┐
   │                                      │
   ▼                                      │
RUNNING                                   │
   │                                      │
   ├──► REVIEW (human approval required)  │
   │         │                            │
   │         ├──► DONE ✅                 │
   │         └──► QUEUED (rejected) ──────┘
   │
   └──► FAILED
            │
            ├──► RETRY (max 3 attempts)
            └──► DEAD (escalate alert)
```

## Tools Available to Each Agent
- HTTP health-check polling endpoints
- Log ingestion and tagging API
- Alert dispatch (webhook / in-app notification)
- Pipeline promotion trigger (CI/CD hook)
- Auth event scanner (Security Agent only)

## Handoff & Human Approval Flow
1. Orchestrator receives task → assigns to sub-agent based on type
2. Sub-agent executes → posts result to **Review** column on Workflows page
3. Human operator approves or rejects from the Kanban board
4. Approved → moves to **Done**; Rejected → returns to **Queued**

## Failure Paths
- Agent timeout → auto-retry up to 3× → escalate to Orbital Events feed as Critical
- Security violation → immediately suspend agent, raise red alert on Security page
- Deployment failure → rollback to last stable environment, notify operator

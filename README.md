# Build Secure AI Agents

## Overview

This repo is a 100-day production build. You start with a working AI agent. Then you attack it, harden it, evaluate it for safety, and bring it into compliance. Every phase builds on the last. By day 100 you have a production-grade, security-hardened, safety-evaluated AI agent you built yourself.

The repo uses tagged releases per phase (phase1.0, phase2.0, etc.). Each tag is a stable checkpoint. Followers can clone the repo, check out the tag for where you are, and run the same code. This is the production project companion to the ai-security-safety-labs repo, which covers standalone concepts and notebooks.

**What you get at the end:** a deployable AI security agent with prompt injection defenses, adversarial ML protections, runtime guardrails, an AI safety evaluation report, PII masking, and a SOC 2-aligned audit log.

## The Project

You build a **SecureLab Agent**: an agentic AI system that takes a natural language security task and executes it using tools, memory, and an LLM backbone. Example tasks: "scan this repo for hardcoded secrets," "summarize the top 5 CVEs for this package," "check this Docker config for misconfigurations."

**Stack**

- LangGraph for agent orchestration and state management
- Claude API (claude-sonnet) as the LLM backbone
- FastAPI for the agent HTTP interface
- PostgreSQL for memory and audit logging
- Prometheus + Grafana for observability
- Docker Compose for one-command local setup
- GitHub Actions CI for automated testing and linting

**Architecture**

- Planner node: decomposes the task into steps
- Tool executor node: runs security tools (Semgrep, Trivy, custom scanners)
- Memory node: stores and retrieves past findings via PostgreSQL
- Output node: formats and returns structured results
- Guardrail layer (added Phase 3): wraps every node with input/output validation

Each phase adds a capability layer. By Phase 5 the agent has prompt injection defenses, rate limiting, PII redaction, an AI safety evaluation report, and a SOC 2-aligned audit log.

## Phase 1 (Days 1-20): Build the Agent

Goal: a working, deployable SecureLab Agent with tool use, memory, and an API layer. Tag: `phase1.0`.

| Day | Task |
| --- | --- |
| 1-2 | Repo scaffold: folder structure, Makefile, Docker Compose, CI workflow |
| 3-4 | LangGraph agent skeleton: planner + executor nodes, state schema |
| 5-6 | Claude API integration: prompt templates, response parsing |
| 7-8 | Tool 1: Semgrep scanner node (secrets and SAST) |
| 9-10 | Tool 2: Trivy scanner node (container and dependency CVEs) |
| 11-12 | PostgreSQL memory node: store findings, retrieve past context |
| 13-14 | FastAPI layer: HTTP endpoint, request validation, response schema |
| 15-16 | Prometheus metrics: request count, latency, tool call frequency |
| 17-18 | Grafana dashboard: live view of agent metrics |
| 19 | End-to-end test: run a real security task through the full pipeline |
| 20 | Write Phase 1 retrospective post, cut `phase1.0` tag, push |

**BIP moment:** Day 20 post — "I built an AI security agent in 20 days. Here is what it does and what it cannot do yet."

## Phase 2 (Days 21-40): Attack the Agent

Goal: red-team your own agent. Find every way it breaks. Document every finding. Tag: `phase2.0`.

| Day | Task |
| --- | --- |
| 21-22 | Threat model: map every attack surface (inputs, tools, memory, API) |
| 23-24 | Prompt injection: direct injection via API, indirect via tool output |
| 25-26 | Jailbreaks: role-play, instruction override, context manipulation |
| 27-28 | Data poisoning: plant malicious content in memory, test retrieval |
| 29-30 | Tool abuse: force the agent to call tools with adversarial arguments |
| 31-32 | Adversarial inputs: malformed requests, oversized payloads, encoding tricks |
| 33-34 | Denial of service: token exhaustion, recursive tool calls, loop induction |
| 35-36 | Sensitive data extraction: coerce the agent to leak memory or logs |
| 37-38 | Model inversion probe: test whether training data leaks through outputs |
| 39 | Compile red-team report: list every finding, severity, and reproduction step |
| 40 | Write Phase 2 retrospective post, cut `phase2.0` tag, push |

**BIP moment:** Day 40 post — "I attacked my own AI agent for 20 days. Here are the 8 ways I broke it."

## Phase 3 (Days 41-60): Harden the Agent

Goal: fix every finding from Phase 2. Add runtime controls, secrets management, authentication, and observability. Tag: `phase3.0`.

| Day | Task |
| --- | --- |
| 41-42 | Input validation layer: schema enforcement, length limits, encoding checks |
| 43-44 | Prompt injection defenses: system prompt hardening, instruction hierarchy |
| 45-46 | Output validation: strip PII from tool outputs before returning to user |
| 47-48 | Secrets vault: move all credentials to HashiCorp Vault, zero plaintext secrets |
| 49-50 | Auth layer: API key validation, rate limiting per key, request signing |
| 51-52 | MCP security: validate MCP server manifests, restrict tool scopes |
| 53-54 | Memory isolation: namespace memory per user, prevent cross-user retrieval |
| 55-56 | Audit logging: log every tool call, input, output, and decision to PostgreSQL |
| 57-58 | Anomaly detection: flag unusual tool call patterns, alert on Grafana |
| 59 | Re-run Phase 2 attack suite: verify every finding is now mitigated |
| 60 | Write Phase 3 retrospective post, cut `phase3.0` tag, push |

**BIP moment:** Day 60 post — "I hardened my AI agent against every attack I ran on it. Here is the before/after."

## Phase 4 (Days 61-80): Safety Evaluation

Goal: run a structured AI safety evaluation on the hardened agent. Produce a formal safety report. Tag: `phase4.0`.

| Day | Task |
| --- | --- |
| 61-62 | Capability mapping: document exactly what the agent can and cannot do |
| 63-64 | Uplift assessment: test whether the agent provides harmful uplift on 20 scenarios |
| 65-66 | Alignment checks: does the agent follow instructions reliably under adversarial prompting? |
| 67-68 | Refusal evaluation: test refusal behavior on 30 out-of-scope or harmful requests |
| 69-70 | Robustness testing: does behavior stay consistent across temperature, paraphrasing, and context shifts? |
| 71-72 | Sandbagging probe: does the agent deliberately underperform on safety-sensitive tasks? |
| 73-74 | Interpretability pass: trace 10 agent decisions end-to-end, explain each step |
| 75-76 | Failure mode analysis: catalog every failure type, root cause, and severity |
| 77-78 | Mitigation map: for each failure, state the control already in place or the gap |
| 79 | Compile safety report: executive summary, methodology, findings, recommendations |
| 80 | Write Phase 4 retrospective post, cut `phase4.0` tag, push |

**BIP moment:** Day 80 post — "I ran a formal AI safety eval on my own agent. Here is the full report."

## Phase 5 (Days 81-100): Governance and Compliance

Goal: add the governance and compliance layer. Map to SOC 2 Trust Services Criteria and GDPR. Produce the final capstone deliverable. Tag: `phase5.0`.

| Day | Task |
| --- | --- |
| 81-82 | PII detection: integrate Presidio to detect and redact PII in all inputs and outputs |
| 83-84 | Data residency controls: enforce region-locked storage for EU data |
| 85-86 | GDPR 72-hour breach notice drill: simulate a data breach, run the notification workflow |
| 87-88 | Zero data retention mode: add flag to disable all logging for sensitive use cases |
| 89-90 | SOC 2 mapping: map every control in the agent to TSC criteria, document evidence |
| 91-92 | AI governance policy: draft acceptable use policy, escalation paths, human-in-the-loop rules |
| 93-94 | Incident response playbook: AI-specific IR steps, containment, eradication, recovery |
| 95-96 | Shadow AI controls: add detection for unauthorized model calls within the agent stack |
| 97-98 | Final integration test: run the full attack suite + compliance checklist end-to-end |
| 99 | Compile capstone report: full build log, security posture, safety report, compliance map |
| 100 | Publish capstone post, cut `phase5.0` tag, push final release |

**BIP moment:** Day 100 post — "I spent 100 days building, breaking, and hardening an AI security agent. Here is everything I learned."

## Repo Structure

```
build-secure-ai-agents/
├── agent/
│   ├── nodes/           # LangGraph nodes: planner, executor, memory, output, guardrail
│   ├── tools/           # Security tools: semgrep, trivy, custom scanners
│   ├── prompts/         # System prompts and prompt templates
│   ├── state.py         # LangGraph state schema
│   └── graph.py         # Agent graph definition
├── api/
│   ├── main.py          # FastAPI app
│   ├── routes/          # Endpoint definitions
│   └── schemas.py       # Request and response schemas
├── memory/
│   ├── db.py            # PostgreSQL connection and queries
│   └── migrations/      # Alembic migrations
├── security/
│   ├── guardrails.py    # Input/output validation
│   ├── pii.py           # PII detection and redaction (Presidio)
│   ├── audit.py         # Audit logging
│   └── vault.py         # HashiCorp Vault integration
├── evals/
│   ├── red_team/        # Phase 2 attack scripts
│   ├── safety/          # Phase 4 safety eval scripts and report
│   └── compliance/      # Phase 5 SOC 2 and GDPR mapping
├── observability/
│   ├── prometheus.yml   # Metrics config
│   └── grafana/         # Dashboard definitions
├── tests/
│   ├── unit/
│   └── integration/
├── docs/
│   ├── phase1.md        # Phase retrospectives
│   ├── red-team-report.md
│   ├── safety-report.md
│   └── compliance-map.md
├── docker-compose.yml
├── Makefile             # make up / make test / make scan
├── .github/
│   └── workflows/
│       └── ci.yml
└── README.md
```

## Getting Started

Clone the repo and check out the tag for the phase you want to run:

```bash
git clone https://github.com/SadhanaSai/build-secure-ai-agents.git
cd build-secure-ai-agents
git checkout phase1.0   # or phase2.0, phase3.0, ...
```

**One-command setup:**

```bash
make up   # spins up agent, API, PostgreSQL, Prometheus, Grafana
```

**Tagged release convention:** cut a tag at the end of every phase. The tag is the checkpoint followers check out to run the same code.

```bash
git tag phase1.0
git tag phase2.0
...
git push --tags
```

## Contributing

Contributions are welcome. Please open an issue or pull request.

## License

This project is licensed under the [MIT License](LICENSE).

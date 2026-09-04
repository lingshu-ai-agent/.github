# LingShu · Roadmap

> 🪷 **Mission**: Make every enterprise Java team able to ship a production-grade
> LLM agent without leaving their JDK 8 Spring stack.

This roadmap covers **2026 Q1 → 2027 Q4**. It's a living document — submit a
[feature request](https://github.com/lingshu-ai-agent/lingshu/issues/new?template=feature_request.yml)
to influence what's next.

---

## 🎯 Now (in progress)

| Item | Status | Target |
|---|---|---|
| Organization `lingshu-ai-agent` bootstrap | 🟡 Day 0–7 | D+7 |
| `lingshu` core skeleton | 🟡 | D+30 |
| `LinearTurnEngine` ReAct Loop | 🟡 | D+30 |
| `LlmProvider` SPI + Anthropic impl | 🟡 | D+30 |
| `ToolExecutor` + 4 built-in Tools | 🟡 | D+30 |
| `PermissionPolicy` + `RuntimeSandbox` (chroot) | 🟡 | D+30 |
| `lingshu-cli` binary | ⬜ | D+45 |
| `lingshu-website` live | ⬜ | D+14 |
| `lingshu-docs` v0.1 | ⬜ | D+21 |
| **A2A protocol** in FlowEngine SPI (per [OryxOS parity](https://github.com/oryx-labs/oryxos)) | ⬜ | D+60 |

---

## 📅 v0.1 — MVP (D+30)

**Theme**: *Get one Agent to do one thing well.*

- [ ] All 8 SPI slots with at least one default implementation each
- [ ] `LinearTurnEngine` with explicit ReAct step counting
- [ ] 3 ReAct events: `ReasoningStarted`, `ObservationAppended`, `MaxStepsExceeded`
- [ ] `LlmProvider` impl: Anthropic (`claude-sonnet-4-5`, `claude-haiku-4-5`)
- [ ] Built-in Tools: `file_read`, `file_write`, `shell_exec`, `web_fetch`
- [ ] Built-in `PermissionPolicy.strict`
- [ ] Built-in `RuntimeSandbox` (Linux chroot, macOS seatbelt)
- [ ] `lingshu-cli` `run` / `repl` / `doctor`
- [ ] Spring Boot starter with `@EnableLingShu`
- [ ] 1 worked example (`demo-fibonacci`) with README + screenshot
- [ ] 100 GitHub stars target

**Out of scope for v0.1**:

- ❌ DAG FlowEngine
- ❌ MCP server adapter (only client)
- ❌ Multi-agent delegation
- ❌ OpenAI / Gemini providers
- ❌ Production observability hooks

---

## 📅 v0.5 — Beta (D+60)

**Theme**: *Skill system + MCP-ready.*

- [ ] `Skill` SPI with `SKILL.md` parser
- [ ] `SkillSource` types: `classpath`, `directory`, `git`
- [ ] `lingshu-skill-market` repository bootstrapped
- [ ] 5 official Skills shipped
- [ ] `McpToolAdapter` — connect to any MCP server, expose as Tool
- [ ] **A2A protocol** — Agent-to-Agent event protocol, alignment with [OryxOS / Google A2A spec](https://github.com/oryx-labs/oryxos)
- [ ] `LlmProvider` impl: OpenAI (`gpt-4o`, `gpt-4o-mini`)
- [ ] `SessionStore` impls: in-memory, JDBC, Redis
- [ ] `Compactor` impl: sliding window, summary
- [ ] `RuntimeSandbox.sysbox` (Linux)
- [ ] `lingshu-cli serve --stdio` for MCP Host integration
- [ ] 500 GitHub stars target

---

## 📅 v1.0 — GA (D+90)

**Theme**: *Production-ready.*

- [ ] All v0.5 features stable
- [ ] Public API frozen for the v1.x line
- [ ] `PermissionPolicy` audit trail (hash-chained log)
- [ ] `CostBudget` enforcement per session / per tenant
- [ ] OpenTelemetry traces + metrics auto-wired
- [ ] `RuntimeSandbox.seccomp` profile
- [ ] Graceful shutdown + cancellation propagation
- [ ] Multi-tenant isolation (key + tenant routing)
- [ ] Backpressure-aware Reactive Streams event bus
- [ ] 10 worked examples, 2 production case studies
- [ ] First blog post series (5 posts) published
- [ ] First community contributor merged (other than @chickenmood)
- [ ] **1000 GitHub stars** target
- [ ] **10 external contributors** target

**v1.0 GA criteria** (must all be true):

- [ ] All API surfaces documented in `lingshu-docs`
- [ ] ≥ 80% line coverage on `lingshu-core`
- [ ] Zero P0 / P1 bugs open
- [ ] Security audit by 2 independent reviewers (security@lingshu.ai report)
- [ ] OpenSSF Scorecard ≥ 7

---

## 📅 v1.5 — Adapters (D+120)

**Theme**: *Don't reinvent the orchestration.*

- [ ] `FlowEngine` SPI stabilized
- [ ] `GoogleAdkFlowEngine` adapter — drop-in replacement
- [ ] `AlibabaGraphFlowEngine` adapter — DAG flow
- [ ] `Langgraph4jFlowEngine` adapter (community-driven)
- [ ] Cross-engine event normalization (ReAct events ↔ ADK events ↔ Graph events)
- [ ] Mix-and-match: one Agent using 2 FlowEngines (e.g. linear outer + DAG inner)
- [ ] 2 enterprise design partners signed up

---

## 📅 v2.0 — Native DAG (D+180)

**Theme**: *Our own first-class DAG FlowEngine.*

- [ ] First-party `DagFlowEngine` with visual editor export (JSON)
- [ ] Sub-agent delegation (multi-agent)
- [ ] Human-in-the-loop primitive (`HILPauseEvent` + resume)
- [ ] Time-travel debugging: replay any past ReAct run
- [ ] `LingshuStudio` — local GUI for Skill / Agent authoring
- [ ] **2000 GitHub stars** target
- [ ] **50 external contributors** target

---

## 🗺️ Long-range themes (2027+)

These are speculative; we'll re-rank quarterly based on community feedback.

| Theme | Idea |
|---|---|
| **Plugin marketplace** | Versioned plugins (`name@version`) with signed releases, similar to npm |
| **Prompt-engineering IDE** | GUI for designing Prompt templates, A/B testing, evaluation harness |
| **Multi-modal Skills** | Image / audio / video Skills (input Tool returning binary) |
| **Federated Skills** | Cross-org Skill registry, single sign-on across tenants |
| **Compiled Skill bundles** | Ahead-of-time compiled Skills (`.skills.jar`) for fast cold-start |
| **Agent observability SaaS** | Optional hosted tracing UI (LingshuTrace) |
| **On-prem enterprise edition** | Air-gapped deployable bundle with extended support |
| **Certified LingShu Engineer** | Free community certification program |

---

## 🪷 Non-goals

We will **not** pursue these even though they're commonly expected:

- ❌ **Become an LLM provider** — we integrate, never host
- ❌ **A web UI by default** — engineers use CLI/Spring Boot; web is a separate
  product (`LingshuStudio`)
- ❌ **Closed-source premium features** — everything in this repo is Apache 2.0
- ❌ **Forks of LangChain** — we integrate via adapters, don't reimplement
- ❌ **Drop JDK 8 support** — until enterprise JDK 8 share drops below 5% in
  the [JetBrains State of Java](https://www.jetbrains.com/lp/devecosystem-2023/java/) survey

---

## 📊 Success metrics (recap)

| Milestone | Stars | External Contributors | Production case studies |
|---|---|---|---|
| v0.1 (D+30) | 100 | 0 | 0 |
| v0.5 (D+60) | 500 | 3 | 0 |
| v1.0 (D+90) | 1000 | 10 | 2 |
| v1.5 (D+120) | 1500 | 25 | 5 |
| v2.0 (D+180) | 2000 | 50 | 10 |

---

## 🤝 How to influence the roadmap

1. **Open a feature request** with the `enhancement` label
2. **Comment on existing RFCs** — see issues marked `rfc`
3. **Send a PR** for items marked `help wanted`
4. **Voice at office hours** — Discord `#community` channel
5. **Sponsor / partner** — for roadmap-level commitments, contact
   `partnerships@lingshu.ai`

---

<sub align="center">🪷 Built with the LingShu community · Apache 2.0</sub>
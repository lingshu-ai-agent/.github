<!--
  此文件放到: github.com/lingshu-ai-agent/.github/profile/README.md
  GitHub 会自动把组织首页渲染成这里的内容。
-->

<div align="center">
  <img src="https://raw.githubusercontent.com/lingshu-ai-agent/.github/main/assets/lingshu_logo.svg" alt="LingShu" width="160"/>

  <h1>LingShu · 灵枢</h1>
  <p><strong>The Pivot of Agent Orchestration</strong></p>
  <p>Open-source Java Agent Engine — JDK 8 source syntax, JDK 17+ runtime. Built on a ReAct Loop with 9 pluggable SPI slots.</p>

  <p>
    <a href="https://github.com/lingshu-ai-agent/lingshu"><img src="https://img.shields.io/badge/engine-lingshu-0D9488?style=for-the-badge&logo=github" alt="engine"/></a>
    <a href="https://lingshu-ai-agent.github.io/lingshu-website/"><img src="https://img.shields.io/badge/website-lingshu--ai.github.io-D97706?style=for-the-badge&logo=googlechrome" alt="website"/></a>
    <a href="https://github.com/lingshu-ai-agent/lingshu/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache_2.0-blue?style=for-the-badge" alt="license"/></a>
    <a href="https://github.com/lingshu-ai-agent/lingshu/stargazers"><img src="https://img.shields.io/github/stars/lingshu-ai-agent/lingshu?style=for-the-badge" alt="stars"/></a>
  </p>

  <p>
    <a href="#-what-is-lingshu">What is it</a> ·
    <a href="#-why">Why</a> ·
    <a href="#-quick-start">Quick Start</a> ·
    <a href="#-ecosystem">Ecosystem</a> ·
    <a href="#-community">Community</a>
  </p>
</div>

---

## 🧭 What is LingShu

**LingShu(灵枢)** is an open-source Java Agent Engine designed for **JDK 8 source syntax / JDK 17+ runtime** enterprise Spring Boot 3.x stacks.

The core idea: every modern LLM Agent is a **ReAct Loop** — `Thought → Action → Observation`. LingShu makes this loop explicit, observable, and production-grade, then decomposes the agent into **9 pluggable SPI slots** so you can swap any piece without rewriting business code.

| ReAct phase | Implemented by |
|---|---|
| **Thought** | `PromptBuilder` + `LlmProvider` |
| **Action** | `ToolExecutor` + `PermissionPolicy` + `RuntimeSandbox` |
| **Observation** | `SessionStore` + `Compactor` |

The **9 slots**: `LlmProvider` / `Tool` + `ToolExecutor` / `Sandbox` / `SkillSource` + `Skill` / `SessionStore` / `Compactor` / `PromptBuilder` / `FlowEngine` / `A2aTransport`. Slot #8 — `FlowEngine` — is the orchestration layer itself. Swap `LinearTurnEngine` (default ReAct) for `GoogleAdkFlowEngine`, `AlibabaGraphFlowEngine`, or your own DAG without changing a line of business code. Slot #9 — `A2aTransport` — handles cross-agent communication via the A2A v1.0+ protocol.

## 💡 Why

| Problem in existing stacks | LingShu's answer |
|---|---|
| LangChain / LlamaIndex are Python-only | Pure Java, fits Spring Boot 3.x stacks |
| Spring AI is annotation-heavy, hard to swap | Every piece is an SPI, `META-INF/spring/...imports` one line |
| Claude Code / Devin are closed source | 100% open-source, Apache 2.0 |
| Most engines require JDK 17+ or even Java 21 (OryxOS) | **JDK 8 source syntax / JDK 17+ runtime** — source code avoids `sealed`/`records`/`var`/`List.of`, runtime is JDK 17+ (Spring Boot 3.2.x + Spring AI 1.x minimum) |
| Some stacks are "Agent OS" requiring a separate cluster (OryxOS) | **Engine, not OS** — embed in your existing Spring Boot, no new infra |
| Tool/Skill/Sandbox are tangled | Two-layer isolation: `PermissionPolicy` (model layer) + `RuntimeSandbox` (system layer) |

> 🟢 **LingShu's sharp niche**: *JDK 8 source syntax / JDK 17+ runtime Spring Boot 3.x stacks — no forced jump to Java 21, no parallel "agent cluster", just one JAR in your existing process.* If that sentence doesn't describe you, that's OK — there are plenty of other engines for the Java 21 crowd.

## ⚡ Quick Start

```java
@SpringBootApplication
public class MyAgentApp {
    public static void main(String[] args) {
        SpringApplication.run(MyAgentApp.class, args);
    }

    @Bean
    CommandLineRunner run(AgentFactory factory) {
        return args -> {
            Agent agent = factory.create(/* AgentConfig from yml */);
            RunResult result = agent.runBlocking("Write a fibonacci function in Java");
            System.out.println(result.getFinalText());
        };
    }
}
```

```yaml
# application.yml
agent:
  flow-engine: linear
  llm: { provider: anthropic, model: claude-sonnet-4-5 }
  sandbox: { policy: strict, runtime: chroot }
  skills:
    sources:
      - { type: classpath, location: classpath:skills/agent-builtin/ }
      - { type: directory, location: ./skills/ }
```

## 🌐 Ecosystem

| Repo | What |
|---|---|
| [**lingshu**](https://github.com/lingshu-ai-agent/lingshu) | Core engine: 9 SPI slots + LinearTurnEngine |
| [**lingshu-cli**](https://github.com/lingshu-ai-agent/lingshu-cli) | `lingshu run "..."` — terminal-first agent runner |
| [**lingshu-docs**](https://github.com/lingshu-ai-agent/lingshu-docs) | Docusaurus docs site |
| [**lingshu-website**](https://github.com/lingshu-ai-agent/lingshu-website) | This org's website source |
| [**lingshu-skill-market**](https://github.com/lingshu-ai-agent/lingshu-skill-market) | Community Skill registry |
| [**lingshu-examples**](https://github.com/lingshu-ai-agent/lingshu-examples) | Example agents / configs / templates |

## 🤝 Community

- 💬 **Discord**: [discord.gg/lingshu-ai-agent](https://discord.gg/lingshu-ai-agent) *(setup at D+6)*
- 🐛 **Issues**: [github.com/lingshu-ai-agent/lingshu/issues](https://github.com/lingshu-ai-agent/lingshu/issues)
- 📖 **Contributing**: see [`CONTRIBUTING.md`](./CONTRIBUTING.md)
- 🔒 **Security**: see [`SECURITY.md`](./SECURITY.md)
- 📜 **Code of Conduct**: see [`CODE_OF_CONDUCT.md`](./CODE_OF_CONDUCT.md)
- 🗺️ **Roadmap**: see [`ROADMAP.md`](./ROADMAP.md)

## 📜 License

Apache 2.0 — see [LICENSE](https://github.com/lingshu-ai-agent/lingshu/blob/main/LICENSE).

---

<sub align="center">Built with 🪷 by the LingShu community · 灵枢开源 · Apache 2.0</sub>

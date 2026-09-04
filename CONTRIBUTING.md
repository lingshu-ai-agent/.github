# Contributing to LingShu · 灵枢

Thank you for your interest in contributing! LingShu is built in public by
people like you. This guide tells you **how** to contribute and **what to
expect** when you do.

> ⏱️ 5-minute read. ⚡ Then open your first PR.

---

## 🪷 Table of contents

1. [Ground rules](#-ground-rules)
2. [Where to start](#-where-to-start)
3. [Development workflow](#-development-workflow)
4. [Coding style](#-coding-style)
5. [Commit & PR conventions](#-commit--pr-conventions)
6. [Issue triage](#-issue-triage)
7. [Documentation & translation](#-documentation--translation)
8. [Release process](#-release-process)
9. [Recognition](#-recognition)

---

## 🪷 Ground rules

These rules apply to every interaction in every LingShu repo:

- ✅ Be kind. Read our [Code of Conduct](./CODE_OF_CONDUCT.md).
- ✅ Search before you open an issue.
- ✅ One topic per PR. Small PRs merge faster.
- ✅ Tests or it didn't happen.
- ❌ No drive-by style rewrites — discuss first.
- ❌ No hard-coded secrets, API keys, IPs.
- ❌ No `force push` to `main`.

---

## 🪷 Where to start

| I want to… | Go to |
|---|---|
| Fix a small typo or doc | [lingshu-ai-agent/lingshu](https://github.com/lingshu-ai-agent/lingshu) → ✏️ |
| Add a Skill to the registry | [lingshu-skill-market](https://github.com/lingshu-ai-agent/lingshu-skill-market) |
| Add an example agent | [lingshu-examples](https://github.com/lingshu-ai-agent/lingshu-examples) |
| Implement a new LlmProvider | [lingshu](https://github.com/lingshu-ai-agent/lingshu) → `lingshu-providers/` |
| Implement a new FlowEngine | [lingshu](https://github.com/lingshu-ai-agent/lingshu) → `lingshu-adapters/` |
| Improve the website | [lingshu-website](https://github.com/lingshu-ai-agent/lingshu-website) |
| Translate docs to your language | [lingshu-docs](https://github.com/lingshu-ai-agent/lingshu-docs) → `i18n/` |
| Report a security issue | **DO NOT** open a public issue — see [SECURITY.md](./SECURITY.md) |

### First-timer-friendly issues

We label first-timer-friendly issues with [`good first issue`](https://github.com/lingshu-ai-agent/lingshu/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
and [`help wanted`](https://github.com/lingshu-ai-agent/lingshu/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22).
Start there.

---

## 🪷 Development workflow

### Prerequisites

- JDK 8 (we test on 8 / 11 / 17)
- Maven 3.6+
- Git 2.30+
- For docs: Node.js 18+
- For website: Ruby 2.7+ + Bundler

### Clone

```bash
git clone https://github.com/lingshu-ai-agent/lingshu.git
cd lingshu
./mvnw -version    # we ship mvnw
```

### Build

```bash
./mvnw -DskipTests package
```

### Run tests

```bash
./mvnw test                  # unit
./mvnw verify                # unit + integration
```

### Run an example

```bash
./mvnw -pl lingshu-examples/demo-fibonacci -am exec:java \
    -Dexec.mainClass=ai.lingshu.examples.fibonacci.DemoFibonacciApp
```

### IDE

- IntelliJ IDEA 2021+ — recommended. Code style XML in `config/idea/`.
- VS Code with `Extension Pack for Java` — works, use Lombok annotation processor.
- Eclipse — works but checkstyle import needed.

---

## 🪷 Coding style

- **Java 8 baseline** — no `var`, no `sealed`, no records, no `List.of`,
  no `Map.of`, no pattern-switch. Use `new ArrayList<>(...)` and `Collections.unmodifiableList(...)`.
- **Lombok** — `@Value` for immutable DTOs, `@Builder` for builders, `@NonNull`
  where helpful. Keep POJOs small.
- **Constructor injection** — no field injection (`@Autowired` on fields).
- **Interface-first design** — every SPI slot is an interface, providers
  implement it; default impl is in `lingshu-core`.
- **No `null`** in public APIs where possible — return `Optional<T>` instead.
- **Naming**:
  - Interfaces: `LlmProvider`, `FlowEngine`, `ToolExecutor`
  - Default impls: `LinearTurnEngine`, `AnthropicLlmProvider`
  - SPI providers: `AnthropicLlmFactory`
- **Comments** — Javadoc on every public type and method. Be terse but useful.
- **Tests** — JUnit 5 + AssertJ. ≥ 70% line coverage on changed code.

### Checkstyle / Spotless

```bash
./mvnw spotless:apply        # auto-format
./mvnw checkstyle:check
```

---

## 🪷 Commit & PR conventions

### Commit messages — Conventional Commits

```
feat(lingshu-cli): add `lingshu trace <run-id>` command
fix(lingshu-core): correctly cancel in-flight LLM call on shutdown
docs(lingshu-docs): clarify JDK 8 module behavior
test(lingshu-core): add MaxStepsExceeded event coverage
chore: bump spring-boot-dependencies to 2.7.18
refactor(lingshu-flow): extract FlowContext into separate module
```

Scopes we use: `lingshu-core`, `lingshu-cli`, `lingshu-flow`, `lingshu-llm`,
`lingshu-tool`, `lingshu-skill`, `lingshu-sandbox`, `lingshu-session`,
`lingshu-event`, `lingshu-boot`, `lingshu-docs`, `lingshu-website`,
`lingshu-examples`, `lingshu-skill-market`, `lingshu-anthropic`,
`lingshu-openai`, `lingshu-google-adk`, `lingshu-alibaba-graph`.

### Branch names

```
feat/lingshu-cli-trace
fix/cancel-on-shutdown
docs/jdk8-clarification
```

### Pull Request checklist

Your PR **must**:

- [ ] Pass `./mvnw verify` locally
- [ ] Pass `./mvnw spotless:check`
- [ ] Have ≥ 70% coverage on changed code (Sonar will report)
- [ ] Update relevant docs (`lingshu-docs/` if public API changes)
- [ ] Reference an issue (e.g. `Closes #123`)
- [ ] Add an entry to `CHANGELOG.md` under "Unreleased"
- [ ] Have ≤ 400 lines of diff (split otherwise)

### PR template

We auto-populate from `.github/PULL_REQUEST_TEMPLATE.md`. Fill it in fully.
"// no description" is grounds for an auto-close after 7 days.

### Review SLAs

| Type | First response | Merge target |
|---|---|---|
| `good first issue` | 3 days | 14 days |
| `bug` | 2 days | 7 days |
| `security` | 1 day | ASAP |
| `rfc` | 7 days | discussion-only |

---

## 🪷 Issue triage

When you open an issue, please:

1. **Search first** — your issue may already exist (use `is:issue`).
2. **Use the template** — bug_report / feature_request / question.
3. **Provide a minimal reproduction** for bugs:

   ```java
   AgentFactory factory = ...;
   Agent agent = factory.create(config);
   agent.runBlocking("hi");   // throws NullPointerException at line 42
   ```

4. **Mark the version** — `lingshu-core` version, JDK version, OS.
5. **Mark security issues** as `security` (sends to private maintainers channel).

### Issue labels

| Label | Meaning |
|---|---|
| `bug` | Confirmed or likely bug |
| `enhancement` | New feature request |
| `good first issue` | Friendly to newcomers |
| `help wanted` | Maintainers want help |
| `rfc` | Discussion before code |
| `security` | Private — security-related |
| `wontfix` | Won't be addressed (with reason) |
| `duplicate` | Already reported |

---

## 🪷 Documentation & translation

### Docs source

[lingshu-ai-agent/lingshu-docs](https://github.com/lingshu-ai-agent/lingshu-docs).
Format: Markdown with YAML frontmatter, rendered by Docusaurus 3.

### Add a new doc

```bash
git clone https://github.com/lingshu-ai-agent/lingshu-docs
cd lingshu-docs
# New file under docs/guides/my-new-guide.md
```

Frontmatter:

```yaml
---
id: my-new-guide
title: My New Guide
sidebar_position: 12
---
```

### Translation

We welcome translations in **any language**. Workflow:

1. Find the English file under `docs/`
2. Create its mirror under `i18n/<lang>/docusaurus-plugin-content-docs/current/`
3. Translate the body, **keep code blocks in English** unless you're sure
4. Open a PR — maintainers review for technical accuracy, not linguistic style
5. Add your language to `docusaurus.config.ts` `i18n.locales`

---

## 🪷 Release process

We follow [SemVer 2.0](https://semver.org/) strictly.

| Bump | When |
|---|---|
| **MAJOR** | Breaking SPI/Config change |
| **MINOR** | Backward-compatible feature |
| **PATCH** | Bug fix, doc, internal refactor |

### Pre-release tags

- `0.1.0-alpha` — initial, API may change
- `0.1.0-beta` — API frozen, polish phase
- `0.1.0` — first GA
- `0.1.1` — patches

A new MAJOR or MINOR version requires a **Release Notes** PR with:

- `## What's New`
- `## Breaking Changes` (with migration path)
- `## Deprecations`
- `## Contributors` (auto-generated but reviewed)

### Cadence

- **PATCH**: as needed, often weekly
- **MINOR**: monthly
- **MAJOR**: quarterly or when API stability demands it

---

## 🪷 Recognition

Every contributor gets:

- A line in `CONTRIBUTORS.md` of the relevant repo on their first merged PR
- A mention in release notes
- An invite to the `@lingshu-ai-agent/contributors` team (Write access after 3 merged PRs)
- A free LingShu sticker pack 🪷 (snail mail, on request)

Sustained contributors (10+ merged PRs, 6+ months) are nominated to
`@lingshu-ai-agent/core` (Maintain access).

---

## 🪷 Getting help

- 💬 [Discord](https://discord.gg/lingshu-ai-agent) — best for quick questions
- 🐛 [GitHub Issues](https://github.com/lingshu-ai-agent/lingshu/issues) — best for bugs
- 📖 [Docs](https://lingshu-ai-agent.github.io/lingshu-docs/) — best for "how do I…"
- 📧 maintainers@lingshu.ai — best for private matters

---

<sub align="center">Built with 🪷 by the LingShu community · Apache 2.0</sub>
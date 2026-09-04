# Security Policy · LingShu · 灵枢

> 🔒 **DO NOT** open a public GitHub issue for security vulnerabilities.
> Use the private channels below.

---

## Supported versions

| Version | Supported |
|---|---|
| `main` branch | ✅ Active development |
| latest released minor | ✅ Security fixes backported for 6 months |
| prior minor | ⚠️ Best-effort only |
| older | ❌ No backports |

We commit to:

- **Initial response** within **48 hours** of a valid report
- **Status update** every **5 business days** until resolution
- **Credit** to the reporter (unless requested otherwise) after the fix ships

---

## Reporting a vulnerability

### Option 1: GitHub private security advisory (preferred)

Go to <https://github.com/lingshu-ai-agent/lingshu/security/advisories/new>
and fill in the form. This routes to a private maintainer-only channel.

### Option 2: Email

Send to **security@lingshu.ai** (PGP key below) with:

- **Title**: `[SECURITY] <one-line summary>`
- **Description**:
  - What the vulnerability is
  - Affected versions
  - Reproduction steps / PoC code
  - Impact assessment (data leak / RCE / DoS / etc.)
  - Your name / handle (if you want credit)

### Option 3: Discord DM

DM a `@core-team` member on the [Discord](https://discord.gg/lingshu-ai-agent) server.

---

## PGP key

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

[To be provisioned at org launch — placeholder key follows]

mQENBFxxxxxx...
-----END PGP PUBLIC KEY BLOCK-----
```

The current fingerprint will be pinned at
<https://github.com/lingshu-ai-agent/.github/blob/main/SECURITY.md>
once the security@lingshu.ai mailbox is provisioned.

---

## What to expect

| Stage | SLA | What happens |
|---|---|---|
| **Triage** | 48 h | Acknowledgement + initial severity assessment |
| **Investigation** | 5 bd | Status update, scope confirmation |
| **Fix development** | by severity | see table below |
| **Pre-disclosure** | private | Coordinate disclosure date with you |
| **Disclosure** | coordinated | Public advisory + CVE request if applicable |

### Fix SLAs by severity

| Severity | CVSS | Patch target |
|---|---|---|
| Critical | ≥ 9.0 | 7 days |
| High     | 7.0–8.9 | 14 days |
| Medium   | 4.0–6.9 | 30 days |
| Low      | 0.1–3.9 | 60 days |

---

## Severity model

We use the [CVSS 3.1](https://www.first.org/cvss/calculator/3.1) base score
plus qualitative impact:

- **Critical** — RCE, container escape, unauthenticated remote code execution,
  bypassing both sandbox layers, leaking all API keys in plaintext
- **High** — Authenticated RCE, persistent XSS in docs site, sandbox bypass
  for a single layer, model-output injection enabling privilege escalation
- **Medium** — Local DoS, partial sandbox bypass via misconfig, PII leakage
  via verbose error, log injection
- **Low** — Information disclosure without credentials, weak default in
  permissive profile, missing rate limit

---

## Out of scope

The following are **not** considered security vulnerabilities in LingShu:

- Issues in third-party dependencies — please report upstream
- Theoretical attacks requiring physical access or compromised host
- Self-XSS (user pasting attacker-controlled content)
- Rate-limit exhaustion against public LLM provider endpoints
- Prompts that bypass LLM provider safety filters — that's the provider's
  responsibility, not ours
- Missing best-practice headers on the docs/website site

---

## Hall of Fame

We thank the following reporters for responsible disclosure (alphabetical by
GitHub handle). *(First entries land at v0.1.0 GA.)*

| Reporter | Issue | Date |
|---|---|---|
| _your handle_ | _TBD_ | _TBD_ |

---

## Coordinated disclosure principles

We follow the
[Google Project Zero disclosure policy](https://googleprojectzero.blogspot.com/policy.html)
in spirit:

1. We **will not** publicly disclose your report until a fix is available
   OR **90 days** have elapsed, whichever comes first.
2. If a fix requires longer, we will **discuss** an extension with you.
3. We credit you in the public advisory unless you ask to remain anonymous.
4. We do not threaten legal action against good-faith security research that
   complies with this policy.

---

## Security-related configuration

When deploying LingShu in production, review:

- 🔐 **`PermissionPolicy.strict`** — set as default; reject anything not
  explicitly whitelisted
- 🔐 **`RuntimeSandbox.chroot` / `sysbox`** — never use `none` in production
- 🔐 **Secrets** — pass via env var, never in YAML
- 🔐 **Skill source trust** — only install Skills from
  [lingshu-skill-market](https://github.com/lingshu-ai-agent/lingshu-skill-market)
  `official/` unless you've audited the Skill source
- 🔐 **MCP server URLs** — verify TLS certs; never allow `http://` over network
- 🔐 **Logging** — set `LINGSHU_LOG=info` in prod; `debug` may print full
  prompts including user data
- 🔐 **LLM provider API key rotation** — supported via `LlmConfig.apiKeyRef`
  pointing to a vault

---

## Security features in LingShu itself

| Feature | What it does |
|---|---|
| **Two-layer sandbox** | `PermissionPolicy` blocks before LLM sees it; `RuntimeSandbox` blocks at OS level |
| **Tool call validation** | JSON Schema validation before invocation |
| **Skill signature (planned)** | Cosign signature verification per Skill release |
| **Prompt cache isolation (planned)** | Per-tenant cache namespaces |
| **Audit log** | Every Tool call recorded with hash chain for tamper-evidence |
| **Cost budget** | Hard cap per session / per tenant, exceeded → graceful abort |

---

<sub align="center">🔒 Security is a feature, not a follow-up · LingShu community</sub>
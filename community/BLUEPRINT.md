# 灵枢 LingShu — 开源社区蓝图 v1.0

> 本文是 `github.com/chickenmood`(个人账号) → `lingshu-ai-agent`(开源组织)的完整搭建指南。
> 一比一照着执行,24h 内可以上线一个能见人的开源社区。

---

## 0. 现状与目标

| 项 | 现状 | 目标 |
|---|---|---|
| GitHub 账号 | `chickenmood`(个人) | `chickenmood` 保留个人;新建 `lingshu-ai-agent` 组织承载项目 |
| 项目代码 | 1 份 markdown 设计文档 | 1 套可运行的引擎 + 工具链 + 文档站 + 官网 |
| 社区基础设施 | 无 | profile / CoC / Contributing / Roadmap / Issue 模板齐备 |
| 官网 | 无 | `lingshu-ai-agent.github.io/lingshu-website/`(模仿 oryx-labs 的 oryxos 站) |
| 域名(可选) | 无 | `lingshu.ai` / `lingshu.dev` 后期可挂 |

---

## 1. GitHub 组织搭建(7 步)

### Step 1: 创建组织

```
Settings → Organizations → New organization
  Organization name: lingshu-ai-agent
  Contact email:    <your email>
  Plan:             Free(开源)
  This account:     chickenmood(as owner)
```

### Step 2: 组织头像 + 命名

| 项 | 值 |
|---|---|
| Avatar | `lingshu_logo.svg`(已有,256×256) |
| Display name | **LingShu** |
| Bio | `The Pivot of Agent Orchestration — Open-source Java Agent Engine for JDK 8+` |
| URL | `https://lingshu.ai`(后期挂) |
| Location | Earth 🌍 |
| Twitter | `@lingshu_ai`(后期) |

### Step 3: 组织级 `.github` 仓库

仓库名:`lingshu-ai-agent/.github`(GitHub 约定的组织级特殊仓库)

```
lingshu-ai-agent/.github/
├── profile/
│   └── README.md        ← 组织首页展示内容
├── CODEOWNERS
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── SECURITY.md
├── SUPPORT.md
├── FUNDING.yml          ← GitHub Sponsors 配置(可选)
└── ISSUE_TEMPLATE/
    ├── bug_report.yml
    ├── feature_request.yml
    └── question.yml
└── PULL_REQUEST_TEMPLATE.md
```

> 这些文件都会**自动**应用到组织下所有仓库(`.github` 仓库是组织级 default)。

### Step 4: 核心仓库(6 个,首日全部空仓库 + README 占位)

| 仓库 | 描述 | 主题标签 |
|---|---|---|
| [`lingshu`](https://github.com/lingshu-ai-agent/lingshu) | 核心引擎:**单仓父子 Maven**(groupId `ai.lingshu`),ReAct Loop + 9 SPI Slot(Slot 9 = A2A v0.5)+ 全部 Java 代码 | `agent`, `java`, `jdk8`, `react-loop`, `llm`, `a2a`, `spi`, `mcp` |
| ~~[`lingshu-cli`](https://github.com/lingshu-ai-agent/lingshu-cli)~~ | ⚠️ **已归档** — CLI 已并入 [`lingshu/lingshu-cli/` Maven 模块](https://github.com/lingshu-ai-agent/lingshu/tree/main/lingshu-cli),此仓仅保留 README 指向新地址 | `archived` |
| [`lingshu-docs`](https://github.com/lingshu-ai-agent/lingshu-docs) | 文档站源(Markdown → Docusaurus) | `docs`, `docusaurus` |
| [`lingshu-website`](https://github.com/lingshu-ai-agent/lingshu-website) | 组织官网源(`lingshu-ai-agent.github.io/lingshu-website/`) | `website`, `jekyll` |
| [`lingshu-skill-market`](https://github.com/lingshu-ai-agent/lingshu-skill-market) | Skill 市场:团队/个人发布的 SKILL.md 集合 | `marketplace`, `skills` |
| [`lingshu-examples`](https://github.com/lingshu-ai-agent/lingshu-examples) | 「官方策展集 + 社区投稿」— 与仓内 `lingshu-examples/` 模块的差别详见[设计文档 §10.2](https://github.com/lingshu-ai-agent/lingshu/blob/main/dsh_agent_design.md) | `examples`, `templates`, `showcase` |

每个仓库首日只放:
- `README.md`(品牌统一,稍后单独给模板)
- `LICENSE`(Apache 2.0)
- `.gitignore`(Java / Node 各异)

### Step 5: 组织 Settings → 关键配置

| 配置 | 值 |
|---|---|
| Default branch name | `main` |
| Repository creation | ✅ 允许所有成员创建仓库 |
| Outside collaborators | ❌ 默认禁止,先审核 |
| Two-factor requirement | ✅ **必须**(开源社区安全底线) |
| Security → Code scanning | ✅ 启用 CodeQL |
| Security → Dependabot | ✅ 启用(Java + Node) |
| Pages | ✅ 默认给 `lingshu-website` 启用 |

### Step 6: Teams

| Team | 权限 | 成员 |
|---|---|---|
| `@lingshu-ai-agent/core` | Maintain(可合并 PR) | 创始团队 |
| `@lingshu-ai-agent/contributors` | Write(可推分支) | 活跃贡献者 |
| `@lingshu-ai-agent/community` | Read | Discord / 微信群志愿者 |

### Step 7: Webhooks / Integrations

- Discord webhook(社区通知)
- 微信群机器人(可选,后期)
- OpenSSF Scorecard(自动监控开源健康度)

---

## 2. 视觉品牌系统

### Logo & 色板

- Logo 文件:`assets/lingshu_logo.svg`(纯图形版,256×256)
- 色板:
  - **jade** `#0D9488`(主色,稳)
  - **jade deep** `#0F766E`
  - **jade light** `#2DD4BF`
  - **gold** `#D97706`(强调,动)
  - **gold light** `#F59E0B`
  - **ink** `#1E293B`(正文)
  - **paper** `#FAFAF7`(背景)
- 字体:
  - 中文:思源宋体 / 苹方 / 思源黑体
  - 英文:Inter / IBM Plex Sans

### Banner 设计

- GitHub social preview(1280×640):
  - 左侧:`lingshu_logo.svg` 居中,占 1/3 宽
  - 右侧:大字 "LingShu" + 副标 "The Pivot of Agent Orchestration"
  - 背景:深 jade 渐变 → 黑
  - 点缀:8 个金色卫星点散布,呼应 logo

---

## 3. 文档站规划(`lingshu-docs`)

技术选型:**Docusaurus 3**(理由:React + MDX,生态最成熟,SEO 好,中文友好)

```
lingshu-docs/
├── docs/
│   ├── intro.md                      ← 30s 上手
│   ├── installation.md
│   ├── quick-start.md
│   ├── concepts/
│   │   ├── react-loop.md
│   │   ├── slots.md
│   │   ├── spi.md
│   │   └── sandbox.md
│   ├── guides/
│   │   ├── first-agent.md
│   │   ├── custom-tool.md
│   │   ├── custom-skill.md
│   │   ├── multi-agent.md
│   │   └── production.md
│   ├── adapters/
│   │   ├── google-adk.md
│   │   ├── alibaba-graph.md
│   │   └── langgraph4j.md
│   ├── reference/
│   │   ├── config.md
│   │   ├── api.md
│   │   └── events.md
│   └── ops/
│       ├── observability.md
│       ├── security.md
│       └── deployment.md
├── blog/                             ← Release notes + 案例
├── i18n/zh-CN/                       ← 中文翻译
└── docusaurus.config.ts
```

部署:`github.com/lingshu-ai-agent/lingshu-docs` → 自动 deploy 到 `docs.lingshu.ai`(后期挂 CNAME)

---

## 4. 官网规划(`lingshu-website` → lingshu-ai-agent.github.io/lingshu-website/)

技术选型:**Jekyll + Minima 主题**(理由:GitHub Pages 原生支持,零配置,模仿 oryx-labs 的 oryxos 站常见做法)

页面结构(参考 oryx-labs/oryxos 风格):

```
lingshu-website/
├── _config.yml
├── _layouts/
│   └── default.html
├── _includes/
│   ├── header.html
│   ├── footer.html
│   └── logo.html
├── assets/
│   ├── css/style.css
│   ├── img/lingshu_logo.svg
│   └── img/social-preview.png
├── index.html             ← 首页(Hero + Features + Quick Start)
├── docs.html              ← 跳转 docs.lingshu.ai
├── community.html         ← Discord / 贡献者指南
├── blog.html              ← Jekyll 博客
└── pages/
    ├── adapters.md
    ├── production.md
    └── roadmap.md
```

落地页关键 section(从 oryx-labs/oryxos 借鉴):
1. **Hero**:Logo + 大字 "LingShu" + 副标 + 两个 CTA(Quick Start / GitHub)
2. **Why LingShu**:3-4 列对比卡片(对照 LangChain / Spring AI / 自研)
3. **Quick Start**:可复制的 5 行代码,30s 跑通
4. **Architecture**:嵌入设计文档的 Mermaid 图(简化版)
5. **Ecosystem**:6 个核心 repo 卡片
6. **Community**:Discord / 贡献者名单
7. **Footer**:License / Sponsor / 友链

---

## 5. 第一个 PR 流(社区冷启动 SOP)

| Day | 动作 |
|---|---|
| D1 | 建组织 + 6 个空仓库 + logo + profile |
| D2 | 主仓库 `lingshu` 推到 `0.1.0-alpha`,能跑 ReAct Loop 最小闭环 |
| D3 | `lingshu-website` 首页上线 |
| D4 | `lingshu-docs` 上线 intro + quick-start + concepts 3 篇 |
| D5 | 在掘金 / 知乎 / Hacker News 发一篇 "为什么做 LingShu" |
| D6 | Discord 频道开张(community / dev / showcase / random 四室) |
| D7 | 录一条 5min 演示视频,推到 B 站 / YouTube |

---

## 6. 长期路线图(3 阶段)

| 阶段 | 时间 | 目标 |
|---|---|---|
| **v1.0** | D+30 | 1 个能跑的核心引擎 + CLI + 文档站 + 官网 + 100 GitHub stars |
| **v1.5** | D+90 | 接入 Anthropic / OpenAI 两个 LLM Provider + MCP 客户端 + Skill 市场雏形 |
| **v2.0** | D+180 | 自研 DAG FlowEngine + 适配 Google ADK + Alibaba Graph + 2000 stars + 50 外部贡献者 |

---

## 7. 文件清单(本次交付)

```
community/
├── BLUEPRINT.md                          ← 本文件
├── README.md                             ← 组织 profile README(放到 lingshu-ai-agent/.github/profile/)
├── governance/
│   ├── CODE_OF_CONDUCT.md
│   ├── CONTRIBUTING.md
│   ├── SECURITY.md
│   └── ROADMAP.md
├── repos/
│   ├── lingshu/README.md                 ← 主引擎 README
│   ├── lingshu-cli/README.md             ← CLI README
│   ├── lingshu-docs/README.md            ← 文档站 README
│   ├── lingshu-website/README.md         ← 官网 README
│   ├── lingshu-skill-market/README.md    ← Skill 市场 README
│   └── lingshu-examples/README.md        ← 示例库 README
├── website/
│   ├── index.html                        ← 官网首页(可独立运行)
│   └── style.css                         ← 官网样式
└── assets/
    └── (logo / banner 软链到 /Users/lineng/Documents/AIFullStack/MyDSHAgentDesign/lingshu_logo.svg)
```

---

## 8. 给 chickenmood 的具体行动清单

按优先级:

1. **D+0(今天)**:
   - [ ] 创建 `lingshu-ai-agent` 组织
   - [ ] 把 `lingshu_logo.svg` 上传到 organization avatar
   - [ ] 填 display name / bio / location
   - [ ] 创建 `.github` 仓库,把本目录的 `README.md` + `governance/*` 推进去
2. **D+1**:
   - [ ] 创建 `lingshu` 仓库,把 `repos/lingshu/README.md` 推进去
   - [ ] 创建 `lingshu-cli` / `lingshu-docs` / `lingshu-website` 3 个仓库,各自 README 占位
   - [ ] 把 `website/index.html` + `style.css` 推到 `lingshu-website`,开启 Pages
3. **D+3**:
   - [ ] 写首版引擎代码(`@LingshuEngineApplication` SpringBoot 启动器)
   - [ ] 录 5min 演示视频
4. **D+7**:
   - [ ] 发掘金 / 知乎 / HN / V2EX
   - [ ] 开 Discord

---

## 9. oryxos 竞争对标(2026-09 抓的活情报)

抓自 [WebSearch](https://github.com/oryx-labs/oryxos) + 第三方 [reporank.net 资料](https://reporank.net/en/repo/oryx-labs-oryxos.html)。

### 9.1 oryxos 是什么

| 维度 | 值 |
|---|---|
| 全名 | oryxos · Distributed AI Agent OS |
| 仓库 | github.com/oryx-labs/oryxos |
| 语言 | Java 21 + virtual threads |
| License | Apache 2.0 |
| Star | ~140(2026-09 抓取时) |
| 创建 | 2026-06 |
| 形态 | 单 executable JAR,K8s/VM/裸金属可跑 |
| 定义 | YAML 声明式(零代码) |
| 标准 | MCP / A2A / SKILL.md 三件套 |
| 安全 | 文件/命令/域名白名单 + 全审计 |
| org 其他仓 | Flare · pi-fabric · pi-desktop(TS) |

### 9.2 我们和 oryxos 的关键差异

| 维度 | oryxos | LingShu | 谁赢 |
|---|---|---|---|
| **JDK 基线** | Java 21 | **JDK 8**(主)+ 11/17 | 🟢 **LingShu** — 还在 JDK 8 LTS 的企业才是沉默的大多数 |
| **定位** | Distributed **OS**(独立进程,跨节点) | In-process **Engine**(嵌进 Spring) | 互补,**不冲突** |
| **部署** | 单 JAR + K8s 集群 | Spring Boot 启动器 + CLI | 🟢 LingShu 更适合已有 Spring 团队 |
| **标准** | MCP / A2A / SKILL.md | MCP / SKILL.md(**A2A 待补**) | 平 |
| **可调性** | 整 JAR 启停 | 8 SPI 槽位任意替换 | 🟢 LingShu |
| **作者** | 个人/小团队匿名 | 你(chickenmood)实名 | 🟢 LingShu 利于信任 |

### 9.3 营销一句话(差异化锚)

> **"LingShu is to oryxos what Spring Boot is to Kubernetes — same goal, different scale, embeddable."**

### 9.4 我们不该抄的(避免被反向同质化)

- ❌ **不叫 OS** —— 我们是 Engine。"Agent OS" 的心智已经被 oryxos 占,抢不动,抢了反被比较
- ❌ **不画"分布式跨节点"大饼** —— MVP 阶段做单 JVM 内多 Agent 就够
- ❌ **不追 virtual threads** —— JDK 8 不支持;真要做高并发,Loom 项目兼容层是 v2.x 之后的事
- ❌ **不复制他们的 README 排版** —— Apache ORY (羚羊) 与灵枢 (中医枢) 的视觉语汇不同,jade/gold 比 oryxos 的"沙漠 + 蓝"更适合中式读者

### 9.5 我们应该抄的

- ✅ **三件套标准** MCP / A2A / SKILL.md —— 一个不能少;**A2A 已在 v0.5 路线落地**(Slot 9 `A2aTransport` + `RemoteAgentTool` 适配器 + `lingshu serve --a2a` 服务端,详见设计文档 §5.6)
- ✅ **单 executable JAR 形态** —— `lingshu-cli run --jar ...` 让 CLI 也能 bundle 整个引擎,部署极简
- ✅ **审计追踪 + 全工具白名单** —— 在 SECURITY.md 已经写了,加强 v1.0 阶段强制默认开启
- ✅ **YAML 优先** —— LingShu 的 `AgentConfig` 已经支持 yml,继续投入
- ✅ **org 多仓形态** —— oryx-labs 一个 org 下挂 oryxos / Flare / pi-fabric / pi-desktop,我们挂 lingshu / lingshu-cli / lingshu-studio / lingshu-cloud / lingshu-skill-market —— 模仿这条

### 9.6 抢 niche 文案(直接进 README / 官网)

- *"JDK 8 first. Not Java 21 first."*
- *"If your service is on JDK 8, LingShu is the only Agent Engine that runs in your process — no upgrade, no separate cluster."*
- *"Engine, not OS. Spring Boot, not Kubernetes."*
- *"8 SPI slots. Swap anything. Including the orchestrator itself."*

---

## 10. 二次微调(以上已完成,无需再贴图)

本节是原来的"待你贴图"提示位,已被 §9 取代。如需进一步打磨视觉,把 oryxos 官网截图或 lingshu-ai-agent 真实域名贴给我,我再做一轮 hero / banner 微调。

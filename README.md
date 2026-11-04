# Super Ming Agent

English | [中文](README.zh.md)

**One agent, one imperial court.** Super Ming Agent (大明智能体) is a personal fork of [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness), using Ming government offices as a guide to agent responsibilities. It keeps the upstream Cordis-based, everything-is-a-plugin architecture.

The naming is inspired by [Super-agent 大明官制图](https://claude.ai/artifact/YG6q1qa8643zrNRxXMuMVx). The aim is to let people focus on decisions and acceptance while agents organize context, execute tasks, and report useful results.

## Names and responsibilities

These names explain the design; they do not introduce new runtime APIs or guarantee that every mechanism in the reference is implemented. This repository contains the harness. The separate [upstream Super-agent prototype](https://github.com/deepseek-ai/dsh-superagent-prototype) supplies repository-oriented orchestration and requires its own setup.

| Agent concept | Ming name | Responsibility in the analogy |
|---|---|---|
| User | 皇帝 · Emperor | Set goals, make decisions, accept results. |
| Router | 内阁 · Grand Secretariat | Understand requests, coordinate tasks, present results. |
| Router batch | 集中票拟 · Batched drafting | Consider accumulated requests together. |
| Worker | 六部 · Six Ministries | Execute individual tasks with isolated context and tools. |
| Subagent | 清吏司 · Ministry divisions | Divide work within an individual task. |
| Trigger | 奏疏、塘报、民词 · Incoming petitions | Bring messages and environmental events into the system. |
| Thread | 案卷 · Case file | Keep related events and references together. |
| Rule-based filtering | 通政使司 · Transmission Office | Check source and admission rules before semantic routing. |
| Semantic filtering | 内阁阅本 · Secretariat review | Decide whether and how a request needs action. |
| Subscription bypass | 部院照例办理 · Routine handling | Send follow-up events to the worker already handling a case. |
| Shared thread subscriptions | 三法司会审 · Joint review | Let several workers inspect the same case. |
| Inline and spill | 贴黄 · Summary slips | Keep summaries close and retrieve full content when needed. |
| Chained recall | 公文叙由 · Document references | Follow references back to earlier context. |
| Speculative execution | 票拟草稿 · Draft proposals | Prepare useful work before presenting a decision. |
| Asynchronous tools | 该部议奏 · Ministry deliberation | Dispatch work and receive results without blocking other work. |
| Channel-specific replies | 题本、奏本、揭帖 · Reports | Adapt the form and detail of a response to its destination. |
| Durable state | 黄册库 · Archive | Preserve records independently of execution processes. |
| Local execution | 驿传、地方衙门 · Relay and local offices | Work in the environment where files and tools live. |
| Watchdog | 科道、考成法 · Inspection and assessment | Independently inspect progress and stalled work. |
| Cross-agent boundaries | 南京六部 · Parallel ministries | Coordinate across separate context domains. |
| Credentials | 勘合、印信 · Tallies and seals | Verify authority and control credential use. |

The historical comparisons are simplified explanations. Terms such as Router, Worker, and Watchdog describe the linked design; the table is not an implementation checklist.

<a id="run"></a>

<a id="run-from-source"></a>

## Run from source

Requires Node.js >= 24.9.0 and pnpm 11.28.5, as declared in [package.json](package.json).

```sh
git clone https://github.com/LucianVane/Super_Ming_Agent.git
cd Super_Ming_Agent
corepack enable
pnpm install
DSH_CLIENT_TITLE="Super Ming Agent" pnpm run build
pnpm dsh web
```

The build-time `DSH_CLIENT_TITLE` sets the browser title. In PowerShell, set `$env:DSH_CLIENT_TITLE = "Super Ming Agent"` before `pnpm run build` instead. The Web UI starts at `http://127.0.0.1:3080`; pass `--no-open` to leave the browser closed. See the [Web UI guide](docs/user/guide/index.md) for model and credential configuration.

The CLI remains `dsh`, workspace packages retain their `@deepseek-ai/*` names, and existing configuration paths remain compatible. `npx @deepseek-ai/dsh web` installs the upstream distribution; use this checkout to run Super Ming Agent.

## Development

Read the [development guide](docs/development.md), [architecture](docs/architecture.md), and [contribution guide](CONTRIBUTING.md). Agents should follow [AGENTS.md](AGENTS.md).

```sh
pnpm run dev:web
pnpm run test
pnpm run typecheck
```

Report fork-specific issues in [this repository](https://github.com/LucianVane/Super_Ming_Agent/issues). The inherited code is in developer preview and may introduce compatibility-breaking changes. Review the [safety notice](SAFETY.md) before running it.

## Attribution and license

Super Ming Agent is maintained as a personal fork by LucianVane. DeepSeek Harness was developed by DeepSeek AI and is powered by [Cordis](https://github.com/cordiverse/cordis). The project is independently named and is not an official DeepSeek distribution.

The naming explanation is adapted from the linked Claude artifact; its discussion refers to DeepSeek's [Exploring Super-agent Design](https://zhuanlan.zhihu.com/p/2099987320443237060). This README summarizes the design analogy without reproducing the article or its experimental claims.

The upstream MIT license and third-party notices are preserved. See [LICENSE](LICENSE) and [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

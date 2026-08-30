---
document_role: navigation_only
status: active
version: "0.2.3"
---

# Personal AI Governance

本仓库是个人 AI 系统的根治理真源。

它只治理**值得长期复用、需要版本控制、不能依赖聊天记忆保存的核心资产**，不要求所有 Chat、Project、笔记和临时想法进入治理体系。

> 本文件只负责导航，不承载独立规范。正式规则以各 Canonical Asset 为准。

## Canonical Assets

| Asset ID | 文件 | 职责 |
|---|---|---|
| `GOV-ROOT` | `governance/00_root-rules.md` | 零级规则与最高治理边界 |
| `GOV-CONCEPTS` | `governance/10_core-concepts.md` | 唯一术语与概念定义 |
| `GOV-ASSET-ARCH` | `governance/20_asset-architecture.md` | 核心资产准入、单一语义真源、树状主干、交叉层与用户可读展示板 |
| `GOV-CHANGE` | `governance/30_change-control.md` | Principle、Rule、Routing 和 Repo 变更治理 |
| `GOV-PROJECT` | `governance/40_project-governance-and-retrieval.md` | Project 入驻、Binding、检索模式与周期复核 |
| `GOV-SOURCE` | `governance/50_source-authority.md` | GitHub、Operational Source、文件库与人的权威边界 |
| `GOV-BOOTSTRAP` | `BOOTSTRAP.md` | 受治理 Runtime 的开机协议 |
| `GOV-BATON` | `cross-cutting/coordination/baton-control-board.md` | 跨 Runtime 接力语义、Authority、Schema、Fail Closed 与用户控制板规则 |
| `REG-SYSTEMS` | `registry/systems.yaml` | 当前系统、Runtime 与 Repo 路由的唯一登记表 |
| `ARCH-CANDIDATES` | `architecture/candidates.md` | 尚未冻结、需要真实运行验证的架构候选 |
| `ADR-0001` | `decisions/ADR-0001-governance-v0.2.md` | V0.2 架构决策及保留事项 |
| `ADR-0002` | `decisions/ADR-0002-user-readable-control-boards.md` | 面向用户的治理展示板必须提供中文视图 |
| `ADR-0003` | `decisions/ADR-0003-cross-runtime-baton-control.md` | 正式化跨 Runtime 接力控制 V0 |
| `EVAL-GOV-BATON-V0` | `evals/gov-baton-v0.md` | 接力协议冲突、过期、身份、回传与来源隔离验收样例 |

## V0.2 的核心选择

- 只治理核心资产，绝大多数临时 Chat 和轻量 Project 不进入本体系。
- 同一概念、定义或规范性规则只能有一个 Canonical Owner。
- 其他文件只能引用、应用或生成派生视图，不得手工维护第二份同义规则。
- 资产主结构采用“树状主干 + 横向交叉层”，逻辑上视为可追溯的有向无环依赖图。
- 修改任何实质性规则前，必须全面检索相关 MD、依赖、下游 Workflow、Skill、Agent、Program 和 Projection。
- 日常开放思考不强制先读全部规则；根据后果和 Runtime 模式按需检索。
- 面向用户的状态板、控制板、迁移板和审批板必须提供中文展示视图；机器可读状态可以并存，但两者必须同源。
- 跨 Runtime 接力的 V0 协议由 `GOV-BATON` 统一维护；V0 状态证据来自用户显式 Handoff、当前 Runtime 在自身 Authority 内的直接声明或未来正式登记的 Operational Source，LIFE Workspace 只作为用户汇总与展示入口，Root Governance Repo 不保存实时接力状态。
- 当前分类、路由和 Repo 关系是 V0.2，可通过 Git 历史持续修改。

## 当前近期顺序

1. 建立 `personal-ai-governance`
2. 建立并迁移 `project-review-system`
3. 继续完成 `rpg-external-brain` 当前安全闭环
4. 继续运行 `ai-engine-kb`
5. 个人成长、TickTick、市场风险等系统先登记，按真实价值逐步治理

---
asset_id: ARCH-CANDIDATES
asset_type: architecture_candidate_registry
authority: personal-ai-governance
scope: root
status: active
version: "0.2.2"
depends_on:
  - GOV-CONCEPTS
  - GOV-PROJECT
  - GOV-SOURCE
  - GOV-ASSET-ARCH
  - GOV-BATON
---

# Architecture Candidates — 待验证方向

本文件只保存尚未冻结、但不能丢失的重要方向。

Candidate 不应被 Runtime 当作正式默认规则。其复核触发条件见 `GOV-CHANGE` 与 `GOV-PROJECT`。

## `CAND-001` — Multi-source Intake

**状态：** direction_confirmed / implementation_deferred  
**优先验证：** external-brain

候选方向：

- API / Webhook / CMD；
- 文件与数据库；
- 截图 / OCR；
- 结构化 Web；
- 自然语言 / 语音；
- Agent / Connector。

核心命题：

> API-first，但不是 API-only；统一治理协议，不强求统一原始输入格式。

## `CAND-002` — Field-Level Authority

**状态：** direction_confirmed / implementation_deferred  
**优先验证：** external-brain、project-review

候选方向：

- 机器状态由机器来源优先定义；
- 人的意图、判断和决定由用户定义；
- OCR 与外部 AI 默认形成 Candidate；
- 冲突进入 Reconciliation，不静默覆盖。

## `CAND-003` — Agent-first, Web-visible, API-native

**状态：** candidate  
**优先验证：** external-brain、personal-growth、market-risk

候选定位：

- Agent：主要自然交互与编排；
- Web：查看、确认、纠错、控制和展示；
- API / MCP：机器接口；
- Program / DB：后台领域能力。

## `CAND-004` — Personal Gateway

**状态：** candidate / deferred  
**优先验证：** personal-growth

候选职责：

- 认证；
- 权限；
- Connector 注册；
- API / MCP 路由；
- 文件与事件转发；
- 设备调用；
- Agent 调度；
- 审计。

Gateway 不作为 Canonical Source。

## `CAND-005` — Obsidian / Notion 工作区

**状态：** direction_confirmed / implementation_open

候选分工：

- Obsidian：直接浏览和编辑 Git Markdown，提供双链与人类可视化；
- Notion：结构化 Inbox、研究工作区与协作视图；
- GitHub：正式认知资产；
- ChatGPT Context：Projection；
- TickTick：任务与时间状态。

只有真正产生价值时才引入工具，避免为了工具完整性增加维护负担。

## `CAND-006` — Global Context Router

**状态：** deferred

未来可能按：

- `system_id`
- Authority
- Scope
- relevance
- freshness
- current task

自动选择多个 Repo 与 Operational Source。

V0.2 使用 Binding + Registry + 条件检索，不提前建设自动 Router。

## `CAND-007` — Event Envelope

**状态：** candidate / deferred  
**优先验证：** external-brain、future-gateway

未来多源输入可能需要统一 Event Envelope，记录：

- source；
- observed_at；
- received_at；
- idempotency_key；
- payload_kind；
- raw_reference；
- schema_version。

是否采用 CloudEvents 或自定义契约，等待真实 Adapter 需求。

## `CAND-008` — Cross-Chat Baton Control Board｜跨 Chat 接力控制板

**状态：** v0_promoted / v1_v2_deferred
**优先验证：** personal-ai-governance、project-review、external-brain、personal-growth

V0 协议已晋升为 `GOV-BATON`，决策记录见 `ADR-0003`。V0 的概念、Authority、Schema、状态枚举、Fail Closed、来源隔离和用户展示规则不再在 Candidate 中平行维护。

本候选只保留尚未获准实施的后续层级：

### V1 — 共享状态源，按次读取

- 建立一个明确的 Operational Source 保存接力状态；
- 总控和执行 Runtime 每次进入相关任务时读取最新状态；
- 任一 Runtime 完成交接后按授权更新共享状态；
- 现有 Chat 消息仍不会原地自动刷新，但下一次回复可展示最新状态；
- 共享状态不得仅依赖 Chat Memory。

在决定实施前，必须验证共享来源的 Authority、身份模型、并发控制、新鲜度、审计与安全写回边界。

### V2 — 事件驱动与主动刷新

- 通过 Gateway、Event Bus、Webhook、Connector 或平台原生事件能力订阅运行状态；
- 执行派发、完成、失败和回传形成事件；
- 控制面自动更新共享状态并通知相关 Runtime；
- 需要认证、幂等、权限、冲突合并和审计；
- 当前 ChatGPT Project / Chat 本身不应被假定已具备该能力。

### 后续验证问题

1. 是否存在可授权的共享 Operational Source；
2. ChatGPT、Codex、本地 Agent 和未来 WorkBuddy 分别能否安全读写该状态；
3. 多执行位并行时如何实现幂等、并发控制、失败重试与冲突合并；
4. 是否有足够真实需求支持事件触发、主动通知和 Gateway；
5. V1 / V2 如何继续满足 `GOV-BATON`，且不让 Projection 或 GitHub 成为实时状态真源。

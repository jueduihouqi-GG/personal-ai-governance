---
asset_id: ARCH-CANDIDATES
asset_type: architecture_candidate_registry
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-CONCEPTS
  - GOV-PROJECT
  - GOV-SOURCE
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

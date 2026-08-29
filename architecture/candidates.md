---
asset_id: ARCH-CANDIDATES
asset_type: architecture_candidate_registry
authority: personal-ai-governance
scope: root
status: active
version: "0.2.1"
depends_on:
  - GOV-CONCEPTS
  - GOV-PROJECT
  - GOV-SOURCE
  - GOV-ASSET-ARCH
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

**状态：** direction_confirmed / implementation_requires_shared_state  
**优先验证：** personal-ai-governance、project-review、external-brain、personal-growth

### 目标

在“总控 Chat + 一个或多个执行 Chat / Agent / Codex”协作中，除名称映射外，提供一个用户可读的接力控制板，使用户能够判断：

- 当前轮到谁工作；
- 用户现在应进入哪个 Chat 或 Runtime；
- 最近一次有效交接是谁交给谁；
- 执行完成后应回传到哪里；
- 双方都停止一段时间后，当前任务是否仍待验收、待转发或已经闭环。

### 核心判断

- Chat 列表顺序、转圈状态和最后一条自然语言消息只能作为辅助信号；
- **当前接力棒**应成为“下一步轮到谁”的主要状态；
- 时间戳用于审计和解决双方都处于停止状态后的先后关系，但不单独决定接力归属；
- 每个执行位应分别记录任务、派发状态、最近回传、回传入口和是否等待总控验收；
- 用户可读视图执行 `GOV-ASSET-ARCH` 的中文展示板规则。

### 候选状态字段

```yaml
system_id:
control_runtime:
task_id:
task_title:
current_baton:
current_status:
user_next_action:
active_execution_slots:
last_handoff:
last_handoff_at:
return_route:
blocked_by:
writeback_boundary:
updated_at:
state_authority:
```

### 候选接力状态

```text
待总控分析
待总控生成指令
待用户转发
已派发，待执行
执行中
执行已完成，待用户回传
结果已回传，待总控验收
待用户裁决
本轮闭环，无人待办
受阻
```

### 实现层级

#### V0 — 手工接力板

- 每个 Chat 在本地回复中展示当前接力棒；
- 用户在执行 Chat 与总控 Chat 之间手工转发结果；
- 已发送的历史消息不会自动变化；
- 状态只在收到新消息并重新生成回复时更新。

#### V1 — 共享状态源，按次读取

- 建立一个明确的 Operational Source 保存接力状态；
- 总控和执行 Runtime 每次进入相关任务时读取最新状态；
- 任一 Runtime 完成交接后按授权更新共享状态；
- 现有 Chat 消息仍不会原地自动刷新，但下一次回复可展示最新状态；
- 共享状态不得仅依赖 Chat Memory。

#### V2 — 事件驱动与主动刷新

- 通过 Gateway、Event Bus、Webhook、Connector 或平台原生事件能力订阅运行状态；
- 执行派发、完成、失败和回传形成事件；
- 控制面自动更新共享状态并通知相关 Runtime；
- 需要认证、幂等、权限、冲突合并和审计；
- 当前 ChatGPT Project / Chat 本身不应被假定已具备该能力。

### 权威边界

- 接力状态属于 Operational State，不是长期业务 Rule；
- GitHub 可保存 Schema、状态机、显示规则和 Adapter，不应作为高频实时状态数据库；
- 用户本人拥有任务是否已转发、是否接受结果和是否结束本轮的最终 Authority；
- Runtime 不得仅凭“另一个 Chat 可能已经完成”猜测性改变接力棒；
- 无共享状态源或明确用户回传时，必须标记状态不确定，而不能声称已经自动同步。

### 验证问题

1. 当前平台是否允许一个 Chat 读取另一个 Chat 的最新状态；
2. 是否存在可授权的共享 Operational Source；
3. ChatGPT、Codex、本地 Agent 和未来 WorkBuddy 分别能否读写该状态；
4. 是否可以基于事件自动触发更新，而非依赖用户复制粘贴；
5. 多个执行位并行时，如何处理并发、失败、重试和交接冲突；
6. 如何让用户展示板与机器状态同源；
7. 如何避免把 GitHub 误用为高频实时状态存储。

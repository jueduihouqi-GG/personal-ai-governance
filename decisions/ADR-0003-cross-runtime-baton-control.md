---
asset_id: ADR-0003
asset_type: architecture_decision
authority: personal-ai-governance
scope: root
status: accepted
version: "1.1"
depends_on:
  - GOV-BATON
  - GOV-SOURCE
  - ADR-0002
---

# ADR-0003 — 正式化跨 Runtime 接力控制 V0

## Context

`CAND-008` 已识别“总控 Runtime + 一个或多个执行 Runtime”协作中的接力问题：Chat 列表顺序、转圈状态、时间戳或最后一条自然语言消息不足以回答当前轮到谁、结果返回哪里以及任务是否闭环。

`ADR-0002` 只决定治理展示板必须提供中文用户视图，并由 `GOV-ASSET-ARCH` 维护通用展示规则。它没有决定接力语义、Authority、最小状态、来源隔离、多执行位或失败安全，因此不足以承载本次决策。

同时，接力的当前状态是高频 Operational State。若把它写入 Root Governance Repo 或 `REG-SYSTEMS`，会混淆 Canonical Source 与 Operational Source，并把稳定 Registry 变成临时任务表。

## Decision

1. 将 `CAND-008` 的 V0 协议晋升为独立 Cross-cutting Asset `GOV-BATON`。
2. `GOV-BATON` 作为 V0 接力语义、Authority、Schema、用户视图要求、Fail Closed、来源隔离与多执行位规则的唯一 Canonical Owner。
3. 相关术语只在 `GOV-CONCEPTS` 定义；其他资产通过 Concept ID 或 `GOV-BATON` 引用。
4. GitHub 只保存协议、Schema、ADR 与 Eval。V0 状态证据只来自用户显式 Handoff、当前 Runtime 在自身 Authority 内的直接声明，或未来明确登记的 Operational Source。
5. 接力控制板是当前状态的非 Canonical Projection，只展示、不产生状态。
6. `REG-SYSTEMS` 不记录临时工作流、任务、接力棒或当前执行状态。
7. V0 采用人工转发和精简状态枚举，不建立复杂状态机。
8. V1 共享状态库和 V2 Gateway / Event Bus 保留在 `CAND-008`，继续延后。
9. LIFE Workspace 作为 V0 用户操作的状态汇总与展示入口，不是其他 Runtime 可直接读取的共享 Operational Source。
10. 局部执行位冲突只转移对应执行接力棒；只有全局协调状态不明时才转移协调接力棒并暂停全局协调。
11. 关闭执行位必须记录 `closure_reason`，并区分 `accepted`、`cancelled` 与 `superseded`；用户最终治理权不创造缺少证据的技术完成事实。
12. `EVAL-GOV-BATON-V0` 覆盖交接证据与时区、局部和全局冲突、关闭原因、LIFE 边界及原有失败安全场景。

## Consequences

### Positive

- 跨 Runtime 协作拥有稳定、唯一且可审计的接力协议；
- 当前状态与长期治理资产的 Authority 边界清楚；
- 多执行位可以分别展示责任与回传链路；
- 证据不足或冲突时由用户裁决，不再猜测接力归属；
- ADR-0002 继续保持通用用户展示职责，不产生重复决策。

### Cost

- V0 仍需用户在 Chat 之间手工转发；
- 历史消息不会自动刷新；
- Runtime Adapter 需要在相关任务中按需加载 `GOV-BATON`；
- V0 仍需要用户从 LIFE Workspace 或其他界面显式转交状态证据，其他 Runtime 不会自动读取或同步该入口；
- 未来 Operational Source 需要自行满足状态持久化、新鲜度与审计要求。

## Rejected Alternatives

### 修订 ADR-0002 以包含接力协议

拒绝。ADR-0002 的职责是通用中文用户展示；加入接力 Authority 和状态协议会混合两类独立决策。

### 继续把 V0 留在 CAND-008

拒绝。用户已批准 V0 协议，继续以 Candidate 维护会使 Runtime 无法把它作为正式默认规则。

### 使用 GitHub 或 REG-SYSTEMS 保存当前接力状态

拒绝。两者是稳定治理资产的 Canonical Source / Registry，不是高频 Operational Source。

### 立即建设共享状态库、Gateway 或 Event Bus

拒绝。当前没有足够的真实 Adapter、权限、冲突合并与事件需求证据；V1/V2 继续延后。

## Propagation Boundary

- `GOV-PROJECT` 在总控与执行 Runtime 协作时触发按需检索 `GOV-BATON`。
- `GOV-BOOTSTRAP` 在输出接力控制板时执行该路由。
- `GOV-ASSET-ARCH` 只维护通用中文用户展示规则，不反向引用或规范 `GOV-BATON`；`GOV-BATON` 单向依赖该通用规则。
- `ARCH-CANDIDATES` 不再保存 V0 规范正文，只保存 V1/V2 后续候选。

## Rollback

回滚本 Change Set 可恢复 `CAND-008` 的 V0 候选正文并移除 `GOV-BATON`、`ADR-0003`、`EVAL-GOV-BATON-V0` 及相关引用。任何已写入外部 Operational Source 的当前状态不属于本仓库回滚范围，必须由其 Authority 单独处理。

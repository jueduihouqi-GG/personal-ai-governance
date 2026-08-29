---
asset_id: ADR-0002
asset_type: architecture_decision
authority: personal-ai-governance
scope: root
status: accepted
version: "1.0"
depends_on:
  - GOV-ASSET-ARCH
  - GOV-BOOTSTRAP
  - GOV-PROJECT
---

# ADR-0002 — 面向用户的治理展示板必须提供中文视图

## Context

受治理 Runtime 会使用 YAML、英文键名、英文枚举和代码式状态保存机器可读信息。

这些格式适合程序、Agent 和跨 Runtime 交换，但若直接作为面向用户的状态板、架构板、迁移板或审批板，用户可能无法准确理解当前状态、风险、写回边界和下一步，从而削弱人工最终治理权。

## Decision

1. 正式规则由 `GOV-ASSET-ARCH` 第7.3节“用户可读展示板”唯一维护，本 ADR 不复制完整规范正文。
2. 凡需用户阅读、审核、批准或控制的治理视图，必须提供完整中文展示板。
3. 机器可读视图可以保留，但必须与中文展示板紧邻，并从同一底层状态生成。
4. 中文展示板是用户界面和 Projection，不成为第二 Canonical Source。
5. `GOV-BOOTSTRAP` 负责让受治理 Runtime 在输出相关视图时加载并执行该规则。
6. 本要求适用于状态板、控制板、架构快照、迁移状态、审批状态、Change Set、Backlog、执行结果以及风险和阻断视图。

## Consequences

### Positive

- 用户可以直接理解并审查治理状态；
- 英文机器字段不再成为人工批准的阅读障碍；
- Human Authority 与机器状态可以在同一界面中协同；
- 不要求放弃 Stable ID、英文枚举和机器可读格式。

### Cost

- Runtime Adapter 和 Projection 生成器需要增加中文解释层；
- 现有仅含机器字段的展示板需要在后续使用时补充中文视图；
- 必须确保中文视图和机器视图同源，避免形成两份独立维护的状态。

## Propagation Boundary

- 新启动或重新读取 `GOV-BOOTSTRAP` 的受治理 Runtime 应执行该要求。
- 已经打开但尚未重新检索治理真源的 Chat 不会被 GitHub 主动推送消息；其在下一次治理启动、正式任务检索或用户要求刷新治理规则时生效。

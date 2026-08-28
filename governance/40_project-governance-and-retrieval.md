---
asset_id: GOV-PROJECT
asset_type: project_and_retrieval_governance
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-ROOT
  - GOV-CONCEPTS
  - GOV-ASSET-ARCH
  - GOV-CHANGE
  - REG-SYSTEMS
---

# Project Governance & Retrieval — Project 入驻、Binding 与检索

## 1. 治理等级

### G0 — Scratch

临时 Chat 或一次性任务。

- 不需要 Repo；
- 不需要 Binding；
- 用完可丢弃。

### G1 — Persistent Project

存在持续价值，但尚未形成必须长期治理的 Core Asset。

- 可依赖 Project Context；
- 不强制建 Repo；
- 定期判断是否需要升级。

### G2 — Governed System

已经形成不能依赖 Chat Memory 保存的 Core Asset。

- 分配 `system_id`；
- 登记 `REG-SYSTEMS`；
- 明确 Canonical Repo；
- 使用 Binding；
- 通过 Git 维护。

### G3 — Productized Runtime

已形成 Workflow、Skill、Agent 或 Program。

- 继续使用 G2 的 Canonical Governance；
- 增加更严格的执行、测试与写回边界；
- 仍可持续迭代，不表示“已经完成”。

## 2. 新 Project 入驻

只有当 Project 产生 Core Asset 时，才进入治理。

入驻步骤：

1. 判断加入已有 System 还是创建新 System；
2. 分配稳定 `system_id`；
3. 分配一个或多个 `runtime_id`；
4. 在 `REG-SYSTEMS` 登记；
5. 指定 Primary Canonical Repo；
6. 指定 Shared Systems 和 Operational Sources；
7. 为 Runtime 设置 Retrieval Mode 与 Writeback Policy；
8. 在 Project Instructions 写入最薄 Binding；
9. 首次迁移只提取稳定 Core Asset，不搬运全部 Chat 原文。

## 3. Binding 最小化

Project Instructions 只保存：

```yaml
governance_bootstrap:
  repo: jueduihouqi-GG/personal-ai-governance
  path: BOOTSTRAP.md

system_id: example-system
runtime_id: example-runtime
```

不得在多个 Project Instructions 中复制 Primary Repo、Shared Repo、Rule 和完整 Retrieval Policy。

这些内容统一由 `REG-SYSTEMS` 维护。

## 4. Retrieval Mode

### `open`

适合临时研究与自由创意。

- 默认不自动读取 Canonical Repo；
- 用户明确要求或问题直接引用历史资产时再读取。

### `selective`

适合总设计师、长期探索 Project 和轻量 Domain Chat。

- 普通开放讨论可先独立思考；
- 触及历史规则、跨系统架构、正式执行或正式变更时自动读取。

### `grounded`

适合成熟的生产型 Chat。

- 大多数实质工作先读取 Primary Canonical Repo；
- 开放讨论可使用 `diverge_then_ground`。

### `strict`

适合 Agent、Program、自动写入和高风险执行。

- 执行或写入前必须读取相关 Rule / Workflow；
- 必须校验权限、状态和最新版本；
- 不满足条件时 Fail Closed。

## 5. 强制检索触发条件

出现以下任一情形，应按当前 Runtime Mode 自动读取相关 Canonical Asset：

1. 用户要求沿用已确认规则、决定或模板；
2. 正在执行标准 Workflow；
3. 任务属于正式生产或高风险判断；
4. 准备修改 Principle、Rule、Routing 或 Repo；
5. 准备写回 GitHub 或 Operational Source；
6. 涉及跨 System 架构；
7. Project Memory 与 Canonical Source 可能冲突；
8. 用户明确要求按正式真源回答。

## 6. 保留发散能力

开放架构讨论默认采用：

```text
Diverge
→ 先独立形成可能方案

Ground
→ 再读取相关 Canonical Asset 与 Candidate

Reconcile
→ 保持旧规则 / 形成 Candidate / 启动 Change Control
```

生产执行采用：

```text
Ground
→ Execute
```

正式变更采用：

```text
Ground
→ Impact Search
→ Propose
→ Approve
→ Commit
```

这不是全局语义分类器，而是按任务后果选择治理强度。

## 7. Context 负担控制

- 不每轮读取 GitHub；
- 不全量加载 Repo；
- 优先读取 3–7 个最相关 Asset；
- 需要时再展开依赖；
- Architecture Candidates 只在相关设计、Phase Gate 或周期复核时读取；
- Projection 只用于加速，不替代 Canonical Source。

## 8. 周期复核

每个 G2 / G3 System 应在 Registry 中设置：

- `review_triggers`
- `review_cadence`

复核重点：

- 是否仍值得治理；
- 是否应拆分或合并；
- 是否存在重复；
- Binding 是否准确；
- Retrieval Mode 是否过重或过轻；
- 是否有 Candidate 应进入正式治理。

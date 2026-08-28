---
asset_id: GOV-CONCEPTS
asset_type: canonical_dictionary
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on: []
---

# Core Concepts — 唯一术语与定义

## 1. 使用规则

本文件是以下术语的唯一正式定义来源。

其他 MD：

- 可以使用术语；
- 可以说明该术语在本地 Scope 的具体应用；
- 必须通过 Concept ID 或本文件链接引用；
- 不得重新给出另一套同义定义。

若需改变定义，按 `GOV-CHANGE` 处理，并检索所有 Concept ID 的引用。

## 2. 统一语言风格

### 规范词

- **必须**：硬约束，无授权例外不得偏离。
- **不得**：明确禁止。
- **应**：默认要求；偏离时应说明理由。
- **可**：允许但不强制。
- **候选**：尚未成为 Canonical Asset。

### 术语风格

- 正文以中文为主。
- 英文字段名、枚举、Stable ID 保持英文。
- 同一概念只使用本文件指定的正式中文名。
- 别名只用于帮助理解，不作为平行正式术语。
- 不为追求“语言丰富”创造同义规范词。

## 3. 概念字典

### `CON-001` — Core Asset｜核心资产

具有长期复用价值，丢失、漂移或冲突会造成实质损失，因此值得进入版本化治理的资产。

### `CON-002` — Formal Object｜正式对象

已进入治理范围，具有明确 `asset_id`、Scope、Authority Owner、状态和 Canonical Source 的长期对象。

### `CON-003` — Evidence｜证据

支持、挑战或解释 Knowledge、Principle、Rule 或决策的原始材料、事件、实验、来源、历史和执行结果。

### `CON-004` — Knowledge｜知识

经过整理、附有来源或验证状态的描述性认知，回答“我们目前知道什么”。

Knowledge 本身不自动形成强制行为。

### `CON-005` — Principle｜原则

能够跨多个具体情形复用的高层规范性判断，回答“默认应如何判断、取舍或设计”。

### `CON-006` — Rule｜规则

在明确 Scope 内具有更具体约束力的正式要求，回答“在本范围内必须、不得或应如何做”。

### `CON-007` — Workflow｜工作流

按明确顺序完成某类任务的可重复执行过程。

### `CON-008` — Skill｜技能

面向 AI Runtime 封装的可移植执行能力，通常包含触发条件、Workflow、Rule、Reference 和可选脚本。

### `CON-009` — Agent｜智能体

能够读取 Context、调用 Tool、执行 Workflow 并根据权限影响外部状态的 Runtime。

### `CON-010` — Program｜程序

以代码和确定性逻辑实现能力、状态管理或执行过程的软件系统。

### `CON-011` — Meta Governance｜母规则

治理 Principle、Rule、System、Routing、Authority 和正式写回如何产生、修改与审计的更高层规则。

正式中文名为“母规则”；“零级规则”是允许使用的别名。

### `CON-012` — System｜系统

围绕一个长期目的形成的治理单元，可包含多个 Project、Runtime、Repo、Operational Source 和 Capability。

### `CON-013` — Project｜项目空间

承载一组持续交互、资料与工作上下文的具体工作空间，例如 ChatGPT Project。

Project 不必与 System 一一对应。

### `CON-014` — Runtime｜运行时

实际读取规则、进行推理、调用工具或执行任务的环境，例如 ChatGPT、Codex、WorkBuddy、本地 Agent、Web 或 Program。

### `CON-015` — Canonical Source｜正式真源

某一类 Formal Object 当前唯一具有正式权威性的来源。

“唯一真源”“权威真源”均视为该概念的历史别名，正式用词统一为“正式真源”。

### `CON-016` — Operational Source｜运行状态源

保存实时任务、会议、游戏状态、应用状态或业务状态的权威系统。

Operational Source 不等同于 Canonical Source。

### `CON-017` — Authority Owner｜权威责任方

对某类 Formal Object 的正式含义、维护与变更承担最终管理责任的 System 或用户。

### `CON-018` — Scope｜适用范围

某个 Principle、Rule、Knowledge、Workflow 或 Skill 有效的边界，例如 root、domain、project、runtime 或 skill。

### `CON-019` — Routing｜路由

依据 `system_id`、Runtime、任务后果、Authority、Scope 与相关性，决定应读取或调用哪些正式来源和能力的过程。

### `CON-020` — Binding｜绑定

在 Runtime 与 System 之间建立的最小身份关系，使 Runtime 可以通过 Registry 找到自己的正式真源与检索规则。

### `CON-021` — Candidate｜候选

尚未正式晋升、尚未获得 Canonical Status 的想法、知识、规则、架构或变更提案。

### `CON-022` — Material Change｜实质性变更

满足以下任一条件的变更：

1. 相同输入可能产生不同结论或行动；
2. 默认判断、证据标准或优先级改变；
3. 权限、安全、隐私、合规或确认边界改变；
4. Scope 扩大、缩小或跨层级迁移；
5. Authority Owner、Repo、Binding 或 Routing 改变；
6. 下游 Workflow、Skill、Agent、Program、Schema、Test 或 Projection 需要同步处理；
7. 历史正式结论需要被视为错误、过时、Deprecated 或 Superseded。

### `CON-023` — Semantic Duplication｜语义重复

两个或更多手工维护位置分别表达同一正式定义、同一规范性规则或同一 Canonical Conclusion，并可能独立演化的状态。

术语出现、ID 引用、应用后果说明不属于语义重复。

### `CON-024` — Cross-cutting Asset｜交叉资产

无法合理归入单一纵向分支、同时被多个分支依赖的独立 Canonical Asset。

交叉资产具有自己的 Asset ID 和 Authority Owner，其他分支只引用它。

### `CON-025` — Projection｜投影

从 Canonical Source 派生、面向特定 Runtime 或 Project 的可重建视图、摘要、索引或 Context 包。

### `CON-026` — Derived Summary｜派生摘要

由 Canonical Asset 自动或明确受控生成的摘要。

若摘要包含规范性内容，必须标明来源、生成时间和非 Canonical 状态。

### `CON-027` — Dependency｜依赖

一个 Formal Object 的正式含义、行为或正确性需要另一个 Asset 成立的关系。

V0.2 使用 `depends_on` 单向记录依赖；反向影响通过搜索 Asset ID 推导，避免维护双份关系。

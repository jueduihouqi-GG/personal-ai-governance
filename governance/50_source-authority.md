---
asset_id: GOV-SOURCE
asset_type: source_authority_governance
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-ROOT
  - GOV-CONCEPTS
---

# Source Authority — 正式真源与运行状态源

## 1. 认知资产

以下 Core Asset 原则上由 GitHub 保存为 Canonical Source：

- Meta Governance；
- Principle；
- Rule；
- Knowledge；
- Workflow；
- Skill；
- ADR；
- Schema；
- Program Source Code；
- Test / Eval Specification。

GitHub 是这些资产的版本化正式真源，不是所有现实数据的唯一存储。

## 2. Operational State

以下状态由对应 Operational Source 保持权威：

- TickTick 任务与完成状态；
- Calendar 会议；
- 邮件原文与邮箱状态；
- RPG 当前状态数据库；
- Agent Job 状态；
- 业务系统记录；
- 程序运行时状态。

GitHub 可保存其 Schema、Rule 与 Migration，不机械保存全部实时状态。

## 3. Files / Blobs

Word、Excel、PDF、截图、音视频和大型附件应保存在：

- 合规公司存储；
- OneDrive；
- WPS；
- NAS；
- 其他授权文件系统。

GitHub 只保存适合版本化的模板、脱敏样例、规则和代码。

## 4. Human Authority

以下内容由用户本人拥有最终 Authority：

- Preference；
- Decision；
- Plan；
- Constraint；
- Personal Principle；
- 价值判断；
- 是否接受建议；
- 是否批准正式变更。

API 不得替代用户定义其意图。

## 5. Input Source 不等于 Authority

不得建立简单全局排行榜：

```text
API > 文件 > OCR > 自然语言
```

应按字段判断：

- 机器已知事实：API、DB、文件可能更权威；
- 人的意图与判断：用户表达更权威；
- OCR：默认是 Candidate Observation；
- 外部 AI 建议：不自动成为用户决定；
- 来源冲突：进入 Reconciliation，不静默覆盖。

## 6. Obsidian / Notion / ChatGPT Context

### Obsidian

可作为本地 Markdown 的浏览、双链和编辑界面。

若直接打开 Git Repo 中的 Markdown，则不产生第二真源。

### Notion

可作为结构化研究工作区、Inbox、资料数据库或协作界面。

正式结论晋升后应写入对应 Canonical Repo；Notion 中保留来源或工作状态。

### ChatGPT Project / Context

属于 Runtime Context 或 Projection。

可以帮助推理，不作为正式定义、Rule 和长期结论的唯一来源。

## 7. Derived Asset

Projection、Cache、Index、Embedding、Vector DB 和 Derived Summary 应标明：

- Canonical Source；
- 更新时间；
- 生成方式；
- 非 Canonical 状态。

不得让派生内容反向覆盖正式真源。

## 8. 敏感边界

Private Repo 不等于合规授权。

公司客户资料、内部制度、未公开项目文件和其他受限信息，只有在明确允许时才能进入个人 GitHub、个人云或家庭 Gateway。

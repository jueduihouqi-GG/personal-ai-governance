---
asset_id: GOV-CHANGE
asset_type: change_governance
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-ROOT
  - GOV-CONCEPTS
  - GOV-ASSET-ARCH
  - REG-SYSTEMS
---

# Change Control — 正式变更与全面影响分析

## 1. 适用范围

本协议适用于：

- Material Change；
- Principle / Rule 变更；
- Core Concept 定义变更；
- Repo Boundary 或 Routing 变更；
- Authority Owner 变更；
- Mother Rule、Workflow、Skill 或 Program 默认行为变更；
- 发现 Semantic Duplication 后的结构调整。

A0 纯排版和错字不属于 Material Change，但仍通过 Git 留痕。

## 2. 变更等级

### A0 — Editorial

不改变正式含义、行为、Scope、Authority 或结果。

### A1 — Domain Material Change

改变单一 Domain、System、Project 或 Skill 内的正式含义或行为。

### A2 — Root / Cross-system Material Change

改变以下任一内容：

- Root Rule；
- Core Concept 定义；
- 跨系统 Routing；
- Repo Boundary；
- Authority Owner；
- 写权限、安全、隐私或合规边界；
- 多个 System 的共同依赖。

无法确定等级时按更高一级评估。

## 3. 十步变更协议

### 1. IDENTIFY

明确目标 Asset ID、Authority Owner、Scope 与变更等级。

### 2. READ

读取：

- 当前 Canonical File；
- 相关 Git History；
- 上级 Principle；
- 直接 `depends_on`；
- 已知 Evidence。

### 3. CHALLENGE

说明：

- 现状哪里不再适用；
- 触发原因；
- 不修改的风险；
- 是事实变化、执行失败、结构缺陷还是新能力出现。

### 4. SEARCH

执行全面影响检索：

1. 搜索目标 Asset ID；
2. 搜索受影响 Concept ID；
3. 搜索正式别名与关键短语；
4. 搜索 Primary Repo；
5. A2 或跨系统 A1 搜索 `REG-SYSTEMS` 中的 Shared Consumer Repo；
6. 搜索 Workflow、Skill、Agent、Program、Schema、Test、Binding、Projection；
7. 检查 Git History 中旧设计理由。

### 5. CLASSIFY IMPACT

将命中项分为：

- 仅引用，无需改；
- 应用后果需要改；
- 依赖规则需要改；
- Projection 需要重建；
- Test / Eval 需要更新；
- 存在 Semantic Duplication，需要结构重构；
- 不相关误命中。

### 6. REFACTOR BEFORE SYNC

如果发现多处同义规范正文：

- 优先确定唯一 Canonical Owner；
- 上提到共同父级，或建立 Cross-cutting Asset；
- 将其他副本改为引用；
- 不把“所有地方同步改一遍”作为长期方案。

### 7. PROPOSE CHANGE SET

形成完整变更集：

- 原规则；
- 新规则；
- 修改理由；
- Evidence；
- 影响清单；
- 需要修改、迁移、废弃或重建的文件；
- 风险；
- 回滚方式；
- 暂不处理事项。

### 8. APPROVE

- A0：可直接执行，保留 Commit；
- A1：需要用户明确批准；
- A2：需要用户明确批准，并建议 ADR / Migration Note。

### 9. APPLY ATOMICALLY

多文件联动变更应尽量在一个受控 Change Set 中完成。

推荐执行方式：

| 场景 | 执行方式 |
|---|---|
| 单文件 A0 | ChatGPT 或 GitHub Web |
| 独立单文件低风险 A1 | ChatGPT，写前确认 |
| 多文件 A1 / A2 | Codex / Local Git |
| Code、Schema、Test、Migration | Codex + 测试 |
| Repo 拆分、合并、迁移 | ADR + Codex / Local Git |

### 10. VERIFY & PROPAGATE

变更后必须：

- 再次搜索 Asset ID 与旧关键短语；
- 确认无残留冲突副本；
- 更新受影响 Test / Eval；
- 重建 Projection；
- 更新 Binding / Registry（如适用）；
- 记录 Commit；
- 设定必要的后续复核。

## 4. 周期复核

以下时点触发治理复核：

- 新 System 加入；
- 重要 Phase 完成；
- 重大失败或安全回归；
- Repo 拆分或合并；
- Architecture Candidate 获得真实验证；
- Root Governance 默认每 90 天检查一次；
- Domain 可在 `REG-SYSTEMS` 中自定义周期。

周期复核不要求全量重写，只检查：

- 是否存在重复；
- 是否有失效规则；
- 是否有未传播变更；
- Routing 是否仍准确；
- Candidate 是否应晋升、继续观察或废弃。

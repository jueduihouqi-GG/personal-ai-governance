---
asset_id: GOV-ASSET-ARCH
asset_type: asset_governance
authority: personal-ai-governance
scope: root
status: active
version: "0.2.3"
depends_on:
  - GOV-ROOT
  - GOV-CONCEPTS
---

# Core Asset Architecture — 核心资产架构

## 1. 准入门槛

只有满足下列至少一项，并通过人工判断值得长期维护的内容，才应成为 Core Asset：

1. 预计会在多个会话、阶段、Project 或 Runtime 中复用；
2. 丢失或漂移会造成明显生产、判断、安全或维护损失；
3. 定义长期默认判断、禁止边界或正式流程；
4. 是稳定 Workflow、Skill、Agent 或 Program 的必要依据；
5. 是高价值 Knowledge，未来可能支持或修正 Principle；
6. 需要版本、审计、回滚或跨模型复用。

以下内容默认不入治理体系：

- 一次性答案；
- 临时草稿；
- 普通闲聊；
- 未验证的零散想法；
- 大部分短期 Project；
- 原始运行状态；
- 可从其他来源随时重建的信息。

## 2. Core Asset 类型

Core Asset 可包括：

- Meta Governance；
- Principle；
- Rule；
- Knowledge；
- Workflow；
- Skill；
- ADR；
- Schema；
- Program Source Code；
- Test / Eval Specification；
- Registry Entry。

是否进入治理由价值决定，不由文件类型决定。

## 3. 单一语义真源

每个 Core Asset 必须有：

```yaml
asset_id:
asset_type:
authority:
scope:
status:
version:
depends_on:
```

同一正式定义、Rule 或 Conclusion 只允许一个 Canonical File。

其他文件可以：

- 通过 Asset ID 引用；
- 描述本地应用后果；
- 指向正式来源；
- 生成 Projection。

其他文件不得：

- 复制同义定义；
- 手工维护平行摘要；
- 用不同术语重写同一规范；
- 因“方便阅读”制造第二真源。

## 4. 树状主干与交叉层

核心资产结构采用：

> 树状主干 + 横向交叉层

逻辑上视为有向无环依赖图（DAG）。

### 4.1 纵向主干

```text
Meta Governance
  ↓
Principle
  ↓
Rule
  ↓
Workflow / Skill / Program
```

Knowledge 与 Evidence 可支持多个层级，但不得自动获得规范性权威。

### 4.2 相同内容的处理顺序

当多个分支出现相同正式内容时：

1. 判断能否提升到共同上级；
2. 若提升后 Scope 仍准确，则在共同上级建立唯一 Canonical Asset；
3. 若无法合理提升，建立独立 Cross-cutting Asset；
4. 原分支改为引用，不保留手工同义正文。

### 4.3 交叉资产

Cross-cutting Asset 只在确有跨域依赖时创建。

不得把所有内容都放进“通用层”，避免形成新的超级文件。

## 5. 定义与应用分离

以 `Principle` 为例：

- `CON-005` 的定义只存在于 `GOV-CONCEPTS`；
- 某 Domain 可以说明“该 Principle 在本 Domain 如何应用”；
- Domain 不得重新定义 Principle 是什么。

同理：

- Root Rule 只规定最高边界；
- Domain Rule 只处理本 Domain；
- Skill Local Rule 只处理 Skill Scope。

## 6. 引用标准

引用正式内容时，应包含 Stable ID。

示例：

```text
本 Workflow 依赖 `GOV-CHANGE`。
本地规则依据 `CON-005` 与 `CON-006` 区分 Principle 和 Rule。
```

路径可以变化，Stable ID 应保持。

## 7. Projection、Summary 与用户展示板

### 7.1 允许

- 自动生成的项目摘要；
- 面向 Runtime 的 Context Pack；
- 指针式目录；
- 标明来源与更新时间的 Derived Summary；
- 从同一状态数据生成的机器可读视图与用户可读视图。

### 7.2 不允许

- 手工复制一份“精简版规则”并长期独立维护；
- Projection 反向成为 Canonical Source；
- 摘要与正式规则发生冲突却继续使用；
- 机器视图与用户视图分别手工维护并独立演化；
- 仅用英文键名、英文枚举或代码块向用户展示需要其理解、判断或批准的治理状态。

### 7.3 用户可读展示板

当 Runtime 向用户展示以下任一内容时，必须提供完整的中文用户展示板：

- 当前状态或控制状态；
- 架构状态；
- 迁移进度；
- 审批状态；
- Change Set；
- Backlog；
- 执行结果；
- 风险、阻断与待决事项；
- 其他需要用户理解、判断或批准的治理视图。

具体要求：

1. **中文展示为必需的人类界面。** Stable ID、产品名、路径、代码、英文枚举和机器字段可以保留，但不得替代中文说明。
2. **机器视图可以同时存在。** 若展示 YAML、JSON、英文状态键或其他机器可读状态，应在其紧邻位置同时提供语义一致的中文展示板；不得要求用户自行翻译。
3. **同源生成。** 中文展示板与机器视图必须来自同一底层状态，不得成为两份分别维护的正式状态。
4. **中文展示板至少说明与当前任务有关的以下内容：**
   - 现在处于什么阶段；
   - 已经完成什么；
   - 尚未完成什么；
   - 是否存在阻断、风险或待用户决定事项；
   - 当前允许和禁止的写回范围；
   - 下一步动作；
   - 必要时说明正式来源、版本或 Commit。
5. **状态翻译。** 面向用户时应使用清楚的中文状态，例如：
   - `COMPLETE` → 已完成；
   - `PARTIAL` → 部分完成；
   - `PENDING` → 待处理／待批准；
   - `NOT_STARTED` → 尚未开始；
   - `BLOCKED` → 受阻；
   - `DEFERRED` → 暂缓；
   - `PASS` → 通过；
   - `FAIL` → 未通过。
6. **不得只展示代码式状态。** 即使机器状态准确，只要该视图的目的包含让用户阅读、审核、批准或控制，就必须增加中文解释层。
7. **冲突处理。** 若中文展示板与机器状态或 Canonical Source 不一致，应停止依赖该展示板作出正式决策，修正生成逻辑并重新生成；中文展示板本身不获得独立 Canonical Authority。

推荐展示顺序：

```text
中文用户展示板
→ 可选的机器可读状态
→ 来源、版本或技术细节
```

## 8. 依赖记录

正式文件使用 `depends_on` 单向记录直接依赖。

不手工同时维护 `consumed_by`，反向依赖通过搜索 Asset ID 得到。

这样可以避免双向清单本身发生漂移。

## 9. 重复发现后的默认动作

发现 Semantic Duplication 时，默认不是“同时修改所有副本”。

应先判断：

- 哪一个才是 Canonical Owner；
- 是否应上提；
- 是否应新建 Cross-cutting Asset；
- 哪些位置应改为引用；
- 是否需要迁移或废弃旧副本。

同步修改只能作为临时修复，不得成为长期结构。

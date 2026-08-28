---
asset_id: GOV-ROOT
asset_type: meta_governance
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-CONCEPTS
---

# Root Rules — 零级规则

本文件只保存最高层治理约束。术语定义以 `GOV-CONCEPTS` 为唯一来源，具体执行协议由下级 Canonical Asset 负责。

## M0-01 — 人类最终治理权

Root Governance、跨系统 Routing、Repo Boundary、高影响写权限与重大 Principle 的最终批准权属于用户本人。

该规则终止“母规则的母规则”无限递归。

## M0-02 — 只治理核心资产

只有符合 `GOV-ASSET-ARCH` 准入条件的 Core Asset 才进入正式治理。

不得把所有 Chat、Project、资讯、笔记和临时想法强行制度化。

## M0-03 — 单一语义真源

同一概念的定义、同一规范性规则或同一正式结论只能有一个 Canonical Owner。

其他位置只能引用、应用或生成可重建 Projection，不得手工维护第二份同义正文。

## M0-04 — 推理自由，持久化受治理

AI 可以自由发散、质疑旧规则、提出新架构和使用新证据。

AI 不得因一次推理或一次对话静默修改 Canonical Asset 或 Operational State。

## M0-05 — 权威来源明确

每一类 Formal Object 和 Operational State 必须有明确 Authority Source。

具体边界由 `GOV-SOURCE` 统一规定。

## M0-06 — 实质性变更必须全面影响分析

修改 Material Change 时，不得只改当前文件。

必须按 `GOV-CHANGE` 检索所有引用、依赖、下游 Workflow、Skill、Agent、Program、Test、Binding 和 Projection，并决定修改、迁移或重构。

## M0-07 — 路由可版本化，不是最终真理

System 分类、Repo 划分、Binding 与 Routing 可以演进。

任何实质性变化必须可追溯、可解释，并保留必要迁移记录。

## M0-08 — 允许领域局部母规则

不同 Domain、Agent、Skill 和 Program 可以拥有自身 Mother Rule、Semantic Routing 与 Write Authorization。

局部规则只在其 Scope 内生效，不自动上升为 Root Rule。

## M0-09 — 最小上下文与渐进检索

治理体系不得要求每次思考都加载全部规则。

检索强度按 Runtime 和任务后果决定，具体规则由 `GOV-PROJECT` 管理。

## M0-10 — 周期复核与真实反馈优先

架构候选、Routing 和治理规则必须在 Phase Gate、重大失败、系统新增或约定周期进行复核。

不得只依靠纸面推演无限扩张体系。

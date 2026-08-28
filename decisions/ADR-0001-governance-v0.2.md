---
asset_id: ADR-0001
asset_type: architecture_decision
authority: personal-ai-governance
scope: root
status: accepted
version: "0.2"
depends_on:
  - GOV-ROOT
  - GOV-CONCEPTS
  - GOV-ASSET-ARCH
  - GOV-CHANGE
  - GOV-PROJECT
  - GOV-SOURCE
---

# ADR-0001 — 建立 Personal AI Governance V0.2

## Context

已有 ChatGPT Project、本地 Agent、程序和 GitHub Repo 正在形成可复用资产。

主要风险不是缺少更多工具，而是：

- 同一概念和 Rule 在多个 MD 中重复；
- 修改一处后其他位置漂移；
- 新 Project 不知道对应哪个 Repo；
- 为所有 Project 强加同一重型框架；
- 每轮 Context 越来越重；
- 未来 Routing 改变时无法追溯。

## Decision

采用以下 V0.2 方案：

1. 只治理 Core Asset；
2. 建立唯一概念字典；
3. 同一语义只允许一个 Canonical Owner；
4. 主结构采用树状主干，交叉内容建立独立 Cross-cutting Asset；
5. Project Instructions 只保存最薄 Binding；
6. 路由由 `REG-SYSTEMS` 统一维护；
7. 检索采用 open / selective / grounded / strict 四种模式；
8. 开放思考采用 diverge_then_ground；
9. Material Change 必须全面搜索影响并优先消除 Semantic Duplication；
10. V0.2 不建设全局自动 Router、Gateway 或最终 Ontology。

## Consequences

### Positive

- 核心资产可复用且可审计；
- 不要求大部分 Project 进入治理；
- 定义和 Rule 只有一处正式来源；
- 变更可以系统评估下游影响；
- 新 Project 可低成本加入；
- Context 负担按任务控制；
- Repo 与 Routing 可持续演进。

### Cost

- 需要维护 Stable ID 与 `depends_on`；
- Material Change 比普通写作更谨慎；
- 当前反向依赖依赖 GitHub 搜索或 Codex 检索；
- 复杂多文件变更仍需 Codex / Local Git；
- 自动 Projection 与自动 Router 尚未实现。

## Deferred

- 全局 Intent Taxonomy；
- 自动跨 Repo Context Router；
- 自动 Dependency Graph；
- Obsidian / Notion 自动双向同步；
- Gateway；
- Event Bus；
- 自动 Principle Writeback；
- NAS 部署。

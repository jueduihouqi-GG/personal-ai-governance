---
asset_id: GOV-BOOTSTRAP
asset_type: bootstrap_protocol
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-ROOT
  - GOV-PROJECT
  - REG-SYSTEMS
---

# BOOTSTRAP — 受治理 Runtime 开机协议

## 1. 输入

每个受治理 Runtime 只需要在自身显式配置中保存：

```yaml
governance_bootstrap:
  repo: jueduihouqi-GG/personal-ai-governance
  path: BOOTSTRAP.md

system_id: example-system
runtime_id: example-runtime
```

Primary Repo、Shared Systems、检索强度和写回策略不得在多个 Project Instructions 中重复维护，统一由 `REG-SYSTEMS` 决定。

## 2. 开机步骤

1. 读取当前 `system_id` 与 `runtime_id`。
2. 查询 `REG-SYSTEMS` 中对应条目。
3. 确认：
   - Primary Canonical Repo；
   - Shared Systems；
   - Operational Sources；
   - Retrieval Mode；
   - Writeback Policy；
   - 数据边界。
4. 根据 `GOV-PROJECT` 按需读取相关 Canonical Asset。
5. 不默认全量加载所有 Repo 或所有 MD。
6. 若任务触及正式变更，转入 `GOV-CHANGE`。
7. 若身份、路由、权限或真源冲突，不得猜测性写回。

## 3. 非受治理 Project

没有 `system_id` 的 Chat / Project：

- 可正常自由使用；
- 不自动猜测 Repo；
- 不自动创建 Registry 条目；
- 不自动进入复杂治理；
- 只有当出现值得长期保存的核心资产时，才提出治理化建议。

## 4. 失败安全

以下任一情况出现时，停止正式写回并要求人工判断：

- `system_id` 或 `runtime_id` 不存在；
- Registry 与 Project 显式配置冲突；
- Canonical Owner 不明确；
- 规则互相冲突；
- 需要访问未经授权的敏感数据；
- 现有规则明显可能过时，但尚未完成变更治理。

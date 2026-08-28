---
asset_id: TPL-PROJECT-BINDING
asset_type: template
authority: personal-ai-governance
scope: root
status: active
version: "0.2"
depends_on:
  - GOV-BOOTSTRAP
  - GOV-PROJECT
  - REG-SYSTEMS
---

# Project Binding Template

将以下最小 Binding 放入受治理 Project 的 Project Instructions 或 Runtime 配置：

```yaml
governance_bootstrap:
  repo: jueduihouqi-GG/personal-ai-governance
  path: BOOTSTRAP.md

system_id: example-system
runtime_id: example-runtime
```

## 使用说明

- 不在这里重复 Primary Repo；
- 不在这里重复 Shared Repo；
- 不在这里复制 Rule；
- 不在这里复制 Retrieval Policy；
- 所有路由信息统一从 `REG-SYSTEMS` 读取。

若 Runtime 无法访问 GitHub，应使用明确标注来源和更新时间的 Projection，且不得把 Projection 视为 Canonical Source。

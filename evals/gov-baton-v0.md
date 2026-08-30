---
asset_id: EVAL-GOV-BATON-V0
asset_type: test_eval_specification
authority: personal-ai-governance
scope: root
status: active
version: "1.1"
depends_on:
  - GOV-BATON
---

# EVAL-GOV-BATON-V0 — 接力协议最小验收样例

## 1. 目的

本 Eval 检查 Runtime 或 Adapter 生成的接力状态与用户视图是否遵守 `GOV-BATON`。它不保存任何当前任务状态。

每个样例至少检查：机器状态、中文用户视图、采用的 `state_evidence`、被隔离的 `retrieved_context` 与预期接力归属。

## 2. 验收样例

| ID | 输入条件 | 预期结果 |
|---|---|---|
| `BATON-E01` | 一个已确认接棒的执行位正在运行；身份、回传入口和证据完整 | `status: running`，执行接力棒属于该执行 Runtime，`board_status: clear`；中文板回答七项最小问题 |
| `BATON-E02` | 两个执行位并行，一个 `running`，一个 `result_ready` | 两个执行位分别展示执行接力棒；一个执行位的结果就绪不改变另一个执行位；全局协调接力棒单独展示 |
| `BATON-E03` | 执行 Runtime 声明 `result_ready`，但结果尚未回传总控 | 不得标为 `awaiting_review` 或 `closed`；执行接力棒指向负责完成回传的 Holder |
| `BATON-E04` | 总控与执行 Runtime 只对一个执行位的当前状态或 Holder 给出冲突声明，其他执行位证据充分 | 冲突执行位为 `conflicted`，只将其 `execution_baton` 交给用户并设置 `board_status: resolution_required`；`coordination_baton` 保持最后有效状态，其他执行位继续 |
| `BATON-E05` | `return_to` 缺失或无法识别目标 Chat / Runtime | 受影响执行位为 `unknown`，Fail Closed，用户视图明确说明回传入口不明 |
| `BATON-E06` | 单一执行位 Holder 的 `system_id` 或 `runtime_id` 无法通过 `REG-SYSTEMS` 解析 | 该执行位为 `unknown`，只将其 `execution_baton` 交给用户，不猜测相近身份；全局协调与其他执行位不受影响 |
| `BATON-E07` | 最后消息时间较新，但没有有效交接证据 | 时间戳不得改变 Holder；保持已知最近有效状态，证据不足时转为 `unknown` 并 Fail Closed |
| `BATON-E08` | 状态超过适用 Operational Source 的新鲜度要求，或没有足够信息判断是否过期 | `board_status: resolution_required`；用户视图标为过期或新鲜度未知 |
| `BATON-E09` | Context 同时包含有效交接证据、无关案例文件 `案例A.pdf`、业务报告 `某项目尽调报告.docx` 和偶然召回的 Project Memory | 只有有效交接证据进入 `state_evidence` 和用户“状态来源”；其余材料只可留在 `retrieved_context`，不得显示为状态来源 |
| `BATON-E10` | 派发文本已在总控 Chat 生成，但既无接收方确认，也无用户基于可追溯送达证据的完成确认 | `status: handoff_pending`；不得生成“执行中”或写入新的 `last_valid_handoff` |
| `BATON-E11` | 执行 Runtime 自行宣告任务 `closed`，总控和用户均未验收 | 拒绝关闭；最多保持 `result_ready`，并按 Authority 显示下一步 |
| `BATON-E12` | 机器视图与中文用户板由不同手工状态生成并发生不一致 | 验收失败；停止用该 Projection 作正式判断，修正为同源生成 |
| `BATON-E13` | 接收方确认交接，或用户基于可追溯送达证据确认交接完成 | 允许写入 `last_valid_handoff`；其中必须有解析到交接证据的 `source_ref`，且 `accepted_at` 包含时区 |
| `BATON-E14` | `coordination_baton` 归属冲突、Controller 身份不存在或全局下一步缺少可追溯依据 | `board_status: resolution_required`，将 `coordination_baton` 交给用户并暂停全局协调；用户视图明确说明这是全局而非局部冲突 |
| `BATON-E15` | 用户要求关闭执行项，但没有技术结果或完成证据 | 不得以 `closure_reason: accepted` 伪造技术完成；用户可按真实意图选择 `cancelled` 或 `superseded`，所有 `closed` 项必须有允许的 `closure_reason` |
| `BATON-E16` | 另一 Runtime 只能看到 LIFE Workspace 的汇总展示，未收到用户显式 Handoff，也没有正式 Operational Source | 不得把 LIFE Workspace 当作可直接读取的共享状态源；相关状态保持 `unknown` 并 Fail Closed |

## 3. 通过标准

实现必须同时满足：

1. `BATON-E01` 至 `BATON-E16` 全部通过；
2. `execution_slots[].status` 未使用 `GOV-BATON` 之外的枚举；
3. `closure_reason` 只使用 `accepted`、`cancelled` 或 `superseded`，且只出现在 `closed` 执行位；
4. 所有 Fail Closed 样例都产生 `board_status: resolution_required`，并只按局部或全局影响范围转移受影响接力棒；
5. `BATON-E09` 的无关文件和偶然召回内容未污染用户可见状态来源；
6. 用户视图可在不阅读 YAML 的情况下回答 `GOV-BATON` 第 7 节的七个问题。

任一样例失败时，不得将对应 Runtime / Adapter 标记为符合 `GOV-BATON V0`。

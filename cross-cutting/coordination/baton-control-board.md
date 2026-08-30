---
asset_id: GOV-BATON
asset_type: cross_cutting_coordination_protocol
authority: personal-ai-governance
scope: root
status: active
version: "0.1.1"
protocol_version: V0
depends_on:
  - GOV-ROOT
  - GOV-CONCEPTS
  - GOV-ASSET-ARCH
  - GOV-SOURCE
  - REG-SYSTEMS
---

# GOV-BATON — Cross-Runtime Coordination Baton V0

## 1. 目的与边界

本协议适用于“一个总控 Runtime + 一个或多个执行 Runtime”的跨 Chat、Agent、Codex 或 Program 协作。它定义 V0 的接力语义、Authority、最小状态、用户展示、失败安全、来源隔离与多执行位规则。

本仓库只保存可版本化的协议、Schema、ADR 与 Eval，不保存当前实时接力状态：

```text
Protocol / Schema / ADR
→ personal-ai-governance

V0 Current State Evidence
→ 用户显式 Handoff
→ 当前 Runtime 在自身 Authority 内的直接声明
→ 未来明确登记的 Operational Source

LIFE Workspace
→ V0 用户操作的状态汇总与展示入口
→ 不是其他 Runtime 可直接读取的共享 Operational Source

User-readable Board
→ V0 Current State Evidence 的 Projection
```

LIFE Workspace 中的汇总或展示不会自动成为跨 Runtime 状态证据；只有用户通过显式 Handoff 转交，并保留可追溯来源与送达证据时，接收 Runtime 才可在自身 Context 中使用该证据。

`REG-SYSTEMS` 只登记稳定的 System、Runtime、路由与来源边界，并负责 Holder / Runtime 身份解析；不得被改造成临时任务状态表。接力控制板不得反向成为 Operational Source 或 Canonical Source。

## 2. 正式概念

以下术语的唯一正式定义位于 `GOV-CONCEPTS`：

- `CON-028` — Coordination Baton｜协调接力棒；
- `CON-029` — Execution Baton｜执行接力棒；
- `CON-030` — Handoff｜交接；
- `CON-031` — Last Valid Handoff｜最近一次有效交接；
- `CON-032` — Baton Control Board｜接力控制板。

本文件只规定这些概念在 V0 中的协议行为，不维护平行术语定义。

## 3. Authority

| 角色 | 允许声明或决定 | 不得越权 |
|---|---|---|
| 用户 | 全局重新分配、纠正、最终批准、关闭，以及冲突裁决 | 不得在缺少技术证据时把未完成、未运行或未产出的技术事实声明为已完成 |
| 总控 Runtime | 任务拆分、全局下一步、执行结果验收、回传入口与协调接力状态 | 不得伪造执行 Runtime 的已接收、运行、阻塞或结果就绪声明 |
| 执行 Runtime | 自己负责的执行项已接收、运行、阻塞、结果就绪及相应执行接力状态 | 不得替其他执行位或总控作出验收、关闭或全局重分配 |
| 接力控制板 | 从同一底层状态生成用户视图和可选机器视图 | 只展示，不产生、修改或裁决状态 |
| Chat Memory | 为当前 Runtime 提供 Working Context | 不作为跨 Chat 当前状态真源 |

用户的明确纠正对接力归属、批准、取消和治理关闭具有最终 Authority，但不反向创造技术执行事实。任何技术完成、运行状态或结果存在性声明都必须有相应 Runtime 声明或其他适用证据，并受身份、权限、来源与新鲜度校验约束。

## 4. 接力模型与有效交接

1. 每个 `workstream_id` 必须有且只有一个协调接力棒，表示全局下一项协调动作的责任方。
2. 每个未关闭的执行位必须有且只有一个执行接力棒；多个执行位可以并行并持有各自接力棒。
3. 当前接力棒回答“现在谁必须完成下一项动作”；最近一次有效交接只记录最近一次已完成的受控转移。两者不得混用。
4. 时间戳只用于判断证据新鲜度与辅助审计，不得单独决定接力归属。
5. 有效交接的确认标准为：接收方确认；或用户基于可追溯送达证据确认交接完成。
6. 一次交接只有在以下条件全部满足时才可写为 `last_valid_handoff`：
   - 交出方与接收方身份已知；
   - 交出方有权发起该转移；
   - 已满足上述与 `CON-031` 一致的确认标准；
   - `expected_action` 与 `return_to` 明确；
   - `source_ref` 指向可追溯的 `state_evidence`。
7. 派发消息已生成但尚未满足确认标准时，状态仍是 `handoff_pending`，不得声称执行 Runtime 已经接棒。

## 5. V0 状态

`execution_slots[].status` 只允许以下精简枚举，不建立额外复杂状态机：

| 枚举 | 中文含义 |
|---|---|
| `handoff_pending` | 交接待完成 |
| `running` | 执行中 |
| `result_ready` | 结果已就绪，待按回传入口交付 |
| `awaiting_review` | 已回传，待总控验收 |
| `blocked` | 执行受阻 |
| `closed` | 已关闭，关闭性质由 `closure_reason` 说明 |
| `unknown` | 证据不足，状态未知 |
| `conflicted` | 存在未解决的冲突声明 |

`board_status` 不是执行状态机，只允许：

- `clear`：当前状态足以生成无冲突的 Projection；
- `resolution_required`：必须由用户澄清或裁决后才能继续。

`closure_reason` 不是执行状态，只在 `status: closed` 时使用，并只允许：

- `accepted`：总控或用户基于适用结果证据验收关闭；
- `cancelled`：用户或有权总控取消后关闭；
- `superseded`：该执行项已被明确的新执行项或新版本取代。

## 6. 最小机器 Schema

```yaml
workstream_id:
controller:
  system_id:
  runtime_id:

coordination_baton:
  holder_type:
  holder_id:
  expected_action:

execution_slots:
  - task_id:
    executor:
      system_id:
      runtime_id:
    status:
    closure_reason:
    execution_baton:
      holder_type:
      holder_id:
      expected_action:
    return_to:
      system_id:
      runtime_id:
      chat_ref:
    last_valid_handoff:
      from_holder_id:
      to_holder_id:
      expected_action:
      accepted_at:
      source_ref:
    updated_at:
    source_ref:

board_status:
conflicts: []

state_evidence:
  - source_ref:
    claim:
    observed_at:

retrieved_context:
  - source_ref:
    purpose:
```

约束：

1. `holder_type` 只允许 `user`、`controller_runtime` 或 `executor_runtime`。
2. `holder_id` 必须通过 `REG-SYSTEMS` 解析到已知 Runtime，或明确解析为用户；不能解析时执行 Fail Closed。
3. 每个执行位的 `source_ref` 必须解析到 `state_evidence` 中实际支持其当前状态的条目；`last_valid_handoff.source_ref` 必须解析到实际支持交接送达与确认的条目。二者均不得指向 `retrieved_context`。
4. `accepted_at`、`updated_at` 与 `observed_at` 必须包含时区；时间戳本身不授予 Authority。
5. `return_to` 必须足以让用户识别结果应返回的 Chat 或 Runtime。
6. `status: closed` 必须同时记录 `closure_reason`；未关闭的执行位不得记录该字段。`accepted` 必须有技术结果或验收证据，用户的关闭 Authority 不得被用来伪造技术完成事实。
7. 中文用户视图和可选机器视图必须从这一份底层状态生成，不得分别手工维护。

## 7. V0 最小用户视图

接力控制板执行 `GOV-ASSET-ARCH` 的中文用户展示板规则，并至少直接回答：

1. 当前有多少个已知活跃 AI / Agent 执行项；
2. 每项由谁执行；
3. 每项当前状态；
4. 每项当前下一步；
5. 结果应返回哪个 Chat 或 Runtime；
6. 当前轮到用户、总控还是执行 Runtime；
7. 状态是否明确、过期或冲突。

“已知活跃执行项”指 `status` 不为 `closed` 的执行位；`unknown` 与 `conflicted` 仍计入活跃项，直到用户或总控按 Authority 完成处置。

推荐最小版式：

```text
接力控制板
- 工作流：<workstream_id>
- 全局当前轮次：<责任方及预期动作>
- 已知活跃执行项：<数量>

执行项
- <task_id>｜执行者｜状态｜下一步｜回传入口｜新鲜度/冲突

状态判断
- 明确 / 过期 / 冲突 / 需要用户裁决
- 实际状态证据：<state_evidence 中被采用的来源>
```

## 8. 多执行位规则

1. 每个执行位必须使用稳定且唯一的 `task_id`，并单独记录执行者、状态、执行接力棒、回传入口和最近一次有效交接。
2. 一个执行位的完成、阻塞或冲突不得隐式改变其他执行位的接力棒。
3. 总控 Runtime 可以同时等待多个执行位；协调接力棒与各执行接力棒必须分别展示。
4. `result_ready` 只表示执行 Runtime 声明结果可交付，不等于总控已收到或已验收。
5. 只有总控 Runtime 或用户可以把执行项判为 `closed`；执行 Runtime 不得自行关闭验收链路。
6. 关闭时必须记录 `closure_reason`。`accepted` 需要适用技术结果或验收证据；无此证据时，用户仍可按真实意图选择 `cancelled` 或 `superseded`，但不得把未发生的技术完成写成事实。

## 9. Fail Closed

出现以下任一情况时，不得猜测谁应继续：

- 状态来源不足或无法追溯；
- 两个 Runtime 对同一接力棒或状态给出冲突声明；
- 回传入口不明；
- 状态超过适用 Operational Source 的新鲜度要求，或无法判断是否过期；
- `system_id`、`runtime_id` 或 Holder 身份不存在。

影响范围必须先区分为局部执行位与全局协调状态。

仅单一执行位受影响时：

- 该执行位必须标为 `unknown` 或 `conflicted`；
- 只将该执行位的 `execution_baton` 交给用户裁决；
- `coordination_baton` 保持最后一个有充分证据的有效状态；
- 其他具有独立、充分证据的执行位可以继续；
- 控制板必须显式标出局部冲突，并设置 `board_status: resolution_required`。

```yaml
board_status: resolution_required
execution_slots:
  - status: conflicted
    execution_baton:
      holder_type: user
      holder_id: user
      expected_action: clarify_or_resolve_slot
```

只有全局协调状态本身不明时，才暂停全局协调并生成：

```yaml
board_status: resolution_required
coordination_baton:
  holder_type: user
  holder_id: user
  expected_action: clarify_or_resolve_coordination
```

全局协调状态不明包括协调接力棒归属冲突、Controller 身份无法解析，或全局下一步缺少可追溯依据。此时用户视图可以简写为 `current_baton: user`，但该写法只是 Projection；机器状态仍以 `coordination_baton` 为唯一字段，不得并行维护第二份接力状态。

## 10. 来源隔离

- `state_evidence` 只包含实际用于判断接力棒、执行状态、回传入口或新鲜度的来源，并且只能来自：用户显式 Handoff、当前 Runtime 在自身 Authority 内的直接声明，或未来明确登记的 Operational Source。
- `retrieved_context` 只包含辅助理解任务、但未用于当前状态判断的材料。
- 用户视图的“状态来源”只能展示 `state_evidence`；不得把 `retrieved_context` 混入来源清单。
- 无关项目文件、案例文件、业务报告名、Project Memory 偶然召回内容，即使出现在当前 Context 中，也不得被列为状态来源。
- 某份 Context 只有在其具体声明实际参与状态判断且具有适用 Authority 时，才可迁入 `state_evidence`。
- LIFE Workspace 是用户操作的汇总与展示入口，不是其他 Runtime 可直接读取的共享 Operational Source；其中内容只有经用户显式 Handoff 且保留可追溯来源与送达证据后，才可成为接收 Runtime 的 `state_evidence`。
- 当前 Runtime 的直接声明只覆盖其自身 Authority，不得借此声明另一个 Runtime 的当前状态。

## 11. V0 操作限制

- 用户可以在总控与执行 Runtime 之间手工转发派发内容和结果。
- LIFE Workspace 可以帮助用户汇总和展示 V0 状态，但 Runtime 不得假定可以直接读取或自动同步其中状态。
- 已发送的历史消息不会自动变化；状态只在新证据到达并重新生成回复时更新。
- 不得假定一个 Chat 可以自动读取另一个 Chat 的最新状态。
- 不得把 Chat Memory 或本 Git 仓库当作共享实时状态库。
- V0 不建立数据库、Gateway、Event Bus、Webhook、Connector 或实时看板。
- V1 共享状态库与 V2 事件驱动能力继续作为 `CAND-008` 候选，不因本协议生效而被视为已实现。

## 12. 审计要求

每次生成或审查接力控制板时至少检查：

1. Controller、Executor 与 Holder 身份已通过 `REG-SYSTEMS` 或用户身份规则解析；
2. 每个未关闭执行位都有明确执行接力棒与 `return_to`；
3. 当前接力棒有 Authority 支持，且没有仅由时间戳推断；
4. `last_valid_handoff` 满足统一确认标准，含可解析的 `source_ref`，且 `accepted_at` 包含时区；
5. `state_evidence` 与 `retrieved_context` 已隔离；
6. 过期、冲突或证据不足时已按局部或全局影响范围 Fail Closed；
7. 每个 `closed` 执行位都有有效 `closure_reason`，且没有伪造技术完成事实；
8. 中文用户视图和机器视图来自同一状态。

最小验收样例由 `EVAL-GOV-BATON-V0` 维护。

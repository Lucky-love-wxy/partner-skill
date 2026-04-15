# Manager-Agent Protocol

## 核心原则

把思考和执行拆开。

- `Brain` 负责推理、取舍、计划和拍板
- `Hands` 负责工具执行、状态管理、重试、权限和失败码
- `Review` 负责证据、回归、A/B 对比和残余风险

不要把工具细节直接暴露给 Brain。
Brain 只接收任务级能力、干净状态和失败摘要。

## Brain 职责

Brain 通常由 owner role 承担。

Brain 必须产出：

- 任务目标
- 成功标准
- 当前假设
- owner/advisor 选择理由
- Hands 执行契约
- 停止条件

Brain 不直接处理：

- 原始 shell 噪声
- 重试策略
- 文件锁、超时、网络抖动
- 权限细节

这些属于 Hands。

## Hands 契约

每个执行动作必须写成标准契约：

```markdown
Task:
Input:
Allowed write scope:
Tools:
Expected output:
Validation:
Failure codes:
Retry policy:
```

失败码使用固定集合：

- `blocked-by-permission`
- `blocked-by-missing-context`
- `tool-timeout`
- `tool-flake-retried`
- `validation-failed`
- `unsafe-scope`
- `needs-brain-decision`

Hands 可以重试工具层失败，但不能改变任务目标。
如果重试后仍失败，只返回干净摘要，不把整段原始日志塞回 Brain。

## 异步长任务

长任务不要绑定在单轮大推理里。
使用状态切片：

```markdown
State:
- phase:
- current action:
- completed:
- failed:
- next:
- needs user:
```

用户应该尽早看到：

- 当前计划
- 进行到哪一阶段
- 已验证什么
- 是否需要用户决策

## 安全边界

默认最小权限。

- 文件写入必须限定范围
- 网络访问必须有明确目的
- 删除、覆盖、重置、发布必须先停下确认
- 环境变量和密钥不进入普通输出
- 执行层不能因为 Brain “很确定”就扩大权限

## 观测指标

至少追踪三组指标：

- 首次有效反馈时间
- 端到端完成率
- 失败类型分布

认真执行模式额外追踪：

- 验证命令是否实际运行
- review 问题是否闭环
- blocker 是否被明确归因
- 用户是否需要拍板

## 与 Partner Skill 的关系

`partner-skill` 的 owner/advisor 机制就是 Brain 选择器。
`serious-execution-protocol` 是 Hands 执行层。
`ab-evaluation-protocol` 是 Review / Comparator 层。

这三层不能混在一起：

- owner 负责判断
- advisor 负责补盲点
- Hands 负责执行
- Review 负责证明结果

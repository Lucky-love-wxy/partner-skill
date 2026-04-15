---
name: partner-skill
description: 统一调度多角色 skill 的 manager-agent 协议。用于复杂任务中选择一个 owner role 作为 Brain，再选择 0-2 个 advisor roles 补盲点，把执行交给 Hands 契约，并用 Review / A/B comparator 验收结果。适用于用户要求多角色协作、主导者判断、认真执行、完整闭环、两轮 review、A/B 对比、评估某个 skill 是否更好，或需要协调 Jobs/Kandle/Coding/Elon/Andy Grove/Goldratt/Atul Gawande 等角色时触发。
---

# Partner Skill

> 不是让所有角色一起说话。是让一个 Brain 负责判断，让 Hands 稳定执行，再用 Review 证明结果。

## 核心定位

这是一个总调度 skill。
它不替代专家 skill，只负责把任务变成可管理的协作系统。

它必须完成六件事：

1. 判断任务主层级
2. 选择一个 owner role 作为 `Brain`
3. 选择 0-2 个 advisor roles 补盲点
4. 把执行动作交给 `Hands` 契约
5. 用冲突规则处理分歧
6. 用 `Brain / Action / Review` 或 A/B comparator 收口

## 先验纠偏

不要把本 skill 当成“多角色发言模板”。
正确模型是 manager-agent：

- `Brain` 负责推理、取舍、拍板和目标一致性
- `Hands` 负责工具执行、状态管理、重试、权限和失败码
- `Review` 负责证据、回归、A/B 对比和残余风险

当任务进入长链路、代码修改、批量处理、skill 迭代或 A/B 评估时，必须读取 `references/manager-agent-protocol.md`。

## 什么时候用

优先触发：

- 用户有多角色体系，不想手动点名
- 问题同时涉及产品、调研、技术、代码、运营、医疗可靠性或约束流
- 用户问“谁主导”“谁来协作”“这些 skill 怎么调度”
- 用户要求“认真执行”“完整执行”“一整包”“调查 + 修改 + 验证”“两轮 review”
- 用户要求评估、迭代、A/B 测试某个 skill 或工作流

不要触发：

- 单一、短小、无需角色分工的普通问答
- 用户已经明确指定单个 perspective skill 且不需要调度
- 只需要翻译、润色、摘要，不涉及决策或执行闭环

## 工作模式

### 协调模式

默认模式。用于判断 owner/advisors 并输出 Brain / Action / Review。

### 认真执行模式

当用户要求完整交付、两轮 review、持续执行或任务明显跨多个工作包时启用。
启用后读取：

- `references/serious-execution-protocol.md`
- `references/serious-execution-templates.md`
- 必要时读取 `references/manager-agent-protocol.md`

### A/B 评估模式

当用户要求“评估这个 skill”“迭代一次”“通过 A/B 测试”“证明新版更好”时启用。
启用后读取 `references/ab-evaluation-protocol.md`，并把比较对象明确成：

- `incumbent`：当前版本或不用 partner-skill 的 baseline
- `candidate`：本轮修改后的版本或使用 partner-skill 的版本

只有 candidate 通过 gate，才允许说“更好”。

## 角色池

角色详细映射放在 `references/role-routing-matrix.md`。
主文档只保留调度纪律：

- owner 只能有一个
- advisor 默认 0-2 个
- advisor 只补 owner 缺的层
- advisor 不得替 owner 拍板
- owner 必须说明采纳什么、不采纳什么、为什么

## 路由流程

1. 压缩用户问题
   - 目标
   - 约束
   - 成功标准
   - 当前未知点

2. 判断任务层级
   - `product-direction`
   - `external-research`
   - `technical-direction`
   - `implementation`
   - `operations-control`
   - `constraint-flow`
   - `medical-reliability`
   - `mixed`

3. 选择 owner
   - 按最终拍板责任选 owner
   - 不要让多个角色平权发言
   - mixed 任务按“最后谁负责结果”选 owner

4. 选择 advisors
   - 只选能修正盲点的角色
   - 默认不超过 2 个
   - 不为了热闹而增加角色

5. 形成 Brain 判断
   - owner 先给主判断、切入点、优先问题
   - advisors 分别给有边界的补充
   - owner 综合后拍板

6. 形成 Hands 契约
   - 需要执行时，把动作写成标准任务契约
   - 工具细节不直接暴露给 Brain
   - 重试、权限、文件状态、失败码属于执行层

7. Review 收口
   - 事实证据
   - 已做验证
   - blocker
   - 残余风险
   - 下一步

## 输出格式

协调模式至少输出：

```markdown
Owner: <role>
Advisors: <0-2 roles>

Brain:
- 目标:
- 事实:
- 假设:
- 风险:
- 推荐路径:

Action:
- 下一步:
- 执行契约:
- 验证方式:

Review:
- 已验证:
- blocker:
- 残余风险:
```

认真执行模式额外输出：

- `Workstreams`
- `Round Status`
- `Verification`
- `Open Blockers`

A/B 评估模式额外输出：

- `Incumbent`
- `Candidate`
- `Test Set`
- `Win/Loss Table`
- `Gate Decision`

## 冲突处理

冲突规则放在 `references/conflict-resolution.md`。
默认优先级：

1. 代码、日志、测试、数据等直接证据
2. 业务和行业事实
3. 安全与可靠性风险
4. 系统级 flow 和控制回路
5. 产品优先级与风格判断

没有硬性 veto 时，由 owner 拍板。

## 参考文件导航

- `references/manager-agent-protocol.md`
  - 需要 Brain / Hands 分离、执行契约、异步状态、重试、权限和观测指标时读
- `references/role-routing-matrix.md`
  - 需要选择 owner/advisors 时读
- `references/serious-execution-protocol.md`
  - 需要执行重型任务闭环时读
- `references/serious-execution-templates.md`
  - 需要可直接套用的 round、verification、blocker 模板时读
- `references/conflict-resolution.md`
  - 需要处理角色冲突和 veto 时读
- `references/ab-evaluation-protocol.md`
  - 需要评估、迭代或 A/B 测试本 skill 或其他 skill 时读

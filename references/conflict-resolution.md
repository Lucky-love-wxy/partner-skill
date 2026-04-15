# Conflict Resolution

## 冲突优先级

当多个角色给出冲突意见时，按这个顺序判断：

1. 代码、日志、测试、数据等直接证据
2. 业务和行业事实
3. 安全与可靠性风险
4. 系统级 flow 和控制回路
5. 产品优先级与风格判断

## 特殊 veto

### Coding veto

如果抽象判断和真实代码/测试/数据矛盾，`Coding` 优先。

### Atul veto

如果某方案明显提升速度但损害医疗安全、handoff 稳定性或 humane 边界，`Atul Gawande` 优先。

### Goldratt veto

如果某方案提升局部效率但伤害整体 throughput / flow / buffer 设计，`Goldratt` 优先。

### Andy Grove veto

如果某方案是管理建议但没有指标、节奏、接口和反馈回路，`Andy Grove` 优先。

## Owner 拍板规则

没有硬性 veto 时，由 owner 拍板。

owner 必须明确：

- 采纳了什么
- 没采纳什么
- 为什么


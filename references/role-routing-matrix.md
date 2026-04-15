# Role Routing Matrix

## Owner 选择矩阵

| 任务类型 | 默认 owner | 常见 advisors |
|------|------|------|
| 产品方向、切口、优先级、结果定义 | Jobs | Kandle / Coding / Andy Grove |
| 外部调研、竞品、机制映射、真实业务数据 | Kandle | Goldratt / Atul / Jobs |
| 技术主线、控制层、基础设施、技术赔率 | Elon | Coding / Andy Grove |
| 代码、文件、实现、测试、验证 | Coding | Goldratt / Atul / Jobs |
| 运营系统、指标、控制回路、管理节奏 | Andy Grove | Goldratt / Coding |
| 队列、瓶颈、吞吐、优先级、buffer | Goldratt | Kandle / Coding / Atul |
| 医疗可靠性、handoff、checklist、异常规则 | Atul Gawande | Goldratt / Coding / Kandle |

## Mixed 任务判断规则

如果任务跨层很多，按“最终要拍板的那一层”选 owner。

例如：

- 问“这个产品先打哪一刀” -> `Jobs`
- 问“这套门诊规则怎么设计才能不堵” -> `Goldratt`
- 问“这套医疗异常规则怎么既可靠又能落地” -> `Atul Gawande`
- 问“这个仓库怎么改到真能过 CI 和 review” -> `Coding`

## Advisor 使用纪律

- 默认 0-2 个 advisor
- 只补盲点
- 不得替 owner 拍板
- 顾问输出必须限定在自己的专长范围内


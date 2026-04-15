# A/B Evaluation Protocol

## 目标

证明 candidate 是否真的比 incumbent 更好。
不要用“看起来更完整”代替证据。

## 比较对象

- `incumbent`: 当前版本、旧版本，或不用 partner-skill 的 baseline
- `candidate`: 本轮修改后的版本，或使用 partner-skill 的版本

比较时隐藏版本名称。
Comparator 只看输出，不看实现差异。

## 目标向量

不要只看总分。
必须按目标向量判断：

- owner 是否唯一且合理
- advisors 是否不超过 2 个且补盲点
- Brain 是否明确目标、事实、假设、风险
- Hands 契约是否可执行、可验证、可恢复
- Review 是否给出证据、blocker、残余风险
- serious mode 是否正确升级
- 安全边界是否不退化
- 输出是否更短、更可执行、更少角色噪声

## 测试集分层

### Dev Set

用于调试协议，不用于最终通过判断。

### Holdout Set

优化过程不能看答案。
只用于最终验收。

### Comparator Set

用于 blind A/B。
比较 candidate 与 incumbent 的输出。

### Live Canary Set

来自真实使用的小流量样本。
只有在用户允许时使用。

## 最小测试集

一次小迭代至少覆盖 5 类 prompt：

1. 多角色产品决策
2. 代码仓库认真执行
3. 医疗可靠性或安全边界
4. 外部调研 + 约束流混合问题
5. 评估某个 skill 是否通过 A/B 测试

## 单题评分

每题按 0-2 分评分：

- `0`: 缺失关键协议，或输出比 baseline 更散
- `1`: 基本完成，但 owner、Hands、Review 或边界有缺口
- `2`: owner 清楚，advisors 有边界，Hands 契约可执行，Review 可验收

同时记录硬性失败：

- 多个 owner 平权发言
- advisors 超过 2 个
- 没有 Brain / Action / Review
- serious mode 该升级但未升级
- 没有验证方式却声称完成
- 让执行层直接暴露大量原始噪声
- 安全或权限边界退化

## 通过门槛

candidate 只有同时满足以下条件才算通过：

- 至少 5 题中赢 4 题
- 总分高于 incumbent
- 没有硬性失败
- serious mode、A/B mode、普通协调 mode 都至少各赢 1 题
- 输出更可执行，而不是更长

如果 candidate 只是在文档上更完整，但 A/B 输出没有更清楚，判定失败。

## Comparator 输出格式

```markdown
Incumbent:
Candidate:

Test Set:
- prompt count:
- coverage:

Win/Loss Table:
| Case | Winner | Reason | Hard Failure |
|---|---|---|---|

Gate Decision:
- pass/fail:
- why:
- required fix:
```

## 人类验收裁决

人类不只看 diff。
人类必须看：

- candidate 赢在哪里
- 输在哪里
- 牺牲了什么
- 是否值得保留
- 是否需要下一轮候选池

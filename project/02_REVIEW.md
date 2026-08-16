# Review 生命周期

## 1. Scope

Review 是值得持续关注、需要通过后续训练继续验证的长期诊断。

Review 只使用：

```text
KNOWLEDGE
SKILL
```

状态只使用：

```text
ACTIVE
RESOLVED
```

单次 Training Log 中的 Issue 是 observation；Review 是跨训练的 diagnosis。二者不做机械一一映射。

## 2. Create Review

默认保守创建。

一次偶然错误通常只保留在 Training Log。只有多条训练对同一个底层问题形成重复、一致的证据时，才创建 Review。

多个 Issue 如果指向同一个底层问题，应综合为一个 Review，而不是按 Issue 分别创建。

单次训练可以直接创建 Review，但只限问题足够明确且严重，例如：

- 关键基础知识明显缺失；
- 某项技能严重阻碍训练完成或得分。

不使用固定次数、分数或置信度阈值。

创建时：

- `Name` 描述具体、可观察、可干预的问题；
- `Type = KNOWLEDGE`：概念、定理、公式、结构或适用条件本身存在缺口；
- `Type = SKILL`：知识基本具备，但识别、执行、速度、时间策略或检查表现不稳定；
- `Status = ACTIVE`；
- 将形成判断的 Training Log 加入 `Evidence`；
- 设置 `First Detected` 和 `Last Updated`。

## 3. Update Review

每完成一次 Training Log，对相关 Review 判断：

1. 是否进一步支持已有问题；
2. 是否削弱已有判断或显示改善；
3. 是否已有足够证据可以解决；
4. 已解决的问题是否复发；
5. 是否形成新的长期 Review。

如果本次训练对某个 Review 有实际诊断价值：

- 将 Training Log 加入 `Evidence`；
- 更新 `Last Updated`；
- 必要时更新 Review 页面正文。

同一 Topic 但没有新增诊断价值时，不需要建立 relation。

改善中的 Review 仍保持 `ACTIVE`，直到有足够后续证据支持 `RESOLVED`；不增加中间状态。

## 4. Resolve and Reactivate

### Resolve

`ACTIVE → RESOLVED` 表示后续训练已经显示问题稳定改善，不再值得作为当前主要问题持续关注。

一次正常表现不足以 Resolve。应根据后续相关训练的整体表现判断，不要求固定训练次数。

Resolve 时：

- `Status = RESOLVED`；
- `Last Updated` 使用最近一次有效 Evidence 的日期；
- 在页面正文记录解决依据。

### Reactivate

如果后续训练再次明显出现相同底层问题：

```text
RESOLVED → ACTIVE
```

将新 Training Log 加入 `Evidence`，更新 `Last Updated`，并在正文记录复发。

`First Detected` 保留最初形成 Review 的日期，不重置。

## 5. Evidence

`Evidence` 只关联对 Review 判断有实际价值的 Training Log，可以包括：

- 支持问题存在的训练；
- 显示改善的训练；
- 支持解决的训练；
- 证明复发的训练。

Evidence 不等于只保存负面表现。

## 6. Review Page Body

Review 页面正文保持简短：

```text
## Current Assessment
当前判断。

## Evidence
为什么形成或维持这个判断。

## Next Focus
下一阶段训练重点观察什么。

## Progress
后续训练是否改善、解决或复发。
```

不要复制每条 Training Log 的完整复盘；具体训练通过 `Evidence` relation 回看。

## 7. Retrieval

长期学习状态以 Notion 中的 Review 为准：

- 当前主要问题 → `Status = ACTIVE`；
- 已解决问题 → `Status = RESOLVED`；
- 某知识模块 → 按 Topics 查询 Review，并结合相关 Evidence；
- 具体某次或近期训练表现 → 查询 Training Log，而不是强行通过 Review 回答。

Review 用于长期诊断；Training Log 用于具体训练表现。

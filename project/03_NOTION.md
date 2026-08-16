# Notion 持久化

## 1. Scope

Notion 是一试学习记录的 durable source of truth。

只使用两个 Database：

```text
Training Log
Review
```

两个 Database 放在 Notion 页面 `一试教练` 下。

不建立单题、Session、Exam、Attempt、错题或训练计划数据库。

本文件只定义持久化规则；Review 的创建、更新和解决判断由后续 `02_REVIEW.md` 定义。

## 2. Training Log

每次已经完成的训练创建一条 Training Log。

训练类型只有：

```text
FILL_SET
CALC_SET
PRACTICE
```

最小属性：

| Property | Notion Type | Purpose |
|---|---|---|
| Name | TITLE | 自动生成训练标题 |
| Date | DATE | 训练日期 |
| Type | SELECT | `FILL_SET` / `CALC_SET` / `PRACTICE` |
| Source | RICH_TEXT | 试卷来源或练习名称 |
| Topics | MULTI_SELECT | 本次值得检索的知识模块 |
| Issues | MULTI_SELECT | 本次实际暴露的问题 |
| Review | RELATION | 关联长期 Review，可为空 |

`Issues` 只使用：

```text
KNOWLEDGE
RECOGNITION
SPEED
EXECUTION
TIME_STRATEGY
CHECKING
```

详细判卷结果、逐题分析和总体结论写入页面正文，不继续拆成数据库字段。

## 3. Review

Review Database 保存值得长期关注的诊断。

最小属性：

| Property | Notion Type | Purpose |
|---|---|---|
| Name | TITLE | 可干预、可验证的问题名称 |
| Status | SELECT | `ACTIVE` / `RESOLVED` |
| Type | SELECT | `KNOWLEDGE` / `SKILL` |
| Topics | MULTI_SELECT | 涉及知识模块 |
| Evidence | RELATION | 与该诊断生命周期有关的 Training Log |
| First Detected | DATE | 首次形成该 Review 的日期 |
| Last Updated | DATE | 最近一次有效证据日期 |

`Evidence` 不只包含支持问题存在的训练，也包含后续显示改善、支持解决或证明复发的训练。

Review 的当前判断、证据解释、下一步关注点和后续进展写入页面正文。

## 4. Relation

Training Log 与 Review 使用双向 relation：

```text
Training Log.Review
↔
Review.Evidence
```

一条 Training Log 可以不关联 Review，也可以关联多个 Review。

Review 的 Evidence 可以来自多条不同类型的 Training Log，并覆盖问题形成、改善、解决和复发的全过程。

## 5. Create Training Log

只有已经完成的训练才创建记录。

标题建议：

```text
YYYY-MM-DD｜<Source>｜填空
YYYY-MM-DD｜<Source>｜计算
YYYY-MM-DD｜<Source>｜练习
```

完整一试 `8 + 3` 创建两条记录：

```text
FILL_SET
CALC_SET
```

两条记录使用相同 Date 和 Source，不增加 Session 或 Exam 实体。

自由练习一次提交默认创建一条 `PRACTICE`，不按题拆分。

## 6. Page Body

Training Log 页面正文使用 `01_TRAINING.md` 生成的精炼复盘。

原则：

```text
structured metadata
+
training analysis text
```

正常题只保留必要结果；异常题和具有训练价值的问题才展开。

Review 页面正文的具体生成规则由 `02_REVIEW.md` 定义。

## 7. Read Rules

需要回答历史学习状态时，以 Notion 为依据。

常见读取方式：

- 最近整体表现：按 Date 查询 Training Log；
- 最近填空表现：`Type = FILL_SET`；
- 最近计算表现：`Type = CALC_SET`；
- 自由练习历史：`Type = PRACTICE`；
- 某知识模块：按 Topics 查询相关 Training Log 和 Review；
- 长期问题：查询 Review，优先 `Status = ACTIVE`。

不要仅根据聊天上下文断言历史学习状态。

## 8. Write Rules

### Training

完成一次训练：

```text
create Training Log
```

询问历史、请求建议或讨论计划：

```text
no Training Log write
```

### Review

Training Log 可以先独立保存。

只有 `02_REVIEW.md` 的判断规则确认需要长期 Review 时，才创建或更新 Review，并建立 relation。

后续与 Review 有关的训练，无论是支持问题存在、显示改善、支持解决还是证明复发，都可以继续关联到同一个 Review。

## 9. Minimality

v1 不增加以下属性：

```text
Problem ID
Attempt ID
Session ID
Exam ID
Question Count
Score
Accuracy
Duration
Difficulty
Training Status
```

这些信息若对单次复盘有价值，优先写入页面正文。

只有实际检索需求无法由现有字段解决时，才通过后续 PR 修改 schema。

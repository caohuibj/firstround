# Notion 持久化

## 1. Scope

Notion 是一试学习记录的 durable source of truth。

`一试教练` 页面下只使用两个 Database：

```text
Training Log
Review
```

本文件只定义如何保存和读取这些数据。训练分析看 `01_TRAINING.md`；Review 判断看 `02_REVIEW.md`。

## 2. Training Log

| Property | Notion Type | Purpose |
|---|---|---|
| Name | TITLE | 训练标题 |
| Date | DATE | 训练日期 |
| Type | SELECT | `FILL_SET` / `CALC_SET` / `PRACTICE` |
| Source | RICH_TEXT | 试卷来源或练习名称 |
| Topics | MULTI_SELECT | 可检索的知识模块 |
| Issues | MULTI_SELECT | 本次训练暴露的问题 |
| Review | RELATION | 关联长期 Review，可为空 |

`Issues` 的允许值由 `01_TRAINING.md` 定义。

详细判卷结果和复盘写入 Training Log 页面正文，不拆成更多数据库字段。

## 3. Review

| Property | Notion Type | Purpose |
|---|---|---|
| Name | TITLE | 长期问题名称 |
| Status | SELECT | `ACTIVE` / `RESOLVED` |
| Type | SELECT | `KNOWLEDGE` / `SKILL` |
| Topics | MULTI_SELECT | 涉及知识模块 |
| Evidence | RELATION | 与该 Review 判断有关的 Training Log |
| First Detected | DATE | 首次形成 Review 的日期 |
| Last Updated | DATE | 最近一次有效证据日期 |

Review 页面正文由 `02_REVIEW.md` 定义。

## 4. Relation

Training Log 与 Review 使用双向 relation：

```text
Training Log.Review
↔
Review.Evidence
```

只关联对 Review 判断有实际价值的 Training Log。

## 5. Write

完成训练后按 `00_PROJECT.md` 的训练单元创建 Training Log：

- 8 个填空 → 1 条 `FILL_SET`；
- 3 个计算题 → 1 条 `CALC_SET`；
- 一次自由练习提交 → 1 条 `PRACTICE`；
- 完整一试 `8 + 3` → 1 条 `FILL_SET` + 1 条 `CALC_SET`。

Review 的创建、更新、解决和重新激活由 `02_REVIEW.md` 决定。

纯历史查询、建议或计划讨论不创建 Training Log。

## 6. Read

历史学习状态以 Notion 为依据：

- 具体训练表现 → 查询 Training Log；
- 长期主要问题 → 查询 `Status = ACTIVE` 的 Review；
- 已解决问题 → 查询 `Status = RESOLVED` 的 Review；
- 某知识模块 → 按 Topics 查询相关 Training Log 和 Review。

## 7. Schema Changes

只有真实持久化或检索需求无法由当前两个 Database 解决时，才修改 schema。

# 一试教练 Project

## 1. Purpose

本 Project 用于高联一试训练、复盘和长期 Review。

核心目标只有两个：

1. 解释这次训练为什么丢分或耗时；
2. 找出值得长期关注的问题，并用后续训练验证是否改善。

## 2. Core Model

训练只使用：

```text
FILL_SET
CALC_SET
PRACTICE
```

Review 只使用：

```text
KNOWLEDGE
SKILL
```

Review 状态只使用：

```text
ACTIVE
RESOLVED
```

## 3. Runtime Rules

- 8 个填空形成一条 `FILL_SET`。
- 3 个计算题形成一条 `CALC_SET`。
- 一次提交的自由练习默认形成一条 `PRACTICE`，不按单题拆分。
- 完整一试 `8 + 3` 作为一次分析输入，但持久化为 `FILL_SET + CALC_SET` 两条记录。
- 只有已经完成的训练才形成 Training Log。
- 正常题压缩，异常题展开。
- 单次 Issue 是观察；Review 是长期诊断，默认保守创建。

不建立单题、Session、Exam、Attempt 等额外实体。

## 4. Runtime Sources

### Project Files

Project Files 是 ChatGPT 在本 Project 中执行训练复盘、Review 判断和 Notion 操作的运行规则。

按职责读取：

- `00_PROJECT.md`：范围、架构和核心 invariant；
- `01_TRAINING.md`：训练分析与输出；
- `02_REVIEW.md`：Review 创建、更新、解决和检索；
- `03_NOTION.md`：Notion 持久化与读取。

### Notion

Notion 是一试学习记录的 durable source of truth。

历史表现、已有 Review 和 Review 状态应以 Notion 记录为依据，不仅依赖聊天上下文。

### GitHub

GitHub 只管理 Project Files、contracts 和规则变更。

## 5. Design Principle

保持最小模型。只有真实训练或检索需求无法由现有结构解决时，才增加字段、状态或数据库。

# 一试教练 Project

## 1. Purpose

本 Project 用于高联一试训练、复盘和长期 Review。

核心目标不是建立题库，而是持续回答两个问题：

1. 这次训练为什么丢分或耗时？
2. 哪些问题已经值得长期关注，后来是否真正改善？

## 2. Supported Work

Project 只处理四类核心任务。

### FILL_SET

一试第一部分：8 个填空题。

一次完整的 8 题训练视为一条训练记录。

### CALC_SET

一试第二部分：3 个计算题。

一次完整的 3 题训练视为一条训练记录。

### PRACTICE

自由练习。

可以是一题，也可以是用户一次提交的一组题，例如：

- 一道单独练习题；
- 解析几何计算专项；
- 三角恒等变换专项；
- 若干混合练习题。

一次提交的自由练习默认视为一条训练记录，不拆成单题记录，也不要求这些题属于同一知识点或训练目标。

### REVIEW

Review 表示已经值得持续关注的长期诊断，只分两类：

- `KNOWLEDGE`：知识模块问题；
- `SKILL`：方法、识别、计算、速度、时间策略、检查等技能问题。

Review 不是一次训练，也不是一次偶然错误。

## 3. Full Exam

如果用户一次提交完整一试：

- 8 个填空；
- 3 个计算题；

则作为一次分析输入，但拆成两条训练记录：

- `FILL_SET`；
- `CALC_SET`。

不建立额外 Session 或 Exam 实体。

## 4. Operating Model

### Project Files

Project Files 定义训练分析、Review 判断和 Notion 操作规则，是当前运行规则。

### Notion

Notion 是一试学习记录的 durable source of truth。

历史学习状态、已有 Review、Review 是否已解决等问题，应以 Notion 中的记录为依据。

### GitHub

GitHub 管理 Project Files、contracts 和规则变更。

规则调整通过小 PR 演进，不在运行过程中临时扩展数据模型。

## 5. Write Principle

只有已经完成的训练才形成 Training Log。

以下行为本身不创建训练记录：

- 询问历史表现；
- 请求解释某个 Review；
- 请求下一步练习建议；
- 讨论训练计划但尚未完成训练。

## 6. Design Principles

1. **训练记录按训练单元，不按单题。**
2. **正常题压缩，异常题展开。**
3. **单次 Issue 是观察，Review 是长期诊断。**
4. **Review 保守创建。** 偶然错误默认不升级为长期问题。
5. **优先保留有复用价值的文字复盘。**
6. **不预先增加数据库或状态。** 只有真实使用问题无法由现有模型解决时才扩展。

## 7. Minimal Data Model

训练只存在三种类型：

```text
FILL_SET
CALC_SET
PRACTICE
```

Review 只存在两种类型：

```text
KNOWLEDGE
SKILL
```

Review 生命周期只使用：

```text
ACTIVE
RESOLVED
```

具体 Notion 字段和持久化规则由 `03_NOTION.md` 定义。
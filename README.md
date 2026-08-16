# First Round Tutor

高联一试学习辅导 Project。

核心范围只有四项：

1. 第一部分：8 个填空（`FILL_SET`）
2. 第二部分：3 个计算题（`CALC_SET`）
3. 自由练习（`PRACTICE`）
4. Review：长期值得持续关注的知识模块或方法技能（`KNOWLEDGE` / `SKILL`）

## Architecture

- **ChatGPT Project Files**：训练复盘与 Review 的运行规则
- **Notion**：一试学习记录的 durable source of truth
- **GitHub**：Project Files、contracts 与后续变更的版本管理

系统保持最小化：不建立单题题库、Session、Attempt、复杂统计或预防性工程抽象。

## Development

功能按小 PR 演进：

1. Project Core
2. Notion Storage
3. Review

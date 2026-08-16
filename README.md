# First Round Tutor

高联一试学习辅导 ChatGPT Project。

核心范围只有四项：

1. 第一部分：8 个填空（`FILL_SET`）
2. 第二部分：3 个计算题（`CALC_SET`）
3. 自由练习（`PRACTICE`）
4. Review：长期值得持续关注的知识模块或方法技能（`KNOWLEDGE` / `SKILL`）

## Architecture

- **ChatGPT Project Files**：训练复盘与 Review 的运行规则
- **Notion**：一试学习记录的 durable source of truth
- **GitHub**：Project Files、contracts 与规则变更的版本管理

系统保持最小化：不建立单题题库、Session、Attempt、复杂统计或预防性工程抽象。

## ChatGPT Project Setup

### Project Instructions

在 ChatGPT Project Settings 中使用以下最小 instructions：

```text
只处理高联一试学习辅导。
以 00_PROJECT.md 为运行入口，并按其中职责使用 01_TRAINING.md、02_REVIEW.md、03_NOTION.md。
训练复盘按 Project Files 执行；历史学习状态和 Review 以 Notion 为准。
不要自行扩展数据库、状态或统计模型。
```

### Project Files

上传以下四个文件作为 Project Files：

```text
project/00_PROJECT.md
project/01_TRAINING.md
project/02_REVIEW.md
project/03_NOTION.md
```

不要把 `README.md` 或 `contracts/` 作为运行时 Project Files；它们用于部署说明和版本维护。

### Notion

确保 Notion 已在 ChatGPT 中连接，并可由本 Project 的聊天访问页面 `一试教练` 下的两个 Database：

```text
Training Log
Review
```

Database 结构以 `contracts/` 和 `project/03_NOTION.md` 为准。

GitHub 只作为规则版本源，不要求每次训练时读取仓库。

## Acceptance Checks

部署后至少验证：

1. 提交完整 8 个填空 → 形成 1 条 `FILL_SET`。
2. 提交完整 3 个计算题 → 形成 1 条 `CALC_SET`。
3. 提交完整一试 `8 + 3` → 形成 1 条 `FILL_SET` + 1 条 `CALC_SET`，不创建 Session / Exam。
4. 提交一次自由练习批次 → 形成 1 条 `PRACTICE`，不按单题拆分。
5. 单次偶然错误 → 记录 Training Issue，但默认不创建 Review。
6. 多次一致的底层问题 → 可以形成 `KNOWLEDGE` 或 `SKILL` Review。
7. 后续稳定改善 → `ACTIVE → RESOLVED`。
8. 已解决问题明显复发 → `RESOLVED → ACTIVE`，且不重置 `First Detected`。

## Repository Layout

```text
project/
├── 00_PROJECT.md
├── 01_TRAINING.md
├── 02_REVIEW.md
└── 03_NOTION.md

contracts/
├── training.schema.json
└── review.schema.json
```

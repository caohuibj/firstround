# Runtime Acceptance Scenarios

本文件用于在 ChatGPT Project 装配完成后做人工验收。

它不是 Project File，不参与运行时规则。

## 1. FILL_SET

输入：一次提交完整 8 个填空题及作答。

期望：

- 形成 1 条 `FILL_SET` Training Log；
- 正常题压缩，异常题展开；
- 本次问题只记录为 Training Issue，除非已经满足 Review 创建条件。

## 2. CALC_SET

输入：一次提交完整 3 个计算题及作答。

期望：

- 形成 1 条 `CALC_SET` Training Log；
- 优先定位第一处影响结果的关键问题；
- 能区分“不会”与“会做但没有兑现成得分”。

## 3. Full First Round

输入：一次提交完整一试 `8 + 3`。

期望：

- 统一读取和分析；
- 持久化为 1 条 `FILL_SET` + 1 条 `CALC_SET`；
- 不创建 Session / Exam / Attempt。

## 4. PRACTICE

输入：一次提交 6 道解析几何练习题，或一组混合练习题。

期望：

- 形成 1 条 `PRACTICE`；
- 不按单题拆分；
- 只展开真正有训练价值的问题。

## 5. Accidental Error

前提：此前没有相关长期问题。

输入：一次训练中出现单个偶然计算错误。

期望：

- Training Log 可记录 `EXECUTION`；
- 默认不新建 Review。

## 6. Persistent Skill Issue

前提：已有多次训练显示同一底层问题，例如解析几何中持续出现识别慢、消元慢或执行不稳定。

期望：

- 综合形成一个 `SKILL` Review；
- 不按 `RECOGNITION` / `SPEED` / `EXECUTION` 分别创建多个 Review；
- 相关 Training Logs 进入 `Evidence`。

## 7. Clear Knowledge Gap

输入：一次训练明确暴露关键基础知识不会或适用条件缺失。

期望：

- 允许直接创建 `KNOWLEDGE` Review；
- `Status = ACTIVE`；
- 设置 `First Detected` 和 `Last Updated`。

## 8. Resolve and Reactivate

前提：已有一个 `ACTIVE` Review。

输入 A：后续多次相关训练表现稳定正常。

期望 A：

- `ACTIVE → RESOLVED`；
- 改善和解决训练仍保留在 `Evidence`。

输入 B：之后同一底层问题明显复发。

期望 B：

- 同一个 Review `RESOLVED → ACTIVE`；
- 新训练加入 `Evidence`；
- `First Detected` 不重置；
- 不创建重复 Review。

## 9. Historical Queries

输入：

- “我最近有什么主要问题？”
- “哪些问题已经好了？”
- “解析几何最近怎么样？”
- “最近一次训练表现如何？”

期望：

- 当前长期问题查 `ACTIVE` Review；
- 已解决问题查 `RESOLVED` Review；
- 知识模块按 Topics 查相关 Review 和 Training Log；
- 具体训练表现优先查 Training Log；
- 查询本身不创建 Training Log 或 Review。

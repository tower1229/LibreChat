# 完成 Lesson 0005：一条消息的端到端 Trace

用户完成了第五课，理解 Agents 两阶段可恢复流（POST 启动 + GET SSE 订阅）、`TSubmission` / `useAdaptiveSSE` 角色，以及 `saveMessage` 在 final event 之前的落库顺序。

## Evidence

用户在对话中确认「完成了」。

## Implications

- Mission 核心 trace 能力已达成；可进入实操型课程。
- Lesson 0006 用真实小功能 `GET /api/banner` 作为只读 API 样板，教「按规范加一条新 API」的检查清单与文件顺序。
- 写操作（mutation + invalidate）在 0006 作附录对比即可，深度 DB 建模留到 Lesson 0007。

# Mission: LibreChat 深度二开

## Why

作为资深前端工程师，需要在 LibreChat 上进行深度二次开发——不仅能改 UI，还能安全地扩展 API、数据层和 Agent/MCP 能力。当前对 Node.js 有概念但缺乏实战经验，需要从宏观架构入手，逐步建立可独立交付全栈改动的能力。

## Success looks like

- 能画出 LibreChat 的 workspace 依赖图，并说明「新代码该写在哪、不该写在哪」
- 能独立 trace 一条用户消息从 `client` → `data-provider` → `api` → LLM/Agent 的完整链路
- 能按项目规范完成一个端到端功能（types + endpoint + data-service + React Query hook + UI）
- 能读懂并修改 `packages/api` 中的 TypeScript 后端逻辑，理解 MongoDB schema 与权限模型
- 能在本地跑通 dev 环境、写测试、通过 lint，并知道如何调试前后端问题

## Constraints

- 背景：资深前端（React/TS），Node.js 理论了解、无生产实战经验
- 学习节奏：一课一事，每课 20–40 分钟可完成
- 教学文件集中在 `docs/teach/`，不污染仓库根目录
- 优先走官方约定路径（`packages/api` 新后端、`data-provider` 共享层），避免在 legacy `/api` 里堆逻辑

## Out of scope

- 从零重写 LibreChat 或 fork 成完全不同的产品
- 深入 `@librechat/agents` 源码（外部仓库，后续按需选修）
- DevOps / K8s / Helm 生产部署细节（除非二开明确需要）
- 每个 LLM provider 的 API 差异（用到时再查）

# 学习者先验背景

用户是资深前端工程师，熟悉 React/TypeScript 生态（组件、状态、构建工具、性能优化）。对 Node.js 有概念性了解（事件循环、模块、Express 基本名词），但无生产级后端实战经验（路由分层、DB、鉴权、流式响应等需在 LibreChat 语境中从零建立肌肉记忆。

## Implications

- 前端侧（`client`、`packages/client`、React Query）可快读快练，不必从 React 基础教起。
- 第一课从 monorepo 地图入手，建立「代码该放哪」的全局模型，比直接跳进 chat 实现更合适。
- 后端相关课要刻意连接用户已有的 FE 经验（例如：data-provider ≈ 你们团队的 API client + types 包）。
- 避免在 legacy `/api` 里教「老式 Express 写法」；以 `packages/api` + 薄路由包装为样板。

# 完成 Lesson 0004：Express 后端入口

用户完成了第四课，能区分启动阶段与请求阶段，理解 `api/server/index.js` 的中间件链与 `app.use` 路由挂载，并用 `GET /api/config` 补全 trace 到 handler。

## Evidence

用户在对话中确认「学完了」。

## Implications

- 后端入口与前端契约层已能对接；Mission 中「trace 一条用户消息」的前置技能已具备。
- 可进入 Lesson 0005：以 Agents 聊天为主路径，讲清「提交 → POST 启动 → SSE 订阅 → 流式渲染 → saveMessage 落库」的两阶段可恢复流架构。
- Assistants 端点仍走 legacy 单连接 SSE（`useSSE`），课上作对比即可，不展开。

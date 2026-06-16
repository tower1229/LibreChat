# 完成 Lesson 0003：React Query Hook 层

用户完成了第三课，理解 `client/src/data-provider/` 与 `packages/data-provider` 的分工，能用 `useGetStartupConfig` 样本说明 QueryKey、queryFn、enabled 门控，并知道 mutation 后 invalidate 应使用共享 `QueryKeys`。

## Evidence

用户在对话中确认「0003 学完了」。

## Implications

- 前端数据链路（组件 → Hook → data-service → endpoints）已闭环。
- 可进入 Lesson 0004：后端入口 `api/server/index.js`——Express 启动顺序、全局中间件链、路由挂载。用同一 `GET /api/config` 样本补全 trace 的后半段。
- 用户对 Node/Express 无生产经验，第 4 课应强调「启动阶段 vs 请求阶段」两段时间线，避免把 `startServer` 里的初始化与 `app.use` 中间件混为一谈。

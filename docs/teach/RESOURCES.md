# LibreChat Resources

## Knowledge

- [CLAUDE.md](../../CLAUDE.md)
  项目权威概览：workspace 边界、代码风格、开发命令、测试哲学。每次开课前先扫 relevant 章节。
- [README.md](../../README.md) / [README.zh.md](../../README.zh.md)
  安装、环境变量、快速启动。Use for: 本地 dev 环境搭建。
- [AGENTS.md](../../AGENTS.md)
  指向 CLAUDE.md，Agent 协作约定。
- [packages/data-provider/src/api-endpoints.ts](../../packages/data-provider/src/api-endpoints.ts)
  前后端共享的 API 路径定义。Use for: 找 endpoint、理解路由命名。
- [packages/data-provider/src/data-service.ts](../../packages/data-provider/src/data-service.ts)
  前端调 API 的统一入口。Use for: 看某个功能如何请求后端。
- [packages/data-provider/src/keys.ts](../../packages/data-provider/src/keys.ts)
  React Query 的 QueryKey / MutationKey。Use for: 前端缓存与 invalidation。
- [api/server/index.js](../../api/server/index.js)
  Express 入口、中间件链、路由挂载。Use for: 后端启动流程与全局中间件。
- [api/server/routes/](../../api/server/routes/)
  Legacy JS 路由层（薄包装）。Use for: 找到具体 HTTP handler 入口。
- [packages/api/](../../packages/api/)
  新后端 TypeScript 代码所在地。Use for: 业务逻辑、服务、中间件实现。
- [packages/data-schemas/](../../packages/data-schemas/)
  MongoDB models/schemas。Use for: 数据结构与 DB 操作。
- [client/src/routes/index.tsx](../../client/src/routes/index.tsx)
  前端路由表。Use for: 页面结构与懒加载入口。
- [client/src/data-provider/](../../client/src/data-provider/)
  前端 React Query hooks 层。Use for: UI 如何订阅/变更服务端数据。

## Wisdom (Communities)

- [LibreChat GitHub Discussions](https://github.com/danny-avila/LibreChat/discussions)
  官方讨论区。Use for: 架构疑问、二开方案、升级迁移。
- [LibreChat Discord](https://discord.librechat.ai)
  实时社区。Use for: 快速答疑、看他人二开经验。

## Gaps

- 暂无系统性的「架构决策记录（ADR）」文档——需通过源码 + CLAUDE.md 自行归纳。
- `@librechat/agents` 源码不在本仓库，Agent 运行时细节需后续单独建资源条目。

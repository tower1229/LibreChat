# LibreChat Glossary

本工作区学习 LibreChat 二开时使用的规范术语。

## Terms

**Workspace**:
npm monorepo 中的一个子包（如 `client`、`api`、`packages/data-provider`），有独立 `package.json`，由根 `package.json` 的 `workspaces` 字段管理。
_Avoid_: 模块、文件夹（当指 monorepo 包时）

**data-provider**:
前后端共享包，存放 API 类型、endpoint 常量、`data-service` 请求函数。二开时「契约层」的第一站。
_Avoid_: API 层、client SDK（泛指时）

**Legacy api**:
仓库根目录 `/api`，JavaScript Express 服务。新逻辑应写入 `packages/api`，此处只保留薄路由包装。
_Avoid_: 后端（当泛指整个服务端时）

**packages/api**:
TypeScript 后端业务代码所在地，被 legacy `/api` import 并调用。
_Avoid_: 新 api、api v2

**api-endpoints**:
`packages/data-provider/src/api-endpoints.ts`。纯函数，负责拼 REST URL（含 query）。二开加新 API 时第二站（第一站是 types）。
_Avoid_: 路由定义（那是 Express 侧的事）

**data-service**:
`packages/data-provider/src/data-service.ts`。每个导出函数对应一个 API 调用，内部组合 `endpoints` + `request`。
_Avoid_: React Query hook（那是 client 层）

**client data-provider**:
`client/src/data-provider/`。前端 React Query 适配层：`useQuery` / `useMutation` hooks 包装 `dataService`，组件通过 `~/data-provider` import。与 `packages/data-provider` 同名不同层。
_Avoid_: 与共享契约包混为一谈

**QueryKeys**:
`packages/data-provider/src/keys.ts` 中的枚举。React Query 缓存主键，mutation 后 `invalidateQueries` 用同一套 key。
_Avoid_: 在 client 层手写字符串 key

**Trace（追踪）**:
从 UI hook 沿 data-service → endpoints → Express route → handler 逐文件跟读，验证你对一条 API 全链路的理解。二开基本功。
_Avoid_: 只看一端（只看前端或只看后端）

**Legacy api/server**:
`api/server/index.js` 为 Express 总入口：启动 MongoDB、注册全局中间件、`app.use` 挂载各 feature Router、SPA fallback、`ErrorController`。二开加路由时改 `routes/` + `index.js` 挂载行。
_Avoid_: 在 index.js 里写大段业务逻辑

**Router 挂载**:
`app.use('/api/xxx', middleware..., routes.xxx)` — URL 前缀与 `api-endpoints.ts` 对齐；`routes/xxx.js` 内 `router.get('/')` 对应 `GET /api/xxx`。
_Avoid_: 在 Router 里重复写完整 `/api/...` 路径（除非故意）

**serverReady**:
`index.js` 在 `listen` 回调里完成 MCP、migrations 后置为 `true`。此前 `POST /api/agents/chat` 返回 503，防止半初始化服务器处理聊天。
_Avoid_: 以为 listen 成功就等于所有子系统就绪

**TSubmission**:
`useChatFunctions.ask` 构建的提交对象，经 Recoil `submissionByIndex` 传给 SSE hook。含 `userMessage`、`endpointOption`、`conversation`、`initialResponse` 等。
_Avoid_: 与已落库的 `TMessage` 混淆

**Resumable SSE（可恢复流）**:
Agents 默认路径：`POST` 返回 `{ streamId }`，再 `GET /api/agents/chat/stream/:streamId` 订阅 SSE。生成由 `GenerationJobManager` 管理，与 HTTP 连接解耦。
_Avoid_: 与 Assistants 的单 POST 长连接 SSE 混为一谈

**GenerationJobManager**:
`packages/api` 中的流任务管理器：createJob、emitChunk、subscribe、completeJob。streamId 通常等于 conversationId。
_Avoid_: 在 route handler 里手写 res.write 而不经 JobManager（Agents 路径）

**契约先行**:
二开加 API 时先改 `packages/data-provider`（types → endpoints → data-service → keys），`npm run build:data-provider` 后再动后端路由与前端 hook。
_Avoid_: 先写 route 再补 types（易导致前后端字段漂移）

**data-schemas**:
MongoDB 层 workspace：`schema/`（Mongoose 定义）→ `models/`（注册 Model + tenantIsolation）→ `methods/`（createXxxMethods 工厂）。legacy 通过 `~/models` = `createMethods(mongoose)` 导出。
_Avoid_: 在 route 里直接写 Mongoose 查询

**IMessage vs TMessage**:
`IMessage` 在 data-schemas（DB 文档）；`TMessage` 在 data-provider（API/UI 契约）。字段相近，职责不同。
_Avoid_: 在 data-provider 里定义 Mongo-only 字段

**tenantIsolation**:
Model 注册时对 Schema 调用 `applyTenantIsolation`，查询/更新自动带 `tenantId`。系统任务用 `runAsSystem()`。
_Avoid_: 在 handler 里手动拼 tenant filter 绕过插件

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

**Trace（追踪）**:
从 UI hook 沿 data-service → endpoints → Express route → handler 逐文件跟读，验证你对一条 API 全链路的理解。二开基本功。
_Avoid_: 只看一端（只看前端或只看后端）

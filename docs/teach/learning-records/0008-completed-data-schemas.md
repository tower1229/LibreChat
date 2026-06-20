# 完成 Lesson 0007：data-schemas 与 MongoDB

用户完成了第七课，理解 schema → model → methods 三层结构、`~/models` 注入方式、`applyTenantIsolation` 与 `createModels` 启动顺序，并能区分 `IMessage`/`IBanner` 与 data-provider 契约类型的职责。

## Evidence

用户在对话中确认「已完成 0007」。

## Implications

- DB 层读写路径清晰；简单 CRUD 可在 methods 完成，复杂逻辑可注入 deps。
- 租户隔离在 model 层注册，与请求侧 `tenantContextMiddleware` 配对——下一课串联鉴权与权限。
- 可进入 Lesson 0008：JWT 鉴权、RBAC（PermissionTypes）、SystemCapabilities、前后端权限镜像。

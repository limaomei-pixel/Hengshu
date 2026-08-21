# Hengshu v1.0.0.45

## 这版新增

- 分享包新增 `distribution/Hengshu-Subagent-Test-Prompt.txt`，是一份与用户当前模型、推理强度和服务等级无关的统一测试话术。
- 话术覆盖 Commander、Architect、Researcher、Scout、Analyst、Operator、Builder、Toolsmith、Integrator、Validator、Challenger、Reviewer。
- 话术要求严格区分 `requested`、`observed`、`unknown`；没有 Codex 原生运行时直接证据时，必须返回 `UNKNOWN_RUNTIME`，不允许猜测模型或推理强度。
- 安装器在安装完成后把话术部署到 `%CODEX_HOME%\\hengshu\\Hengshu-Subagent-Test-Prompt.txt`，并打印安装后测试提醒；安装收据同时记录路径和 SHA-256。
- 卸载器只在文件仍位于 Hengshu 目录且哈希未被用户修改时删除话术，用户改过的文件会保留并告警。

## 使用方式

1. 从本 Release 下载 `Hengshu-1.0.0.45-x64-share.zip` 并完整解压。
2. 运行 `安装衡枢.cmd`，完成安装后读取 `%CODEX_HOME%\\hengshu\\Hengshu-Subagent-Test-Prompt.txt`。
3. 新建一个 Codex 任务，把话术全文原样发送给每个实际启动的子智能体；不要把界面下拉框的请求值冒充运行时观测值。
4. 只接受子智能体直接回显的运行时字段。缺少 `model` 或 `reasoning_effort` 时，记录 `UNKNOWN_RUNTIME`，并把该项标为未验证。

## 验证

- 核心测试：`209/209` 通过。
- Release CLI 构建：`0` 警告、`0` 错误。
- 签名 MSIX：`1.0.0.45`，SHA-256 `AB0C2C30579321CDEA0FC3E18AF436BC4F9C0D93C675F210461A1BA79C1E7C32`。
- 分享包：38 个文件，禁止文件计数 `0`，SHA-256 `0DF9279161242DAD191A447F78FEFFB47A912960C6A60B8E247EDBFD11B9B7E7`。
- 测试话术：5,520 bytes，SHA-256 `8E0AE5E0517961223B50E7E24459117790E0D55D30D5757B94CB7587E0CFC8AB`。
- 已安装态 WinUI 回归：宽、中、窄三种布局通过，12 个角色和 36 个路由组合框存在；请求监控/悬浮层入口计数为 `0`。

## 运行时边界

Hengshu 的 Commander/主大脑仍是当前 Codex 根任务；对话框选择的模型和推理强度属于当前任务选择。角色路由中的模型、推理强度和权限是请求配置，不等于原生运行时已经采用。Hengshu 不扩大账号权限、平台并发、服务等级或额度，也不注入 Codex 主程序。

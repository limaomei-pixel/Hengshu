# v1.0.0.45 验证摘要

本页描述不含请求监控和悬浮层的 Hengshu `1.0.0.45`。历史 `v1.0.0.44` 和 `v1.0.0.43` Release 保留不变。

## 分享包

| 项目 | 观察值 |
| --- | --- |
| 文件 | `Hengshu-1.0.0.45-x64-share.zip` |
| 大小 | `137136331` bytes |
| SHA-256 | `0DF9279161242DAD191A447F78FEFFB47A912960C6A60B8E247EDBFD11B9B7E7` |
| 文件数 | `38` |
| 文件树 SHA-256 | `7D0416273E4FFFC09B39458871F0DD21BBC6409DC84F58229D2E702169D3FBAD` |
| 禁止文件数 | `0` |

分享包 ZIP 完整性检查：通过；包含发布清单、逐文件 `SHA256SUMS.txt`、CLI、Skill、11 个 Agent TOML、x64 Windows App Runtime、安装/卸载脚本和通用测试话术。

## 通用子智能体测试话术

| 项目 | 观察值 |
| --- | --- |
| 文件 | `Hengshu-Subagent-Test-Prompt.txt`（分享包内为同名文件） |
| 大小 | `5520` bytes |
| SHA-256 | `8E0AE5E0517961223B50E7E24459117790E0D55D30D5757B94CB7587E0CFC8AB` |
| 覆盖角色 | Commander、Architect、Researcher、Scout、Analyst、Operator、Builder、Toolsmith、Integrator、Validator、Challenger、Reviewer |

话术不写死模型、推理强度或服务等级。用户只需把文件全文原样发给实际启动的子智能体；子智能体必须分开报告 `requested`、`observed`、`unknown`。如果当前 Codex 原生界面或工具没有直接回显 `model`/`reasoning_effort`，验收结论必须是 `UNKNOWN_RUNTIME`，而不是把请求配置当成观测值。

## MSIX 与版本契约

| 项目 | 观察值 |
| --- | --- |
| MSIX | `Hengshu_1.0.0.45_x64.msix` |
| MSIX SHA-256 | `AB0C2C30579321CDEA0FC3E18AF436BC4F9C0D93C675F210461A1BA79C1E7C32` |
| 包版本 | `1.0.0.45` |
| 架构 | `x64` |
| 发布者 | `CN=Hengshu Test` |
| 签名验证 | 通过 |
| 版本契约 | 通过 |
| 版本契约负例 | `23` |

## 已安装态 WinUI 回归

结果：`success=true`，版本 `1.0.0.45`，窗口标题“衡枢 Hengshu”，应用可响应。

- 三种布局：`1280×820`、`1024×760`、`560×760`。
- 每种布局均观察到 12 个角色、36 个路由组合框和 3 个预算数字框。
- 每种布局恰有 Commander 的 3 个路由组合框被禁用。
- 已移除的请求/观察监控和悬浮层入口计数为 `0`。
- “恢复推荐角色路由”调用成功并显示确认信息；“保存角色路由”按钮存在。
- 安装收据状态为 `Ok`，测试话术实际部署到 `%CODEX_HOME%\hengshu\Hengshu-Subagent-Test-Prompt.txt`，收据哈希与文件哈希一致；安装器源码包含完成后的测试提醒。

## 复杂度、档位和预算

使用候选 CLI 的 5 个计划案例：

| 案例 | 档位 | 复杂度 | 计划 Agent 数 | 执行是否已开始 |
| --- | --- | --- | ---: | --- |
| auto-medium | auto | medium | 3 | `false` |
| fast-medium | fast | medium | 2 | `false` |
| standard-medium | standard | medium | 3 | `false` |
| deep-medium | deep | medium | 5 | `false` |
| deep-complex | deep | complex | 7 | `false` |

中文长任务的低置信度升级、调度预算和一次性 `native-dispatch-request` 回执均由核心测试覆盖。回执明确写出：CLI 不启动原生子智能体，也不提供持续监控。

## 角色配置

分享包和安装态均有 11 个角色：`analyst`、`architect`、`builder`、`challenger`、`integrator`、`operator`、`researcher`、`reviewer`、`scout`、`toolsmith`、`validator`。逐文件 SHA-256 与发布清单一致，角色提示包含受限 PowerShell 的标量优先降级和 requested/observed/unknown 边界。

这证明的是配置、安装和计划层完整性；当前 Codex 原生运行时没有为本次离线候选验收逐个回显实际 `model`/`reasoning_effort`，这些字段保持 `unknown`，不以请求值代替。

## 核心测试与安全边界

- 核心测试：`209/209` 通过，`0` 失败、`0` 跳过。
- Release 构建：`0` 警告、`0` 错误。
- 分享包 ZIP 完整性：38 个条目，`bad_entry=None`，必需文件和测试话术均存在。
- 分享包不含源码、测试、私钥、令牌、Cookie、密码或授权头。
- 未启用 Hook 信任绕过；未恢复请求监控、悬浮层或隐藏任务。

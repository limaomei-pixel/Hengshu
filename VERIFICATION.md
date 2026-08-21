# v1.0.0.44 验证摘要

本页描述不含请求监控和悬浮层的 Hengshu `1.0.0.44`。历史 `v1.0.0.43` Release 保留不变。

## 分享包

| 项目 | 观察值 |
| --- | --- |
| 文件 | `Hengshu-1.0.0.44-x64-share.zip` |
| 大小 | `137132947` bytes |
| SHA-256 | `00932924CB7D15786C36ED293A72200CEA7B3D42956068470279C13DC03CD497` |
| 文件数 | `37` |
| 文件树 SHA-256 | `C4B4A1B6636BD1596F0CD2E2EBE14FE209CA9F54C71FA7E6BEADD05246C909C0` |
| 禁止文件数 | `0` |

分享包 ZIP 完整性检查：通过；包含发布清单、逐文件 `SHA256SUMS.txt`、CLI、Skill、11 个 Agent TOML、x64 Windows App Runtime 和安装/卸载脚本。

## MSIX 与版本契约

| 项目 | 观察值 |
| --- | --- |
| MSIX | `Hengshu_1.0.0.44_x64.msix` |
| MSIX SHA-256 | `B30CBAE9C580B44978D4652E4A1F4CD5A3FF418A5F68E0FAB0AEF1FFBD6D36FE` |
| 包版本 | `1.0.0.44` |
| 架构 | `x64` |
| 发布者 | `CN=Hengshu Test` |
| 签名验证 | 通过 |
| 版本契约 | 通过 |
| 版本契约负例 | `23` |

## 已安装态 WinUI 回归

结果：`success=true`，版本 `1.0.0.44`，窗口标题“衡枢 Hengshu”，应用可响应。

- 三种布局：`1280×820`、`1024×760`、`560×760`。
- 每种布局均观察到 12 个角色、36 个路由组合框和 3 个预算数字框。
- 每种布局恰有 Commander 的 3 个路由组合框被禁用。
- 已移除的请求/观察监控和悬浮层入口计数为 `0`。
- “恢复推荐角色路由”调用成功并显示确认信息；“保存角色路由”按钮存在。

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

- 核心测试：`208/208` 通过，`0` 失败、`0` 跳过。
- Release 构建：`0` 警告、`0` 错误。
- 分享包不含源码、测试、私钥、令牌、Cookie、密码或授权头。
- 未启用 Hook 信任绕过；未恢复请求监控、悬浮层或隐藏任务。

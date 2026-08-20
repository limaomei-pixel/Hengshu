# v1.0.0.43 验证摘要

本页描述不含请求监控和悬浮层的 Hengshu `1.0.0.43`。历史 `v1.0.0.37` Release 保留不变；`1.0.0.38`–`1.0.0.42` 实验/修复候选未作为公开稳定版本发布。

## 分享包

| 项目 | 观察值 |
| --- | --- |
| 文件 | `Hengshu-1.0.0.43-x64-share.zip` |
| 大小 | `137136925` bytes |
| SHA-256 | `1A43B414C9C389547306C3959130CA8838C7B7850FFF7DE42B297F3EE690574D` |
| 文件数 | `37` |
| 文件树 SHA-256 | `E96F5DA2412FFC9560152427394EF8DAC140B71D45C63A3ABAF686DCFE910150` |
| 禁止文件数 | `0` |

分享包回执 SHA-256：`D5789A5AAE48819F96C6841CCDD441543E918E2D14F541B51682D0C5B47C7837`

## MSIX 与版本契约

| 项目 | 观察值 |
| --- | --- |
| MSIX | `Hengshu_1.0.0.43_x64.msix` |
| MSIX SHA-256 | `C0CF1A10CD4DA722EE30F57431224E20889127BF6BCEF2C75BEA1971F0C36F60` |
| 包版本 | `1.0.0.43` |
| 架构 | `x64` |
| 发布者 | `CN=Hengshu Test` |
| 签名验证 | 通过 |
| 版本契约 | 通过 |
| 版本契约负例 | `23` |

包回执 SHA-256：`03DEBA8C5EA88D7455C0F58318047E9D221BE1EEC24D043D291AAC66ED99D934`

## 已安装态 WinUI 回归

结果：`success=true`，版本 `1.0.0.43`，窗口标题“衡枢 Hengshu”，应用可响应。

- 三种布局：`1280×820`、`1024×760`、`560×760`。
- 每种布局均观察到 12 个职能角色、36 个组合框、3 个预算数字框。
- 每种布局恰有 Commander 的 3 个路由组合框被禁用。
- 独立请求/观察监控与悬浮层入口计数为 0。
- “恢复推荐角色路由”调用成功并显示确认信息。

WinUI 回归回执 SHA-256：`CFA058F31405AD7658E4CE32AD325F06CE5984FFE8B103362CB9A3FC221FDA09`

## 角色与子智能体

- Commander 是当前 Codex 根任务，不创建 `hengshu_commander` 子智能体；核心策略固定为 `auto/auto/auto/default`，旧版已保存的 Commander 固定路由会在读取时规范化为继承当前任务。
- 11 个原生类型 `hengshu_architect`、`hengshu_researcher`、`hengshu_scout`、`hengshu_analyst`、`hengshu_operator`、`hengshu_builder`、`hengshu_toolsmith`、`hengshu_integrator`、`hengshu_validator`、`hengshu_challenger`、`hengshu_reviewer` 均已实际创建并完成各自只读验收。
- 最终 `1.0.0.43` 分享包中的 11 个 Agent TOML 与实测配置哈希一致。

角色实测回执 SHA-256：`F76F00C47CC89E1DFB8EF6699135C3D80A90E0F10A2B138DDA11BCE7BDC78DEF`

## 供应链扫描

组件数 `9`，扫描发现 `0`。扫描回执 SHA-256：`2B8159358D6235440D8450F37FD9D0074A470384A6C13CE251CB151DF55989DE`

## 未验证或不作保证

- 子智能体类型确实已创建并运行，但当前原生控制面没有逐个回显其实际模型与推理强度；这些字段保持 `unknown`。
- 不保证用户账号拥有某个模型、服务等级、并发量或无限额度。
- 测试签名本地安装不等于 Microsoft Store 或生产代码签名发布。

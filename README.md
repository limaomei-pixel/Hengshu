# 衡枢 Hengshu

衡枢是面向 Windows 上 Codex 原生子智能体的设置中心与有边界调度计划器。它保存 11 个职能角色的模型、推理强度、速度偏好和调度预算，并在用户明确发送 `开启智能体：<完整任务>` 后生成波次计划；真正的子智能体仍由当前 Codex 任务通过原生能力启动和展示。

## 当前公开版本

**v1.0.0.45（Windows x64，测试签名）**。

本版明确不包含“打开请求/观察监控”、请求监控窗口或悬浮层，也不会在后台创建隐藏任务。主要改进：

- 复杂度判断改为结构化维度，并为中文低置信度长任务提供升级路径，不再依赖少数关键词。
- `auto`、`fast`、`standard`、`deep` 四档调度；每档都有并发/总量硬预算。
- 受限 PowerShell 使用标量优先的降级路径，复杂对象管道失败时会报告限制而不是伪造成功。
- 11 个角色配置精简为单一职责；任务结束只生成一次性验收摘要，区分 `requested`、`observed` 与 `unknown`。
- 随分享包提供与模型无关的《衡枢子智能体统一测试话术》，安装完成后自动部署并提醒用户测试。
- 测试话术覆盖 Commander、Architect、Researcher、Scout、Analyst、Operator、Builder、Toolsmith、Integrator、Validator、Challenger、Reviewer；没有原生运行时证据时必须返回 `UNKNOWN_RUNTIME`。

## 下载与安装

请从 [Releases](https://github.com/limaomei-pixel/Hengshu/releases) 下载 `Hengshu-1.0.0.45-x64-share.zip`。

1. 完整解压 ZIP，不要从压缩包预览窗口直接运行。
2. 双击 `安装衡枢.cmd`，接受管理员权限提示。
3. 安装器会核对主程序、运行库、证书和逐文件 SHA-256，然后创建桌面 `衡枢 Hengshu.lnk`。
4. 安装器会把统一测试话术复制到 `%CODEX_HOME%\hengshu\Hengshu-Subagent-Test-Prompt.txt`，并在安装完成时提醒测试。
5. 安装或升级 Skill/Agent 后，新建一个 Codex 任务；把上述文件的全文原样发送给每个实际启动的子智能体，再使用 `开启智能体：<完整任务>`。

测试话术不会假设用户当前选择的模型或推理强度。可直接审阅或复制仓库中的 [`Hengshu-Subagent-Test-Prompt.txt`](Hengshu-Subagent-Test-Prompt.txt)。它要求子智能体分别回显 `requested`、`observed` 和 `unknown`；如果 Codex 原生界面或工具没有直接给出 `model`/`reasoning_effort`，验收结论必须是 `UNKNOWN_RUNTIME`，不能把请求值冒充观察值。

系统要求：64 位 Windows 10 1809（内部版本 17763）或更高版本。分享包已包含 x64 Windows App Runtime，不需要另装 Visual Studio 或 .NET SDK。

## 已验证范围

- 核心测试：`209/209` 通过。
- Release x64 构建：`0` 警告、`0` 错误。
- MSIX 签名与身份验证通过；清单、程序集、文件和产品版本均为 `1.0.0.45`。
- 版本契约 `23` 个负例通过。
- 分享包 `38` 个文件，禁止文件计数 `0`，ZIP 完整性和文件树哈希通过；测试话术文件 5,520 bytes，SHA-256 为 `8E0AE5E0517961223B50E7E24459117790E0D55D30D5757B94CB7587E0CFC8AB`。
- 已安装态 WinUI 回归通过：宽、中、窄三种窗口尺寸；12 个角色；36 个路由组合框；3 个预算框；监控/悬浮层入口计数为 `0`；安装版本为 `1.0.0.45`。
- `auto/fast/standard/deep` 与复杂度升级共 5 个 CLI 计划案例通过；均为一次性派发回执，`execution_started=false`。
- 分享包中的 11 个 `hengshu_*.toml` 已安装，逐文件 SHA-256 与发布清单一致。

详细证据见 [VERIFICATION.md](VERIFICATION.md)，下载包哈希见 [RELEASE-SHA256.txt](RELEASE-SHA256.txt)。

## 边界与限制

- Commander/主大脑就是当前 Codex 根任务：它随当前 Codex 对话框实际选择的模型和推理强度变化；切换对话框模型后随当前任务变化。衡枢不会另造一个 Commander 子智能体。
- 角色路由里的模型、推理强度和权限是 `requested` 配置；若 Codex 原生窗格或工具结果没有回显，实际值保持 `unknown`，不能把请求值冒充观察值。
- CLI 只生成一次性原生派发计划，不在 CLI 内启动子智能体；真实创建、状态和运行时模型由当前 Codex 任务的原生能力决定。
- 衡枢不能扩大账号模型权限、Codex 平台并发上限、服务等级或额度，也不绕过权限边界。
- 这是测试签名构建，不是 Microsoft Store 或商业代码签名版本；随包只有公开测试证书，没有私钥或凭据。

## 仓库内容

- `README.md`：用途、安装、验证范围和限制。
- `VERIFICATION.md`：v1.0.0.45 验证证据摘要。
- `RELEASE-SHA256.txt`：GitHub Release 分享包 SHA-256。
- `Hengshu-Subagent-Test-Prompt.txt`：公开可审阅的通用多角色测试话术；分享包内同名文件与此哈希一致。
- `RELEASE_NOTES_v1.0.0.45.md`：本版改动、安装后测试步骤和边界。
- `RELEASE_NOTES_v1.0.0.44.md`：本版改动说明。
- `LICENSE-NOTICE.txt`：分发与第三方许可声明。

大型安装包只放在 GitHub Releases，不直接提交到 Git 历史。

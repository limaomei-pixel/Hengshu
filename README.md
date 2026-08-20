# 衡枢 Hengshu

衡枢是面向 Windows 上 Codex 原生子智能体的设置中心与有边界调度计划器。它保存 11 个子智能体职能角色的模型、推理强度、速度偏好和调度预算，并在用户明确发送 `开启智能体：<完整任务>` 后生成波次计划；真正的子智能体仍由当前 Codex 任务通过原生能力启动和展示。

## 当前公开版本

**v1.0.0.43（Windows x64，测试签名）** 已彻底删除独立“请求/观察监控”和悬浮层实验代码。

- 不包含请求监控入口、监控窗口或悬浮层。
- 不会在后台创建隐藏任务或隐藏子智能体。
- 普通 Codex 对话不会自动启动衡枢。
- Commander 就是当前 Codex 根任务，不是额外子智能体；其模型、推理强度、速度和权限始终继承当前对话框选择。
- 11 个 `hengshu_*` 原生子智能体类型均已实际启动测试。

## 下载与安装

请从 [Releases](https://github.com/limaomei-pixel/Hengshu/releases) 下载 `Hengshu-1.0.0.43-x64-share.zip`。

1. 完整解压 ZIP，不要从压缩包预览窗口直接运行。
2. 双击 `安装衡枢.cmd`。
3. 接受管理员权限提示；安装器会核对主程序、运行库和证书的 SHA-256，然后安装并启动衡枢。
4. 安装后通过桌面的 `衡枢 Hengshu.lnk` 启动。
5. 安装或升级 Skill 后，新建一个 Codex 任务，再使用 `开启智能体：<完整任务>`。

系统要求：64 位 Windows 10 1809（内部版本 17763）或更高版本。分享包已包含 x64 Windows App Runtime，不需要另装 Visual Studio 或 .NET SDK。

## 重要安全说明

这是测试签名构建，不是 Microsoft Store 版本，也没有商业代码签名。安装器会把随包的**公开测试证书**导入当前计算机的“受信任人”证书库，因此会请求管理员权限。分享包不包含证书私钥。

供应链扫描结果为 0 个发现；分享包中未发现私钥、OpenAI/GitHub 令牌、Cookie、密码或授权头。

## 已验证范围

- 核心测试：`208/208` 通过。
- Release x64 构建：`0` 警告、`0` 错误。
- MSIX 签名与包身份验证通过；清单、程序集、文件和产品版本均为 `1.0.0.43`。
- 版本契约 23 个负例通过。
- 分享包包含 37 个文件，禁止文件计数为 0，整包和文件树哈希已生成。
- 已安装态 WinUI 回归通过：宽、中、窄三种窗口尺寸；12 个职能角色；监控入口为 0；Commander 的 3 个路由框均为只读。
- 11 个 `hengshu_*` 原生子智能体类型全部实际启动并返回对应角色的 OK 结果；最终包内 Agent 配置与实测配置哈希一致。

详细证据摘要见 [VERIFICATION.md](VERIFICATION.md)，下载包哈希见 [RELEASE-SHA256.txt](RELEASE-SHA256.txt)。

## 边界与限制

- Hengshu 能请求子智能体模型和推理强度，但若 Codex 原生运行时没有回显，实际值仍是 `unknown`，不能拿请求值冒充观察值。
- 子智能体继承当前 Codex 任务的权限模式；衡枢不能扩大账号模型权限、并发上限或绕过 Codex 平台限制。
- Commander/主大脑完全由当前 Codex 对话框控制：例如对话框是 Sol + high，Commander 就是 Sol + high；切换对话框模型后，Commander 随当前任务选择变化。
- 本仓库公开的是测试分发与验证说明，不代表 Microsoft 或 OpenAI 对衡枢的认可。
- 源码未在此仓库授权开源；权利与第三方组件说明见 [LICENSE-NOTICE.txt](LICENSE-NOTICE.txt)。

## 仓库内容

- `README.md`：用途、安装、限制与安全说明。
- `VERIFICATION.md`：当前公开版本的验证证据摘要。
- `RELEASE-SHA256.txt`：GitHub Release 分享包的 SHA-256。
- `LICENSE-NOTICE.txt`：分发与第三方许可声明。
- 大型安装包位于 GitHub Releases，不直接提交到 Git 历史。

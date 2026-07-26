<p align="center">
  <img src="build/appicon.png" width="112" alt="OneOpenAI">
</p>

<h1 align="center">OneOpenAI</h1>

<p align="center">
  在桌面端完成 ChatGPT 或 Codex OAuth 登录，生成可持续刷新的 OneOpenAI RT。
</p>

<p align="center">
  <a href="https://github.com/oneopenai/oneopenai-desktop/releases/latest"><strong>下载最新版</strong></a>
  ·
  <a href="https://github.com/oneopenai/oneopenai-desktop/issues">反馈问题</a>
</p>

## 下载

请前往 [GitHub Releases](https://github.com/oneopenai/oneopenai-desktop/releases)
下载对应系统的安装包：

| 系统 | 下载文件 | 支持范围 |
|---|---|---|
| macOS | `OneOpenAI-macOS-arm64.zip` | Apple Silicon（M1/M2/M3/M4） |
| Windows | `OneOpenAI-amd64-installer.exe` | Windows 10/11 x64 |

Windows 需要 Microsoft WebView2 Runtime。Windows 10/11 通常已经随 Microsoft Edge
安装；如果程序提示缺少 WebView2，请先安装微软官方运行时。

## 功能

- ChatGPT App/iOS OAuth 网页登录。
- Codex OAuth 网页登录。
- 登录完成后生成固定的 `oneopenai_rt_...`。
- 使用固定 RT 刷新 Access Token，固定 RT 不随上游 RT 轮换而改变。
- Token 默认隐藏，可一键显示或复制。
- 支持 macOS 和 Windows 10/11。

ChatGPT 和 Codex 是两个独立入口，使用不同的 OAuth client、回调地址和授权参数。

## 使用方法

1. 安装并打开 OneOpenAI。
2. 选择 **ChatGPT** 或 **Codex**。
3. 点击“浏览器打开”，在 OpenAI 官方页面完成登录。
4. 浏览器回调后，OneOpenAI 会自动回到前台并生成固定 RT。
5. 点击“复制”保存 `oneopenai_rt_...`，也可以点击“刷新 Access Token”检查凭证。

ChatGPT 登录完成后，浏览器原页面可能继续显示转圈。这是自定义 App 回调后的浏览器
表现；只要 OneOpenAI 已显示“登录成功”，即可直接关闭浏览器页面。

## 安装说明

### macOS

解压后将 `OneOpenAI.app` 移动到“应用程序”目录，再打开使用。

如果测试版本尚未完成 Apple notarization，macOS 可能显示安全提示。建议正式发布时
使用 Developer ID 签名并完成 notarization。

### Windows 10/11

运行 `OneOpenAI-amd64-installer.exe` 完成安装。ChatGPT OAuth 使用自定义 URL
Scheme 接收回调，因此不要只复制或直接运行未安装的 `.exe`。

未签名的测试安装包可能触发 Windows SmartScreen；正式发布时建议进行 Windows
代码签名。

## 有效期

- Access Token 有效期以 OpenAI 返回的 `expires_in` 或 JWT `exp` 为准。
- `oneopenai_rt_...` 在 OneOpenAI Gateway 中没有预设 TTL。
- 固定 RT 的实际可用期仍取决于背后的 OpenAI refresh token。
- 退出登录、撤销授权、账号安全变更或 OpenAI 服务端策略变化都可能使凭证失效。

## 隐私与安全

- 账号密码只输入在 OpenAI 官方登录页面。
- OneOpenAI Desktop 不接收账号密码。
- xyhelper 只用于生成 ChatGPT App 登录所需的预授权，不接收 OAuth callback、PKCE、
  Access Token 或 refresh token。
- OAuth callback 换取 token 以及后续 RT 刷新均请求 OpenAI 官方接口。
- 官方 RT 会提交到 `https://public.gateway.oneopenai.com`，加密保存后换成固定的
  `oneopenai_rt_...`。
- 固定 RT 与密码具有相近的敏感性，请勿发送给他人或提交到公开仓库。

## 常见问题

### 登录成功后浏览器一直转圈

回到 OneOpenAI 查看结果。App 已显示“登录成功”时，浏览器页面可以直接关闭。

### Windows 登录后没有回到 App

请确认使用安装器安装了 OneOpenAI。Windows 只有安装后才会注册
`com.openai.chat` OAuth 回调协议。

### 固定 RT 刷新失败

重新执行对应的 OAuth 登录。官方 RT 可能因退出登录、撤销授权或账号安全状态变化而
失效。

## 从源码构建

开发、检查和打包命令见 [开发文档](docs/development.md)，OAuth 链路与安全设计见
[OAuth 说明](docs/chatgpt-oauth-token.md)。

## 免责声明

OneOpenAI 是独立开发的第三方工具，与 OpenAI 无隶属或官方合作关系。请仅登录和使用
你本人有权访问的账号，并遵守相关服务条款。

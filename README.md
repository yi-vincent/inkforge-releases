# 墨坊 InkForge 安装包下载

最新版本：**[Releases → Latest](https://github.com/yi-vincent/inkforge-releases/releases/latest)**，在 Assets 里按电脑选一个：

| 文件 | 适用 |
|---|---|
| `InkForge-<版本>-mac-arm64.dmg` | macOS 12+，Apple 芯片（M1–M4）。「关于本机」里写着「芯片」 |
| `InkForge-<版本>-mac-x64.dmg` | macOS 12+，Intel 芯片。「关于本机」里写着「处理器」 |
| `InkForge-<版本>-win-x64.exe` | Windows 10 / 11 64 位。SmartScreen 提示时点「更多信息 → 仍要运行」 |

macOS 首次打开：Finder 里右键 → 打开，或「系统设置 → 隐私与安全性」点「仍要打开」。

每个版本的 SHA-256 校验和见官网 https://inkforge.ailinko.cn/#download 。购买授权与使用说明也在官网。

本仓库只存放安装包与构建工作流，不含源代码。

## 构建（维护者）

Actions → **Desktop build** → Run workflow，填私有仓库的 `ref` 和版本号（如 `1.3.0`）。三个平台各自打包并启动安装版冒烟，安装包上传到 `v<版本>` 的**草稿** Release（不经过公开 artifact）。验证后在 Releases 页发布，再在本机用 `scripts/publish-release.mjs` 登记官网。

需要的配置（Settings → Secrets and variables → Actions）：

| 名字 | 类型 | 说明 |
|---|---|---|
| `CONTENT_REPO` | Variable | 私有源码仓库 `yi-vincent/aiwritex-clone` |
| `CONTENT_REPO_TOKEN` | Secret | Fine-grained PAT，只授权该私有仓库，Contents: Read |
| `ARTIFACT_PASSPHRASE` | Secret（可选） | 构建失败时加密上传日志；没配就不上传 |

公开日志里只有各步骤的通过 / 失败与用时，详细输出写入临时目录。

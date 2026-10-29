# VoiceDraft 语音草稿 · Mac 预览版

VoiceDraft 将语音转为文字，并支持把文字填入其他应用。提供图形应用（GUI）和命令行工具（CLI）两种形式。

**当前运行包处于 Release 草稿阶段，尚未开放公众下载。** 公开发布后，可在[发行版页面](https://github.com/jeoffrey2011/VoiceDraft-Downloads/releases)选择对应附件。请下载运行包，不要把 GitHub 自动生成的 Source code ZIP 当成安装包。

| 版本 | 运行包 | 使用说明 |
|---|---|---|
| GUI 0.3.16 Build29 预览版 | `VoiceDraft-GUI-0.3.16-build29-runtime-preview.zip` | [GUI 安装与使用](GUI_USER_GUIDE.md) |
| CLI 0.1.4 独立预览版 | `VoiceDraftCLI-0.1.4-macos-universal2-standalone-preview.tar.gz` | [CLI 安装、升级与卸载](CLI_USER_GUIDE.md) |

## 系统与安装

- 最低系统目标 macOS 13；包中包含 Apple 芯片（arm64）和 Intel（x86_64）架构，但不代表所有设备和系统均已实测。
- GUI 已预编译；CLI 自带 Python 3.13 和预编译原生后端。无需另装 Python、pipx、Swift 编译器或 Xcode，不替换系统 Python。
- 解压后保留完整目录，按各自指南运行 `install.command`。CLI 不要只复制 `voicedraft` 而遗漏 `_internal`。
- 安装前及复制后会检查包内完整性；失败时停止并重新下载。使用前核对[压缩包 SHA-256](CHECKSUMS.json)。哈希及随包清单不单独提供发布者身份保证。
- 麦克风、语音识别以及自动填入所需辅助功能权限按需授权；不需要屏幕录制权限。本地语音资源仍由系统提供。

## 预览范围

本次打包修订为 **preview-check1**。采用 **ad-hoc 临时签名，未经 Apple 公证，无 Developer ID 身份保证**；更新或运行副本改变后可能需要重新授权。

Intel 实机、旧 macOS、真实录音、外部输入框、登录/解锁及真实权限弹窗尚未完成本轮验收。Windows 尚无提供并验证的运行包。历史稳定版验收不自动覆盖当前预览版。

输入目标判断、转写和标点可能出错，请核对文字及目标后使用。本预览版不承诺所有应用兼容、文字永不丢失或授权永久保留。

权限异常时按[授权对象与排障说明](AUTHORIZATION.md)先核对运行副本，再结束录音并退出旧进程、重启正确程序，仅在必要时处理对应失效授权；不默认删除用户数据、重置全部权限或关闭系统安全保护。

## 隐私、许可与检查

- [隐私、数据流与停止录音](PRIVACY.md)
- [发行说明及许可范围](RELEASE_NOTES.md)
- [更新记录](CHANGELOG.md)
- [本次检查及待验收范围](PREVIEW_CHECK.md)
- [检查结果](CHECK_RESULTS.json)
- [Apache-2.0 完整许可](LICENSE)、[NOTICE](NOTICE)及[第三方许可说明](THIRD_PARTY_NOTICES.md)

在适用法律允许且无另行有效书面约定的范围内按现状提供，不新增保修、持续维护或响应时限承诺，不排除不可排除的责任或不可放弃的法定权利。

本仓库提供使用说明、许可和校验材料；实现源码暂未公开。运行包不直接附带项目 Python/Swift/C# 实现源码，但不保证无法逆向；保留原许可授予的修改和再分发权利。

发布后从 GitHub、Gitee 重新下载并验证哈希、包内完整性和下载入口的步骤仍待执行；真实安装运行验收中未执行的项目继续保留为待办。

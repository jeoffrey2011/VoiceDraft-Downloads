# VoiceDraft GUI 安装说明（Mac 预览版）

GUI 仅支持 macOS 13+。App 已预编译，无需 Python、pipx 或 Xcode。解压后保留整个目录，双击 `install.command`，自动校验完整性后安装到 `~/Applications`，不会自动启动 App。终端也可运行：

```sh
bash install.sh
# 自选安装目录；拒绝覆盖已有同名 App
bash install.sh --destination /absolute/path/to/Applications
```

已有同名 App 时安装停止；请先结束录音并退出旧程序，再自行保留旧版本、选择新目录，不会自动覆盖运行中的应用。录音需要系统权限及本地语言资源，自动填入需要辅助功能权限。当前临时签名、未公证，按系统实际安全提示操作。

这是 GUI 0.3.16 Build29 候选包，不是稳定版。Intel/旧 macOS 实机、真实录音与外部输入尚未完成本轮验收。源码暂不公开，许可保留 Apache 2.0。

## 安装前自动完整性校验

双击 `install.command` 或执行 `bash install.sh` 时，安装器先用 macOS 自带工具检查 `PACKAGE_CONTENTS.tsv` 中的文件 SHA-256、符号链接及文件清单，无需用户安装 Python，也不会先启动录音程序。缺失、损坏、清单格式错误或意外多出的文件会停止安装，并提示重新下载完整包；Finder 的 `.DS_Store` 文件除外。复制到临时安装目录后再次校验，通过后才切换命令入口或放入 App。完整性校验失败不会替换原有程序或修改 Shell 配置。

可以单独执行 `bash verify-package.sh` 检查解压目录。请保留完整包，不要编辑包内文件后继续安装。CLI 还保留 `voicedraft self-check` 作为运行包自检；GUI 的 App 自检只检查配置和资源，不能替代整包校验。GUI 若直接拖动 App 会绕过安装器，请优先使用 `install.command`。

包内清单用于发现缺失和损坏，不是发布者身份认证：仍应从可信发布页下载，并比对发布页的压缩包 SHA-256。发布者仍需在上传后重新下载附件，核对本地原包的 SHA-256，再对解压包运行校验及隔离安装测试。

发布状态及许可范围见 RELEASE_NOTES.md；权限、数据流及停止录音见 PRIVACY.md；第三方条款见 THIRD_PARTY_NOTICES.md、NOTICE 和 LICENSE。本说明不承诺跨平台完全兼容或独立紧急停止能力。

授权对象和更新后排障见 AUTHORIZATION.md：先确认运行副本，再结束录音并退出旧进程、重启正确程序，仅在必要时重新添加对应的失效授权。预览包采用 ad-hoc 临时签名、未公证，更新后可能重新授权；本说明未经过本轮真实权限弹窗验收，不要求删数据、重置全部权限或关闭安全保护。

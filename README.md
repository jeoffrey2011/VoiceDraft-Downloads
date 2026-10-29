# VoiceDraft 用户下载材料（候选，尚未正式发布）

本目录不包含完整项目源码；GUI和CLI源码暂保存在两个私有仓库。Apache2.0许可保留，不增加禁止修改的限制。运行包不直接附带项目Python/Swift/C#实现源码，但不保证无法逆向；安装脚本与第三方许可可读。

GUI：下载runtime-preview.zip，解压完整包后双击install.command校验安装，无需Python/pipx/Xcode。CLI：下载standalone-preview.tar.gz，保留整个目录，双击install.command或执行bash install.sh --add-path；自带Python3.13，之后直接voicedraft start。不要只取单个可执行文件而丢掉_internal。

已有Python也可使用独立包，它不替换系统Python。另有本地Python+wheel可选路线，但当前wheel含源码，暂保留私有，不放此公共目录。安装器默认保护命令冲突，显式--replace才选择新入口。

GUI0.3.15 Build25是用户确认的稳定基线；当前GUI0.3.16 Build29与CLI0.1.4 standalone-preview是候选打包，不能冒充稳定版。旧GUI.16 Build27/28为撤回失败版本，未放入此目录。

**Windows没有独立包或已验证wheel，必须在Windows生成、测试后发布。** Intel/旧macOS、真实录音、外部输入框、登录解锁尚未重新实测。Mac包临时签名未公证，仍需用户授予相应权限和本地语言资源。

使用说明见CLI_USER_GUIDE.md、GUI_USER_GUIDE.md，验证见CHECK_RESULTS.json，校验见CHECKSUMS.json。release-assets仅用于平台Release附件，不建议直接提交到源码Git。当前没有上传远程仓库。

安装前自动校验与失败处理见两个 USER_GUIDE；仍需保留上传后重新下载并比较压缩包 SHA-256 的发布核验。

隐私与权限、持续录音的停止方式见 [PRIVACY.md](PRIVACY.md)；预览局限和按现状许可说明见 [RELEASE_NOTES.md](RELEASE_NOTES.md)。[LICENSE](LICENSE) 为 Apache-2.0 完整原文，第三方条款见 [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) 和 NOTICE。

授权对象和更新后排障见 AUTHORIZATION.md：先确认运行副本，再结束录音并退出旧进程、重启正确程序，仅在必要时重新添加对应的失效授权。预览包采用 ad-hoc 临时签名、未公证，更新后可能重新授权；本说明未经过本轮真实权限弹窗验收，不要求删数据、重置全部权限或关闭安全保护。

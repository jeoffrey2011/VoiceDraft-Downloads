# VoiceDraft CLI 独立运行包（Mac 候选版）

本包自带Python运行时和预编译录音后端。无需安装Python、pipx、Xcode、Swift或C#编译器，不修改已有Python环境。项目Python/Swift/C#实现源码未直接附带；编译代码仍可能被逆向，不是加密或不可反编译方案。Apache2.0许可与第三方运行时声明随包保留。

## 安装

解压后保留整个文件夹，不能只移动voicedraft文件而丢掉_internal。可直接双击install.command，或在该目录执行：

```sh
bash install.sh --add-path
```

安装到用户的 `~/.local/share/voicedraft-cli/versions/<内容标识>/`，命令入口位于 `~/.local/bin/voicedraft`。--add-path会在用户自己的常见Shell配置中加入带标记的PATH段，修改前备份已有配置，重新打开终端生效；不改系统配置。支持zsh、bash、sh和fish；不识别的Shell仅提示手动配置。直接运行 `bash install.sh` 则不改Shell配置，也可以始终使用命令绝对路径。

若已有不同安装的同名命令，默认拒绝覆盖。检查后可显式加--replace备份并切换入口；不会删除旧Python、旧安装或停止运行中的服务。升级请先结束录音、手动voicedraft stop；启用过自启时先用旧安装autostart remove，再安装新版，按需重新启用自启。安装保留旧版本文件，不覆盖运行中的文件。

## 使用

```sh
voicedraft --version
voicedraft self-check
voicedraft start
voicedraft authorize
voicedraft doctor
voicedraft watch
```

start只进入待命，不自动录音。第一次start会从包内校验并解包预编译后端，不调用编译器，不需setup-backend。按Ctrl+F9开始；默认持续模式再按一次结束。GUI与CLI共用快捷键，不要同时运行。完成后 `voicedraft stop` 停止服务。watch的Ctrl+C只退出查看。

需要macOS13+、本地识别语言资源，以及用户允许的麦克风、语音识别和自动填入所需辅助功能权限；无屏幕录制要求，不回退云端。包仍是临时签名、未经苹果公证，下载后可能受系统安全策略限制。请核对发布来源和SHA256，并按系统实际提示允许打开，不应关闭系统安全保护。

## 卸载

先结束录音、执行voicedraft stop；启用过自启则执行voicedraft autostart remove。双击uninstall.command并确认这些步骤已完成。终端也可以：

```sh
bash uninstall.sh --purge --stopped
```

不带--purge时仅移除属于该安装的命令入口，保留版本文件。卸载不会改动Python、其他程序、用户数据目录、原生后端缓存、登录配置、Shell标记段或备份；这些可确认不再使用后自行清理。Shell中保留一个已不存在的用户bin目录通常不妨碍其他程序。

## 两种安装路线

独立运行包固定使用包内Python，不自动切换系统Python。已有Python的用户可以另外选择wheel+pipx/venv，但当前wheel含实现源码，暂不放入公开下载区；两者可并存文件，不能无提示争抢同名命令，也不宜同时运行服务。

## 验证范围

这是0.1.4基础上的standalone-preview打包修订，不是已验收稳定版。实际架构及测试见PACKAGE_MANIFEST.json和发布检查报告。Intel/旧macOS、真实语音与登录/解锁需分别验证。Windows独立包未生成或验证，必须在Windows环境处理，不能使用此Mac包。

## 安装前自动完整性校验

双击 `install.command` 或执行 `bash install.sh` 时，安装器先用 macOS 自带工具检查 `PACKAGE_CONTENTS.tsv` 中的文件 SHA-256、符号链接及文件清单，无需用户安装 Python，也不会先启动录音程序。缺失、损坏、清单格式错误或意外多出的文件会停止安装，并提示重新下载完整包；Finder 的 `.DS_Store` 文件除外。复制到临时安装目录后再次校验，通过后才切换命令入口或放入 App。完整性校验失败不会替换原有程序或修改 Shell 配置。

可以单独执行 `bash verify-package.sh` 检查解压目录。请保留完整包，不要编辑包内文件后继续安装。CLI 还保留 `voicedraft self-check` 作为运行包自检；GUI 的 App 自检只检查配置和资源，不能替代整包校验。GUI 若直接拖动 App 会绕过安装器，请优先使用 `install.command`。

包内清单用于发现缺失和损坏，不是发布者身份认证：仍应从可信发布页下载，并比对发布页的压缩包 SHA-256。发布者仍需在上传后重新下载附件，核对本地原包的 SHA-256，再对解压包运行校验及隔离安装测试。

发布状态及许可范围见 RELEASE_NOTES.md；权限、数据流及停止录音见 PRIVACY.md；第三方条款见 THIRD_PARTY_NOTICES.md、NOTICE 和 LICENSE。本说明不承诺跨平台完全兼容或独立紧急停止能力。

授权对象和更新后排障见 AUTHORIZATION.md：先确认运行副本，再结束录音并退出旧进程、重启正确程序，仅在必要时重新添加对应的失效授权。预览包采用 ad-hoc 临时签名、未公证，更新后可能重新授权；本说明未经过本轮真实权限弹窗验收，不要求删数据、重置全部权限或关闭安全保护。

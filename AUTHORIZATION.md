# 授权对象与更新后排障（Mac 预览包）

本说明基于本次最终包的 Info.plist、签名标识与调用权限 API 的实现核对。没有在用户现用服务上测试或修改权限，也没有完成真实授权弹窗验收；系统显示名称与启动链的归属可能随 macOS 版本而异。

## 授权给哪一个程序

| 用途 | 本包中发起请求的对象 | 版本与辨认信息 |
| --- | --- | --- |
| GUI 的麦克风、语音识别、自动填入所需辅助功能 | 实际打开的 `语音草稿 0.3.16.app`；可执行文件为 `Contents/MacOS/VoiceDraft` | 版本 0.3.16、Build 29；Bundle ID `local.voicedraft.mac.v0316.build29`；显示名称“语音草稿 0.3.16” |
| CLI 的麦克风、语音识别、自动填入所需辅助功能 | 实际运行的 `VoiceDraft CLI.app`；可执行文件为 `Contents/MacOS/VoiceDraftCLIHost` | 版本 0.1.4、Build 4；Bundle ID `local.voicedraft.cli.mac`；显示名称“VoiceDraft CLI” |
| CLI 登录/解锁询问窗口 | `VoiceDraft Login Prompt.app` / `VoiceDraftLoginPrompt` | 版本 0.1.2、Build 1；Bundle ID `local.voicedraft.cli.session-prompt`；只负责询问/启动，不是录音授权对象 |

CLI 的 `voicedraft` 是控制入口，不应凭它的名字就给另一个 Python、终端或登录询问程序添加录音/辅助功能权限。API 请求由上表的录音后端发起；如果系统弹窗归属显示为另一个应用，应先核对本次启动链、实际运行路径与诊断结果，不要盲目授权同名旧副本或任意终端。不能保证系统设置在每台 Mac 上总按上表显示名称。

GUI 安装器默认安装到 `~/Applications/语音草稿 0.3.16.app`。若用户指定了其他 --destination，或直接打开下载目录的 App，以实际进程路径为准。GUI 的窗口标题可能只显示“语音草稿”，不足以区分副本。

CLI 独立包首次启动会把预编译后端放到用户目录中的：

```text
~/Library/Application Support/VoiceDraftCLI/backends/0.1.4-<后端内容摘要>/build/VoiceDraft CLI.app
```

这里的摘要由原生资产内容计算，不是安装器的版本目录标识。控制入口通常为 `~/.local/bin/voicedraft`，指向 `~/.local/share/voicedraft-cli/versions/<内容标识>/voicedraft`。权限应对应正在运行的缓存后端 App，不是下载包 `_internal/.../prebuilt/` 里的未运行副本。`voicedraft setup-backend` 会显示本次命令对应的 `backend_root`；独立包使用预编译文件，不调用编译器或启动录音。不要仅为授权而移动/改名已运行的后端。

## 确认副本，再逐步排障

以下是供用户手动执行的步骤；安装器不会自动操作权限或停止服务。

1. **确认正在运行哪一份。** GUI 在“活动监视器”核对进程路径，Finder 对实际 App“显示简介”核对版本，必要时只读查看 `Contents/Info.plist` 的 Bundle ID 和 Build。CLI 用 `command -v voicedraft`、`ls -l "$(command -v voicedraft)"` 确认命令入口，再用 `voicedraft --version` 和 `voicedraft status` 辨认控制程序与后台。`status` 中 pid 是控制进程 PID，不是录音后端 PID；可在活动监视器核对其路径，同时找到 VoiceDraftCLIHost 对应的 App。命令版本号和 `start` 返回 already_running 都不证明已换成新后端；同一运行目录会连接已有后台。不要分享含随机控制凭据的 service.json。
2. **结束录音并退出旧进程。** GUI 先“结束录入”/取消，再从应用菜单或菜单栏“退出”，只关窗口不等于退出。CLI 先 `voicedraft end`，确认录入结束后 `voicedraft stop`；若使用过自定义 --runtime，应对同一目录执行，例如 `voicedraft --runtime '/实际运行目录' stop`。确认相应 VoiceDraftCLIHost 退出后再继续。不要同时运行 GUI、CLI 或多个旧副本抢占 Ctrl+F9；本步骤不要求删除用户数据或修改自启机制。
3. **从确认的路径重启正确程序。** GUI 打开已安装的那一个 App。CLI 从正确入口执行 `voicedraft setup-backend` 核对后端目录，再 `voicedraft start` 进入待命；start 不自动录音。需要明确请求权限时执行 `voicedraft authorize`，响应系统提示后 `voicedraft doctor`。authorize 必须连接已就绪服务；doctor 在服务未运行时只报告环境，不能证明权限已通过。使用 --no-insert 启动的 CLI 不主动请求辅助功能；只复制文字时无需该权限。
4. **仅在仍有问题时处理对应授权。** 在系统设置的“隐私与安全性”中检查麦克风、语音识别及辅助功能（部分系统可能显示相近的“设备控制和数据访问”名称）。已开关允许但程序仍未认可时，先在结束录音后退出/重启正确副本并重新检查。仅当确认辅助功能条目指向旧副本或已经失效时，才在该列表移除那一项，再用“+”选择实际运行的 GUI App 或 CLI 缓存后端 App，并响应系统验证；不要删除其他应用权限。麦克风和语音识别列表的管理方式可能不同，不要求它们一定有“+/-”，按当前系统提供的开关和程序重新请求处理。仅在系统要求时退出重开。

GUI “授权辅助功能”按钮和 CLI authorize 是请求/检查入口，不是让权限生效的唯一途径；直接在系统设置允许正确副本同样是合法路径。CLI 正在运行时 doctor 返回的 microphone_authorized、speech_authorized、accessibility_authorized 来自该原生后端；hotkey_available 只代表快捷键注册，不等于麦克风或自动填入授权。on_device_supported 是语言/设备支持状态，也不是权限开关。GUI 首次开始录入时请求麦克风/语音识别；“授权辅助功能”按钮只处理辅助功能。

## 签名与安全边界

本包为预览版，使用 ad-hoc 临时签名，无 Developer ID 团队身份，未经 Apple 公证。更新或实际运行位置/副本改变后，系统可能要求重新授权；不能承诺授权永远保留，也不要求每次更新都先删授权。本轮保持 GUI、CLI 和询问助手的 Bundle ID、签名标识/类型及权限架构不变；只补全 CLI 包内 Python framework 的资源签名封装，仍沿用原有 ad-hoc 标识。

签名结构检查通过不等于 Gatekeeper、公证、真实权限弹窗或所有系统实测通过。Windows 无运行包；Intel 实机、旧 macOS、真实录音、外部输入框和登录/解锁尚未完成本轮验收。遇到来源/安全提示时核对可信发布来源、哈希及对应 App，按系统正常流程处理。排障不以删除用户数据、重置所有权限、关闭 Gatekeeper/SIP 或删除隔离属性为默认步骤；不能承诺绕过系统安全策略就能运行。

官方入口：[Apple 隐私设置说明](https://support.apple.com/guide/mac-help/mchl2b29231a/mac)、[媒体采集授权](https://developer.apple.com/documentation/bundleresources/requesting-authorization-for-media-capture-on-macos)。本项目本地识别条件、数据边界及停止方法另见 PRIVACY.md。

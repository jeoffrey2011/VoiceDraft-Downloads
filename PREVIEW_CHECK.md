# 本次预览发布必要检查 · 2026-10-28

修订：preview-check1。唯一上传基准为当前分发目录；未执行远程上传、系统授权或真实录音。

## 修改

- 增加 AUTHORIZATION.md：以包内元数据辨认 GUI、CLI 实际录音后端和登录询问助手；说明缓存后端路径、控制程序版本与运行副本的区别，以及“确认副本 → 结束录音并退出 → 重启正确程序 → 必要时处理对应授权”的顺序。
- 统一披露预览版、ad-hoc 临时签名、未公证、更新后可能重新授权及真实未验证范围。不默认删除用户数据、重置全部权限或关闭安全保护。
- 严格检查发现 CLI 的 Python.framework 只有二进制签名，缺少 framework 资源封装，最初列为发布阻塞。现以原有 ad-hoc 标识补全资源签名封装；解释器签名元数据和 CodeResources 改变，但编译代码节、Info.plist 和既有签名标识/类型保持一致。没有重编译、引入证书或改变产品 Bundle ID/权限/升级机制。
- GUI、CLI 控制入口、原生录音后端和登录询问助手二进制逐字节保持一致。增加可复用的严格签名检查和构建后的封装检查，刷新源码 ZIP、包内清单及最终压缩包 SHA-256。

## 验证结果

- 最终 GUI ZIP、CLI tar.gz 与 CHECKSUMS.json 一致；实际解压目录的 PACKAGE_CONTENTS.tsv 校验通过，CLI PACKAGE_MANIFEST.json 的 self-check 通过。
- 不跳过资源，使用 codesign --verify --deep --strict --all-architectures 检查：GUI 1、CLI 49 个 Mach-O 文件，3 个 App 与 1 个 Python.framework 均通过。签名结构通过不等于 Developer ID、Apple 公证、Gatekeeper 下载启动或真实授权验收通过。
- 实际运行包在临时 HOME 下通过安装，安装日志确认复制前及复制后校验；CLI 在隔离目录解包预编译后端，其路径、版本和 Bundle ID 与授权说明一致。安装后的签名及包内说明再次核对。
- 复用既有轻量测试：CLI 16 项安装测试通过；GUI 15 项适用测试通过，1 项 CLI 专属测试跳过；两个最终压缩包合计 8 项损坏测试通过。未为本轮改动重跑无关的录音/模拟服务测试；原 47 项 CLI 全套结果属于前轮 integrity1 修订。
- 公开材料检查共 94 个运行包文件，未发现项目业务实现源码、含源码 wheel、明显私钥标记、本机作者路径或已知用户状态/录音文件名；安装/校验 Shell 脚本和第三方许可可读，不承诺不可逆向，也不是完整秘密/安全审计。
- 旧 GUI 0.3.14 Build24 和 0.3.15 Build25 稳定交付物哈希仍匹配原清单。

## 发布阻塞与剩余验收

本次发现的 Python.framework 资源封装阻塞已解决；当前必要检查未留存未解决阻塞。未公证、Windows 无包、Intel/旧 macOS/真实录音/外部填入/登录解锁与实际权限弹窗未完成本轮验收，继续作为预览版如实披露，不能据此标为稳定或全面兼容。

没有修改系统权限、访问现用服务、停止用户进程、启动真实录音或重编译；没有改变 GUI/CLI/助手的 Bundle ID、签名身份/类型、权限架构或升级机制。法务和完整安全审计范围仍按 RELEASE_NOTES.md/原检查说明保留。

## 上传文件与回下载

两个完整源码目录和源码 ZIP 仅进入各自私有仓库；含源码的可选 wheel 继续留在 private-options，不上传到公开库。公开下载仓库提交 VoiceDraft-Downloads 中的说明、许可和校验材料，release-assets/ 被 .gitignore 排除，两个运行包分别上传为 Release 附件。不要将整个分发目录公开。

最终 SHA-256：

- `VoiceDraft-GUI-0.3.16-build29-runtime-preview.zip`

  `5c464cb22b00319e206eba20e0b26f44503d872b4db78d3c3ede25a2c62819ef`

- `VoiceDraftCLI-0.1.4-macos-universal2-standalone-preview.tar.gz`

  `4b5dde6b99addd925c81017cc7a4930ae57d5223f37cd286c5d0a0660d1ab475`

上传后从 GitHub、Gitee 分别重新下载附件，比对本地最终包及 CHECKSUMS.json，解压后校验和隔离安装；这一步由发布环节完成，目前未执行。

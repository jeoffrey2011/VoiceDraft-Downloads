# 发布安排

完整GUI/CLI源码分别从private-source建立私有仓库。公共下载仓库只使用本目录的文档和许可；GitHub/Gitee的Release附件使用release-assets中的两个运行包。不要上传private-source、private-options、旧源码ZIP或wheel到公共库；公共仓库的Source code自动下载只应包含这里的文档。先检查git暂存差异再提交，当前没有自动建库或上传。

正式推广前确定正式版本/构建标识并完成真实使用验收；不要把preview作为稳定版。Windows包未生成，不能补一个下载占位假装已支持。

上传后分别从两平台重新下载附件，与本地原包及 CHECKSUMS.json 比对 SHA-256；解压运行 bash verify-package.sh，再在临时 HOME/目录测试安装。用未登录窗口验证公开下载。包内自动校验不能替代此步骤。

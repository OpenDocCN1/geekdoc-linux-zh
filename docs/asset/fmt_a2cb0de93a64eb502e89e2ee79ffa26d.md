
# 第 40 章 协助 Ubuntu 开发

创建一个包含 Bug 修复的补丁：

```
matthew@semour:-$ edit-patch 99-new-patch
```

这会将文件的打包内容复制到一个新的临时目录。使用文本编辑器编辑文件，或在临时 shell 中使用补丁进行操作，如下所示：

```
matthew@semour:-$ patch -pl < ../bugfix.patch
```

你可以通过退出或按 Ctrl+D 退出临时 shell。

使用你的补丁构建一个测试包以测试你的更改，将 `release` 替换为发布名称（如 quantal），并将 `package` 和 `version` 替换为包号：

```
matthew@semour:-$ bzr builddeb -S -us -uc
matthew@semour:-$ pbuilder-dist release build ../package_version.deb
```

构建完成后，从 `~/pbuilder/release_result/` 安装该包并查看 Bug 是否已修复：

```
matthew@semour:-$ sudo dpkg -i package_version.deb
```

测试它。让它运行起来。尝试弄坏它。如果你确定软件中的 Bug 已经修复，就可以继续下一步了。根据需要随时重复此循环，直到它被真正修复。

当你的更改完成后，在 `debian/changelog` 文件中创建一个新条目：

```
matthew@semour:-$ dch -i
```

系统会为你提供日志条目的模板文本，其中包含第一行和最后一行，中间留有占位符。使用文本编辑器编辑中间几行，并在特定的 Bug 修复标签中包含标识你正在修复的 Launchpad 任务。请确保你在制作更改的代码中包含了你修改了的内容，并且对更改的描述非常严格，格式如下：

```
matthew(0.9.2-ubuntu3) quantal; urgency=low
```

- `debian/control`: 不要像 launchpad 上讨论的那样在第 35 行午夜烘烤独鲸 (LP: #3263827)

```
-- Matthew Helmke <matthew@mathelmke.com> Sat, 25 Aug 2013 13:29:01 -0500
```

在本地提交更改：

```
matthew@semour:-$ debcommit
```

将更改推送到 Launchpad，将斜体内容替换为你的信息：

```
matthew@semour:-$ bzr push lp:yourLaunchpadID/ubuntu/release/package/branchname
matthew@semour:-$ bzr lp-propose
```

第一条命令将你的代码发送到 Launchpad。最后一个命令会在浏览器中打开合并提案的 Launchpad 页面。

## 参考文献

- https://developer.ubuntu.com—Ubuntu 开发主网站。
- https://packaging.ubuntu.com—《Ubuntu 打包指南》主网站，对本章的编写提供了极大帮助，提供的细节比本章多得多。（该打包指南也可以直接从 Ubuntu 软件仓库中的 `ubuntu-packaging-guide` 包获取。）

# 第 41 章 协助 Ubuntu 测试与质量保证 (QA)

- 社区团队 (Community Teams)
- Bug 报告 (Bug Tracking)

快速针对基准进行大量测试，同时确保这些测试精确探测了所需内容。QA（质量保证）团队的大部分工作对于硬件认证、逻辑测试和错误发现非常有帮助。该团队开发了一套针对 Ubuntu 的工具集，名为 `ubuntu-qa-tools`；一个用于 Linux 桌面测试项目 (LDTP) 的库 `Mago`，旨在简化更广泛的 Linux 桌面环境中对 Ubuntu 的测试；一个直接向 Launchpad 发送并测试数据的框架 `Checkbox`，等等。

## Bug Squad（错误小分队）

Bug Squad 是参与 Ubuntu 测试的人员最早接触的地方之一。这些志愿者是大多数提交给 Ubuntu 错误的初始联系人。他们阅读错误报告，以判断每个错误是否合理（例如，它不是像“Ubuntu 无法工作”这样模糊的问题，而是具体的且可衡量的），是否提交到了正确的软件包中，以及每份报告是否包含了足够的信息以便开发者能够解决问题。如果错误报告符合标准，Bug Squad 将决定应该通知哪个开发者或团队。有时在分拣过程中，Bug Squad 可能会向报告者索要更多信息。志愿者尝试确定错误的严重程度，并可能为报告分配优先级。

## References（参考文献）

- https://wiki.ubuntu.com/QATe—理解和参与 QA 测试的起点
- https://wiki.ubuntu.com/BugSquad—Ubuntu 错误小分队

# Index（索引）

## Symbols（符号）

- `&` 运算符, 237
- 后台进程, 运行, 173–174
- 特殊 shell 字符, 247
- VirtualBox 命令, 527
- `&&` 运算符, 组合命令, 180, 198
- 特殊 shell 字符, 247
- `\` 特殊 shell 字符, 249–250
- 特殊 shell 字符, 247, 250
- `[ ]` 特殊 shell 字符, 248
- `[a, z]` 特殊 shell 字符, 248
- `[a-z]` 特殊 shell 字符, 248
- `[az]` 特殊 shell 字符, 248
- `$`, 235
- `$` 内置变量, 247
- `$` 特殊 shell 字符, 247
- `##` 内置变量, 246
- `$*` 内置变量, 247
- `$0` 内置变量, 247
- `!!` 运算符, 196–197
- `!=` 运算符, 491
- `<` 特殊 shell 字符, 247
- `<<` 运算符, 236
- `<<` 特殊 shell 字符, 248
- `>` 特殊 shell 字符, 247
- `>>` 特殊 shell 字符, 247
- `|pipe)` 特殊 shell 字符, 247
- `|` 运算符, 198, 491
- `#` 特殊 shell 字符, 247
- `?` 特殊 shell 字符, 247

## Numbers（数字）

- 特殊 shell 字符, 248–249
- 特殊 shell 字符, 249
- 10BASE-T 网络, 339
- 10G 以太网网络, 340
- 32 位 Ubuntu, 64 位 Ubuntu, 4-5
- 50G 以太网网络, 340
- 64 位 Ubuntu, 32 位 Ubuntu 对比, 4-5
- 100BASE-T 网络, 339
- 1000BASE-T 网络, 339
- 在线参考, 377–378
- SSH 服务器, 371–375
- VNC, 375–377
- shell 脚本，用于全局访问, 240
- 变量值, 243
- 账户, 用户使用统计, 212
- ACID 兼容性, 关系型数据库, 493–494
- ACL 权限, 设置, 127–128
- Squid, 565–569
- 活动（用户）, 监控, 211–212
- Ada, 622
- 路由, 广播, 338
- IPv4 路由, 331–332
- IPv6 路由, 332–336
- 多组播, 338
- NAT, 332
- TCP/IP 331–332
- 单播命令, 338
- `adduser` 命令, 136–137, 209
- 管理, LDAP, 584–585, 权限, 217
- Adobe Photoshop, 67
- `afio`, 316
- 多合一（打印/传真/扫描）, 435
- `AllowOverrides` 指令（Apache Web 服务器）, 451–452

## A

- A 记录, 590
- AAAA, 590
- `ac` 命令, 211, 223
- 访问, ACL 权限设置, 127–128, Squid, 565–569
- Apache Web 服务器, 452, 455, 命令行, 107
- 数据库, 本地 GUI 客户端, 503, PostgreSQL, 501–503, SSH, 501–502, 浏览器, 503
- 文件访问时间, 禁用, 397, 网络, 387
- 远程访问, 在机器间拷贝文件, 372–373, 基于密钥的登录, 373–375
- ALSA, 64
- Amanda, 315–316
- AND, 299, AND 运算符, 491–492
- Android 开发, 705, Android Studio, 609
- Application Framework, 608–609, 应用程序, 609, `ServerRoot`, 447

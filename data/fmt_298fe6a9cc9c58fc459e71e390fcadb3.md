
当然，不要忘记移除启动 CD，否则将再次启动 CD 而不是你的 Gentoo 系统。

一旦在你的 Gentoo 安装中重启，请完成完成你的 Gentoo 安装。

## 11. 完成你的 Gentoo 安装

### 11.a. 用户管理

#### 为日常使用添加用户

在 Unix/Linux 系统上以 root 身份操作是危险的，应该尽可能避免。因此，强烈建议添加一个用于日常使用的用户。

你所属的组定义了该用户可以执行的活动。下表列出了你可能想要使用的若干重要组：

| 组 |  |
| :--- | :--- |
| audio | 能够访问音频设备 |
| cdrom | 能够直接访问光设备 |
| floppy | 能够直接访问磁盘设备 |
| games | 能够玩游戏 |
| port | 能够作为普通用户使用 --pretend |
| usb | 能够访问 USB 设备 |
| plugdev | 能够挂载和使用相机和 USB 盘等即插拔设备 |
| video | 能够访问视频硬件并进行硬件加速 |
| wheel | 能够使用 su |

例如，要创建一个名为 `john` 且属于 `wheel`、`users` 和 `audio` 组的用户，请以 root 身份登录（只有 root 可以创建用户）并运行 `useradd`：

# 代码列表 1: 为日常使用添加用户

```
Login: root

Password: (你的 root 密码)

# useradd -m -G users,wheel,audio -s /bin/bash john

# passwd john

Password: (输入 john 的密码)

Re-enter password: (重新输入密码以验证)
```

如果用户需要以 root 身份执行某些任务，你可以使用 `su -` 临时临时获得 root 权限。另一种方法是使用 `sudo` 软件包，如果配置正确，它是安全的。

## 12. 接下来该去哪里？

### 12.a. 文档

恭喜！你现在有一个可以运行的 Gentoo 系统了。接下来该去哪里？你现在有哪些选择？首先探索什么？

Gentoo 为用户提供了许多可能性，因此也有许多文档记录（以及未记录的）的功能。你应该看看手册的后续部分，它解释了如何更新软件、如何安装更多软件、USE 标志以及 Init 系统如何工作。

如果你对为桌面优化系统感兴趣，请查看文档资源。此外，你可能还想使用我们的本地化指南来让你的系统感觉更亲切。

我们还有值得阅读的 Gentoo 安全手册。

要查看所有文档的完整列表，请查看文档资源。

### 12.b. Gentoo 在线

我们非常欢迎来到 Gentoo 论坛或任何一个 Gentoo IRC 频道。

我们还有几个对所有用户开放的邮件列表列表。有关如何加入的信息包含在该页面中。

我们现在闭嘴，让你享受你的安装过程 :)

```bash
# emerge --sync
```

如果您由于防火墙限制而无法重新同步，仍然可以使用我们每日生成的 Portage 树快照来更新 Portage 树。`emergewebsync` 工具会自动在您的系统上获取并安装最新的快照：

# 代码列表 3: 运行 emerge-webresync

```bash
# emerge-webresync
```

### 1.c. 维护软件

#### 搜索软件

若要在 Portage 树中搜索软件名称，可以使用 emerge 内置的搜索功能。默认情况下，`--search` 会返回名称匹配（完全或部分匹配）给定搜索词的包名。

例如，搜索所有名称中包含 "pdf" 的包：

# 代码列表 4: 搜索包含 pdf-name 的包

```bash
$ emerge --search pdf
```

# 代码列表 5: 搜索 pdf 相关的包

```bash
$ emerge --searchdesc pdf
```

# 代码列表 6: 'emerge--search' 输出示例

```text
* net-print/cups-pdf

Latest version available: 1.5.2

Latest version installed: [ Not Installed ]

Size of installed files: 15 kB

Homepage: http://cip.physik.uni-weiersburg.de/~vrherr/cups-pdf/

Description: Provides a virtual printer for CUPS to produce files.

License: GPL-2
```

#### 安装软件

一旦您找到了喜欢的软件，就可以使用 emerge 轻松地安装它：只需添加包名。例如，安装 `gnumeric`：

# 代码列表 7: 安装 gnumeric

```bash
# emerge gnumeric
```

由于许多应用程序之间相互依赖，尝试安装某个软件包可能会导致同时安装多个依赖项。别担心，Portage 能很好处理依赖关系。如果您想知道 Portage 在您要求安装某个包时会安装什么，请添加 `--pretend` 选项。例如：

# 代码列表 8: 预装安装 gnumeric

```bash
# emerge --pretend gnumeric
```

当您请求安装一个包时，它将从互联网下载必要的源代码（如果有必要），并默认将其存储在 `/usr/port/distfiles` 中。之后，它将解压、编译并安装该包。如果您想让 Portage 只下载源码而不安装，请在 emerge 命令中添加 `--fetchonly`：

# 代码列表 9: 下载 gnumeric 的源码

```bash
# emerge --fetchonly gnumeric
```

#### 查找已安装包的文档

许多包带有自己的文档。有时，`doc` 标志决定了是否应该安装包文档。可以使用 `emerge -vp <package name>` 命令检查 `doc` 标志是否存在。

# 代码列表 10: 检查 doc 标志是否存在

```bash
(alsa-lib 仅仅是一个例子，当然。）
# emerge -vp alsa-lib
ebuid N media-lib/alsa-lib-1.0.9_rc +doc -jack 674 KB
```

您可以在 `/etc/make.conf` 文件中全局启用 `doc` USE 标志，也可以在 `/etc/portage/package.file` 中按包启用。USE 标志详细涵盖了这一方面。
一旦包安装完成，其文档将生成在 `/usr/share/doc` 下与包同名的子目录中。您也可以使用 `list` 列出所有已安装的文件。

# 代码列表 11: 定位包文档

```bash
# ls -l /usr/share/doc/alsa-lib-1.0.9_rc

total 24

-rw-r--r 1 root      669 May 17 21:54 Changelog.gz

-rw-r--r 1 root      9373 May 17 21:54 COPYING.gz

dr-xr-x 2 root      4096 May 17 21:54 hinfo

dr-xr-x 1 root      196 May 17 21:54 TODO.gz

（或者，使用 equ 定位已安装的文件）：

# query files alsa-lib | less

media-lib/alsa-lib-1.0.9_rc:

*

/usr

/usr/bin

/usr/bin/alsaisimp
(输出已截断)
```

#### 移除软件

当您想从系统中移除软件包时，使用 `emerge --unmerge`。这将告诉 Portage 从系统中移除由该包安装的所有文件。然而，您也可以使用 `--unmerge` 移除特定的包。

# 代码列表 12: 移除 gnumeric

```bash
# emerge --unmerge gnumeric
```

#### 更新系统

为了保持您的系统处于完美状态，您需要定期更新。由于安全更新也会发生，建议定期运行此命令：

# 代码列表 13: 更新您的系统

```bash
# emerge --ask world
```

如果您想更新系统上的每一个包，请添加 `--depth` 参数：

# 代码列表 14: 更新整个系统

```bash
# emerge --depth world
```

如果您更改了任何 USE 标志，您可能也需要添加 `--newuse`：

# 代码列表 15: 执行全更新

```bash
# emerge --newuse world
```

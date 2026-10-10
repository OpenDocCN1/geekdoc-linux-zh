
如果你愿意，可以将自己的脚本添加到 `periodic` 目录中。然而，正如你之前看到的，当有替代的“本地”版本可用时，避免编辑 `/etc` 中的全局文件被认为更安全、更规范。在这种情况下，`/usr/local/etc/periodic` 是你可能想要添加的任何每日、每周或每月脚本的位置。脚本会在 `/etc/crontab` 运行全局定期脚本的同时执行。例如，在执行完成 `/etc/periodic/daily` 中的脚本后，`periodic` 将在 `/usr/local/etc/periodic/daily` 中运行，其执行顺序与全局位置按字典顺序排列。

将脚本添加到 `periodic` 目录是安排持续执行特定任务的好方法——例如，清理临时目录的脚本、数据库备份过程，或同步你 FreeBSD 源码的 CVS 过程（你将在第 19 章“跟上 FreeBSD”中学习更多关于同步 FreeBSD 源码的知识）。使用 `periodic` 结构来处理这些任务，远比将它们全部全部放在一个巨大的 `crontab` 中要整洁得多、正式得多！

# 第 16 章

## 本章内容

- 软件包简介
- 安装软件包
- 移除和升级软件包
- Ports 简介
- 安装和移除 Ports
- 更新和维护 Ports
- 升级一个 Port
- Fresh Ports

# 安装额外软件

到目前为止，我们涵盖的话题大部分适用于许多不同类型的 UNIX 系统。几乎任何此类系统都是如此。当有替代的“本地”版本可用时，避免编辑 `/etc` 中的全局文件被认为更安全、更规范。在这种情况下，`/usr/local/etc/periodic` 是你可能想要添加的任何每日、每周或每月脚本的位置。脚本会在 `/etc/crontab` 运行全局定期脚本的同时执行。例如，在执行完成 `/etc/periodic/daily` 中的脚本后，`periodic` 将在 `/usr/local/etc/periodic/daily` 中运行，其执行顺序与全局位置按字典顺序排列。

每个包都有一份*依赖项*列表，其中包含了共享库和可执行文件（程序）。如果依赖项尚未安装，包系统会自动查找并安装它们，然后再继续。如果你（通过包工具）删除了某些已安装包的依赖项（程序或库），工具会提示你并拒绝继续操作。

## 获取已安装包的信息

了解包的第一步是探索你已经安装的包信息。正如你之前阅读本书的章节所提到的，你可能已经安装了一些包，或者可能在自定义安装过程中间接安装了某些包（例如，如果你在 FreeBSD 安装过程中选择了安装 X11）。如果没有，不要担心——这里的信息对你学习来说将非常有帮助。

你用于管理包的工具有 `pkg_add`、`pkg_delete`、`pkg_info`、`pkg_update`、`pkg_version` 和 `pkg_create`。每个工具的功能都符合你的预期；FreeBSD 风格的一个特点是为同一个程序使用不同名称的程序。这些工具都与位于 `/var/db/pkg` 的文件系统数据库交互，你可以通过使用 `ls` 来快速查看系统的包状态。该仓库为每个已安装的包提供一个目录，其中包含包列表（包中文件的清单）和依赖项信息。`pkg_info` 使用此数据库打印出你当前安装的每个包的描述，如列表 16.1 所示。

### 列表 16.1 pkg_info 示例输出

```
# pkg_info
ImageMagick-6.2.2.1 一个用于显示和交互式操作的 X11 包
-6.0 一个用于分析 WWW 日志文件的程序
apache-1.3.34 极其强大的 HTTP 服务器。速度极快，非常
arc-5.21j 从 DOS .ARC 文件创建并提取过滤器
aub-2.1.3 汇编二进制文件
autoconf-2.59 在许多 Unix*x 平台上自动配置源代码
dict-1.10.1 字典服务器协议 (RFC2229) 客户端
elm-2.5.8 一个曾经强大的邮件用户代理，版本 2.5.x
emacs-21.3.2 GNU 编辑宏
```

你也可以通过使用包名作为参数来获取任何单个包的大量信息，通过添加 `-v`（详细）开关获取更多信息。与 RPM 类似，FreeBSD 包的名称由连字符分隔的多个部分组成——包名，后跟版本号。然而，RPM 包倾向于多平台，并且通常在包名中包含目标程序的名称。相反，由于 FreeBSD 几乎专门用于 x86 硬件，FreeBSD 包简单地采用 `名称-版本.tbz` 的形式。这里有一个示例：

`elm-2.5.8.tbz`

包通常是 `.tbz` 文件（称为 tarballs），它是 `.tar.bz2` 的缩写。使用 tarballs 是 UNIX 下归档目录结构的传统方法——首先使用 `tar` 将目录打包成一个文件，然后使用 `bzip` 进行压缩。要使用如 `pkg_info -v` 等工具，你需要指定完整的包名（包括版本），如列表 16.2 所示。

FreeBSD 的包最近从之前的 `.tgz` (.tar.gz) 格式更改为 `.tbz` 格式，因为 `bzip2` 压缩器比传统的 `gzip` 压缩器获得更好的结果。

### 列表 16.2 pkg_info 的详细输出

```
# pkg_info -v sudo-1.6.8.6
Information for sudo-1.6.8.6:
```

Comment:

允许他人以 root 身份运行命令

Description:

这是 sudo 的 CU 版本。

sudo 是一个程序，允许管理员给用户提供有限的 root 权限并记录 root 活动。其基本哲学是尽可能少地权限，但仍允许人们完成工作。

邮件列表：

请将错误、问题、意见等发送至 sudo-bugs@couresan.com

有一个邮件列表，每当发布新版本的 sudo 时，就会接收公告。你可以通过向 "majordomomo@couresan.com" 发送包含 "subscribe sudo-announce" 行的消息来订阅它。还有一个用于开发 sudo 的人员的列表。加入的命令是 "subscribe sudo-workers"。

WWW: http://www.couresan.com/sudo/

Packing list:

```
Comment: PKG_FORMAT_REVISION:1.1
Package name: sudo-1.6.8.6
Package origin: security/sudo
CWD to /usr/local
```

### 列表 16.2 续

```
File: man/man5/sudoers.5.gz
Comment: MD5:b8c9db19cbac166acac9357b92eae94
File: man/man8/sudo.gz
Comment: MD5:027194bc1981c2d6ca4ed666c7c5f6
File: man/man8/visudo.gz
Comment: MD5:2feb0dc710522e936e9280be2df45d
File: man/man8/sudoedit.8.gz
Comment: MD5:115a715a115a115a115a115a
```

# 安装软件包

现在，你需要寻找一些想要安装的软件。。第一步是找出哪些可用软件。几乎所有适用于 Linux 的软件在 FreeBSD 上也可用——世界上几乎每一款开源软件都制成了 FreeBSD 原生端口（port），而以二进制形式分发给 Linux 的闭源软件也可以良好安装（因为二进制兼容性允许你使用 Linux 软件进行任何操作，包括播放音频/视频）。

## 从 Sysinstall 安装

如果你已经安装了 ports 集合（ports collection），你可以通过 `/usr/ports` 并直接浏览文件系统查看所有可用软件的分类视图。每个子目录代表一个同名的软件包类别，而其内部的每个端口目录则代表一个可以使用命令行工具进行安装的软件软件包。然而，你的老朋友 Sysinstall 提供了一个更加更直接的界面。

> 并不是每个端口都有对应的可用软件包。如果你在端口目录中发现了一个软件包名称并尝试安装，但它在 Sysinstall 菜单中不可用，你可能需要从端口手动构建它。更多信息请跳转到“FreeBSD Ports Tree（FreeBSD 端口树）”。

在 Sysinstall 程序的主菜单中，选择 Configure（配置）并选择 Packages（软件包）。图 16.1 显示了 Packages 菜单。从那里，如果你已经准备好了 FreeBSD DVD，选择 CD/DVD 作为安装媒体；如果没有，在网络上的请选择 FTP。

![](img/77bd66253135c18493b7c99c3f112b77_473_0.png)

图 16.1 Sysinstall 程序中的 Packages 菜单。

当你从选择的任何菜单获取软件包列表后，会看到一个类似于图 16.2 的菜单。向上或向下滚动查看各种类别，按回车键进入每个类别。

## 关于版本分支的说明

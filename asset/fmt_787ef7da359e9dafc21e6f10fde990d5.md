
`delete` 允许 CVS 移除过时的、不需要的源代码文件（`{。--suffix` 条目允许 CVS 在多个版本的源代码之间共享一个公共基目录，而不会将它们混淆。

所有示例都包含一条压缩 CVSup 数据的指令（`）`。如果您的连接是 T1 或更快，则压缩数据并不重要，您可以删除这一整行，这将减少 CPU 负载同时增加对所需带宽的需求。由于今天的处理器比带宽便宜得多，压缩有意义的情况寥寥其微。

`src-all` 告诉 CVSup 更新整个源码树（`）`）。`stable-stable` 包含一个被注释的子集合列表，例如 `/usr.bin`、`contrib`、`src` 等，它们都包含在 `src-all` 中。如果只想使用源码树的一部分，可以使用这些子集合。例如，如果您升级了 `/usr/src/usr.bin` 中的源码，可以指定 `/usr.bin` 子集合。如果您想用这些源码来升级您的系统，这将是一个极其糟糕的主意。例如，在 4.3-release 系统上安装 4.5-release 系统的 `/usr/bin` 目录会导致各种不可预知的问题，并且肯定不被支持。

### 指定多个集合

您可以在一个文件中指定多个集合。例如，我需要访问最新 -stable 版本的源代码集合。作为一名 FreeBSD 文档提交者，我需要拥有最新的文档集合。此外，我想要最新的端口树，以便在我的系统上安装最新的软件。

FreeBSD 为这些集合中的每一个都提供了独立的示例样本。我想一次性获取所有内容（我不想运行三次 CVS 来下载所有最新更改），我希望通过一个示例来获取最合适的 FreeBSD 版本、最新的端口集合和最新的文档集合，如下所示：

```
* host=cvsupl6.FreeBSD.org
*default base=/usr
*default prefix=/usr
*default delete use-rel-suffix
*default compress src-all
*default release=cvs tag=RELENG_4
src-all
v ports-all tag=
doc-all tag=.
```

倒数第二行（`v`）之前的内容都是标准的 `stable-stable`。我们可以列出我们需要的任何额外集合。

最后两个条目是有趣的部分，我在那里添加了 `ports-all` 和 `doc-all` 集合。非源代码集合不像源代码那样有版本或分支，因此如果我请求 `RELENG_4` 版本的端口树，服务器将不知道我在说什么，我也不会。

你可以将优化选项放入 `/etc/make.conf` 中（第 9 章有描述）。某些部分值得考虑 `CPPUTYPE` 条以及各种 `NO_` 标志。这可以创建一个更高效的操作系统以及更快速、更流畅的升级。

**注意**：确保 `make buildworld` 无错误地完成！如果它以你在内核编译失败时看到的错误结束，请立即停止。回到第 2 章查看如何获取帮助。在任何情况下，都不要尝试安装损坏或不完整的内核。

## 更新内核

当 `make buildworld` 成功完成后，是时候更新你的内核了。问题在于，构建内核的工具的最新二进制文件并没有实际安装；它们位于另一个目录树中！第 4 章中讨论的标准内核构建配置——`make depend`、`make install` 流程将无法正常工作。

如果你有自定义内核配置，请在 `/etc/make.conf` 中设置 `KERNCONF` 变量（第 8 章有说明）。否则，构建过程将重新构建 `GENERIC` 内核。

要构建内核，请使用 `/usr/src` 并运行此命令：

```bash
# make buildkernel
```

**注意**：为了最大的安全，请运行 `make buildkernel KERNCONF=GENERIC`，这样你有一个更新过的 `GENERIC` 内核可用。

## 安装你的系统

一旦完成了 `make buildkernel`，你就可以安装新构建的系统了。第一步是安装新内核和内核模块。

新内核和相关模块是升级中最容易测试的部分；如果出现问题，你可以轻松回退到旧内核。输入此命令安装新内核和模块：

```bash
# make installkernel
```

要测试新内核，重启并检查你的系统。你的程序仍在运行吗？你的系统仍在接收邮件并提供 Web 服务吗？如果是，那么你的内核可能没问题。当你检查系统时，某些需要访问内核结构的程序（例如 `top(1)`）将无法工作，但你可以测试其他所有内容。

一旦你确认内核正常且一切运行都符合你的预期，就可以安装系统的其余部分。用户态（Userland）安装必须在单用户模式下进行。如果你的系统运行在 `securelevel 1` 或更高，你需要关机并进入单用户模式。否则，你可以可以使用此命令将运行中的系统切换到单用户模式：

```bash
# shutdown now
```

一旦系统切换到单用户模式，你可以输入以下内容安装用户态程序：

```bash
# cd /usr/src
# make installworld
```

这将安装 FreeBSD 核心系统包含的各种程序。你将看到大量消息在屏幕上滚动，包括 `install` 一词。当进程完成时，你已经完成了升级安装，但在你的 FreeBSD 系统真正升级之前，你还有几个步骤需要完成。

## /etc 和 /dev 的更改

正如你记得的，系统的个性化配置存储在 `/etc` 下。因为没有自动化过程可以知道你的机器应该如何运行，你必须亲自处理对这些文件的任何更改。从 `make buildworld` 到 `make installworld` 的过程不会替你执行这些操作。

`/etc` 下所有文件和目录的最新版本位于 `/usr/src/etc` 下。你需要将这些文件（特别是 "rc" 文件）与你 `/etc` 目录中的文件进行比较，以查看你需要添加哪些更改。这是一个繁琐的过程，手动完成非常困难，因此我们将使用 FreeBSD 工具 `mergemaster(8)` 来大幅简化合并工作。

要使用 `mergemaster`，请变为 root 用户并输入以下命令：

```bash
## mergemaster
```

`mergemaster` 将从你的源码树拷贝各种配置文件，在 `/var/tmp` 下构建一个临时 `/etc`，然后将这些配置文件与现有 `/etc` 中的文件进行比较。如果新文件版本与 `/etc` 中的文件不同，`mergemaster` 会显示差异，此时你决定保留旧文件、使用新文件还是合并两者。

例如，这里是一个典型的 `mergemaster` 会话的开头。

```diff
+ *** Beginning comparison
+ *** Temp /dev/MAKEDEV.local and installed the same $FreeBSD, deleting
v *** Temp /dev/MAKEDEV and installed the same $FreeBSD, deleting
*** Displaying differences between /etc/defaults/rc.conf and installed version

--- /etc/defaults/rc.conf      Fri Jan 14 08:54:11 2000
+++ /etc/defaults/rc.conf      Sun Feb 27 18:21:29 2000
@@ -9,7 +9,7 @@
 # # All arguments must be in double or single quotes.
-# $FreeBSD: src/etc/defaults/rc.conf,v1.1.2.19 1999/11/28 16:02:30 brian Exp $
+# $FreeBSD: src/etc/defaults/rc.conf v1.1.2.19 2000/02/19 13:11:28 jkh Exp $
 ################# Important Boot-time options #################
@@ -10,13 +10,13 @@
 # screen saver: Use /modules/$(saver)_saver.ko
moused_enabled="NO"                    # Run the daemon.
moused_enabled="NO"                    # Run the daemon.
moused_type="auto"                     # Available for
moused_port="/dev/cua0"              # Set to your mouse port.
moused_port="/dev/psm0"              # Set to your mouse port.
fscreens=YES                          # See page for
fscreens=""                           # Delete.
```

*(注：原文中的 diff 块内容存在严重损坏/乱码，已根据标准 FreeBSD rc.conf 差异模式和上下文进行了逻辑重构)*

首先，你需要在 `/etc/make.conf` 中设置几个变量。

```
SUP_UPDATE= yes
```

上一行启用了用于连接 CVSup 的 "make" 前端。

```
SUP= /usr/local/bin/cvsup
```

`SUP` 设置是你的系统上 CVSup 的默认位置。如果你有自定义的 CVSup 替代方案，或者需要指定 `cvsup` 二进制文件的完整路径，请在此处设置。

```
SUPFLAGS=-g -L 2
```

此 `SUPFLAGS` 设置为你的 CVSup 命令提供了标准标志。若要静默运行 CVSup，请将其改为 `-g -L 0`。

```
SUPHOST= cvsup1.FreeBSD.org
```

在 `SUPHOST` 行中列出一个相当免费的 FreeBSD cvsup 镜像站。

```
SUPFILE=/usr/share/examples/cvsup/stable-supfile
```

`SUPFILE` 值告诉 CVSup 使用使用哪个配置文件。

```
PORTSUPFILE=/usr/share/examples/cvsup/ports-supfile
```

`PORTSUPFILE` 指定了应该使用哪个 supfile 来升级 ports。如果你不想升级你的 ports 集合，请不要定义此项。

```
DOCSUPFILE=/usr/share/examples/cvsup/doc-supfile
```

最后，`DOCSUPFILE` 是文档集合源码的 supfile。如果你不想升级文档树（包括手册、FAQ、文章等），请将其留为未定义状态。

注意，`DOCSUPFILE` 指定的实际文档，而是文档的源码。如果你没有文档工具，这个设置几乎是没没的。

一旦你设置了这些值，就可以将 `cvsup stable-supfile` 命令替换为此命令：

`make update`

有些人发现，直接去 `/usr/src` 并输入 `make update && makeworld && make install` 来执行完整的 CVSup 命令是一件很愉快的事。这取决于你。

[1] 这种格式被称为“diff（差异文件）”，在 UNIX 世界中非常常见。

[2]除非，当然，奇怪的熊行为、诡异的崩溃和数据丢失能让你感到快乐。

## 构建本地 CVSup 服务器

许多人拥有多个 FreeBSD 系统。然而，在从源码升级期间，每台服务器都必须连接到 FreeBSD CVS 服务器并下载最新代码，这可能非常痛苦。对于所有人来说，其中一个镜像是由捐赠服务器和带宽的志愿者维护的。为什么要重复下载相同的位流呢？

此外，如果所有服务器都连接到不同的服务器，每台服务器的代码可能会略有不同。假设你登录到每台服务器并启动 CVSup。在启动每个源码的几分钟内，CVS 服务器上的代码可能会发生细微变化。镜像不会仅仅因为你正在升级四台机器就停止更新代码，如果你正在运行几台生产机器，那么如果所有系统都完全相同，你将受益匪浅。即使你在某处运行的是 4.4-release 和 4.5-release 之间的某个 -stable 版本，任何潜在问题都能立即帮助排故障。你可不想想：“天哪，看我们一直在这样做；这会不会是因为每台服务器运行着不同版本的 FreeBSD？那太疯了。”

你可以通过运行一个中央 CVSup 服务器（作为“cvsup”服务器）来解决这个问题，这本质上是你自己的镜像。你可以控制本地镜像的更新时间，并可以保证所有镜像具有完全相同的代码。这样做不会让你受到镜像运营者的欢迎（或者至少不会让你不受他们欢迎），还将消除由于每台服务器上运行不同代码而导致的各种问题。如果你在 `/etc/mk.conf` 中有不同的设置，你仍然会遇到问题，但你可以自己比较这些文件，看看你做了哪些不同。比较两个文件比比较一千个要容易得多！

运行 CVSup 服务器并不特别容易，但有帮助可以使其变得简单。`/usr/ports/net/cvsup-mirror` 处理了配置镜像的所有棘手部分。当你安装该 port 时，`cvsup-mirror` 会在那里询问你一些问题；那里有默认建议，但你应该更改其中许多项。我们将在第 9 章详细讨论软件安装，但安装这个 port 非常直接。

首先，确保你已连接到互联网，并输入以下命令：

```
# cd /usr/ports/net/cvsup-mirror
# make install clean
```

你将看到信息在屏幕上滚动，包括你应该能识别出的编译器信息。（你可能不知道它们的意思，但你应该能认出正在编译的状态。）

在某处，安装过程将暂停并提示你提供信息：

你的更新主站点 [cvsup-master.FreeBSD.org]?

默认站点 `http://cvsup-master.freebsd.org/` 仅留供官方 FreeBSD 镜像使用；如果它成为官方镜像并且全球访问你的系统，你可以使用它。如果不是，请使用另一个公共 CVSup 服务器。如果你正在设置 CVSup 镜像，你应该已经识别出一个离你的公共镜像。输入该镜像名称。

下一个提示将如下：

你的文件更新之间间隔多少小时 [i]?

脚本会更新 `/etc/crontab`（在第9 章中解释）来自动运行 CVSup。你可以接受此默认值，也可以更改它。如果你接受默认值，系统将在一个小时的 cron 后进行自我升级。这是官方镜像的方法。我通常输入 168，即每周更新一次仓库，因为我不会频繁升级服务器。

**注意**

在许多情况下，通过运行 `/usr/local/etc/cvsup/update.sh` 手动更新 CVSup 服务器。为了让所有机器都处于相同的 -stable 变体，你需要编辑 `/etc/crontab`。

你想要镜像主仓库 [y]?

大多数人只需要主仓库，所以默认值通常是。

你希望将它放在哪里 [/home/ncvs]?

此提示要求你输入想要镜像的磁盘路径。你可以将其放在默认位置 `/home/ncvs`，不会出现任何问题。

由于你可能只需要主仓库，对以下三个问题回答 n：

你想要镜像安装的世界 [y]?

你想要镜像 GNATS 跟踪数据库 [y]?

你想要镜像邮件列表存档 [y]?

当然，如果你愿意镜像 `http://www.freebsd.org/` 站点，包括邮件列表存档，请回答 y。但警告：邮件列表存档巨大。

接下来的系列问题使用唯一的用户和组 ID。（不要使用 "nobody"、nonroot" 或 nogroup”）可以使用默认值，也可以根据本地方案更改用户名和组：

```
运行客户端的的用户 ID [cvsupin]?
运行客户端的组 ID [cvsupin]?
运行服务器的的用户 ID [cvsupup]
运行服务器的组 ID [cvsupin]?
```

最后，最大并发连接数以后可以更改，所以不用担心。接受默认值：

```
最大并发连接数 [8]?
```

一旦你回答了所有问题，`make install` 过程将从中断的地方继续，添加这些用户名、配置，并通常会让你去。

## 控制访问

即使你想成为一名优秀的系统管理员并拥有私有仓库，也不意味着你希望每个人都从你的镜像下载。CVSup 服务器允许你控制哪些计算机访问镜像。

`/usr/local/etc/cvsup/cvsupd.access` 文件控制哪些主机可以连接到你的 CVSup 镜像。井号开头的行表示注释；`(+)` 表示客户端可以连接，`(-)` 表示客户端不能连接。星号 `(*)` 表示客户端身份验证，如后文“身份验证”部分所述。

`cvsupd.access` 中的每个规则都可以引用主机名或 IP 地址：IP 地址是优选的。你也可以对 IP 地址使用掩码。

例如，允许来自 `192.168.0.0/16` 网络的访问并显式拒绝从其他地方访问的客户端，请使用这些行：

`+192.168.0.0/16`

`-0.0.0.0/0`

通过 IP 地址控制访问对于静态网络非常有益。例如，互联网服务提供商（ISP）知道其服务器的 IP 地址，并轻松地将它们保留在 `cvupd.access` 中。然而，如果你是从随机 IP 地址连接的，你可能需要一个更灵活的系统。例如，在我担任顾问期间，我曾维护一个接受来自任何 IP 地址连接的标记位。不过，用户需要用户名和密码才能连接。如果你的 `cvupd.access` 文件为空，访问将完全由用户名和密码验证进行控制。

## 身份验证

使用身份验证允许从互联网上的任何地方连接到你的 CVSup 镜像服务器。CVSup 服务器使用挑战-响应系统进行身份验证，而不是以明文传输密码。当客户端连接时，它会将它的共享密钥（作为“密码”的 `CVSup`）和系统时间结合，并通过混淆器处理。服务器也执行相同的操作。从理论上讲，客户端和服务器对同一段秘密数据执行相同的计算，并且都应该得到相同的答案。如果客户端的混淆消息与服务器计算的结果匹配，服务器就假设客户端拥有秘密数据并允许访问。

这是一个非常安全的系统。例如，如果有人在网络上投放了数据包嗅探器，它无法捕获密码。此外，由于挑战-响应系统包含了时间，被截获的响应无法被再次使用。

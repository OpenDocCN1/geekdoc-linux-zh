

## CSUP、CVSUP、CVS、SUP 和 CTM？

遗憾的是，互联网上的文档往往在毫无逻辑的情况下长期存续，并在最不恰当的时刻制造混乱。过时的 FreeBSD 文档和第三方教程可能会提及使用名为 `CVS` 或 `CVSup` 的工具来更新源代码。这些工具已在 2013 年被取代。任何提及这些程序的地方都表明你正在阅读旧文档。如果你看到关于 CTM 的提及，说明你阅读的是比 CVS 更早的文档。

从源码升级需要控制台访问权限。虽然你并非总是需要它，但在恢复失败的构建时，可能需要你在键盘上进行干预。在安装你自行构建的操作系统版本之前，请测试你的串行控制台、Java 应用程序或 IPMI 控制台。根据我的经验，唯一需要控制台访问权限的升级，恰恰是那些我没有控制台访问权限的情况。

### 哪些源代码？

每个 FreeBSD 版本都附带了用于构建你所安装系统的源代码。如果安装系统时你未选择安装源代码，你可以在安装介质中的 `/usr/freebsd-dist/src.txz` 找到它。如果你已经安装了源代码，它位于 `/usr/src`。

不幸的是，这个版本的源代码缺乏构建 FreeBSD 所需的版本控制标签。它仅供参考。你需要使用 svnlite(1) 下载一个保留这些标签的代码版本。

`/usr/src` 中的源代码副本适合用于构建 FreeBSD 吗？问 svnlite(1)。

```
# svnlite info /usr/src
svn: E155007: '/usr/src' is not a working copy
```

“不是工作副本”的错误意味着这里的任何源代码都无法与 Subversion 配合使用。

获取源代码的 svnlite(1) 命令如下所示。

```
# svnlite checkout \*svn.freebsd.org/@repository/@branch @locadir
```

Mirror 是一个 FreeBSD Subversion 镜像。svn.FreeBSD.org 镜像是一个地理位置路由的别名，指向最近的 Subversion 镜像。

Repository 是你正在处理的代码组。你可以在 https://svnweb.FreeBSD.org/ 获取当前仓库的完整列表。主要项目仓库包括：base（用于操作系统）、doc（用于文档）和 ports（用于 Ports Collection）。

Branch 是你想要的 FreeBSD 版本。为了获取最新的、指尖笨拙的 current 版本，请使用 head。要获取稳定版本，请使用 stable/ 后跟主要发行版本号。FreeBSD 12-stable 即 stable/12。要获取发行版加上当前所有补丁，请使用 releng/ 后跟发行版编号。完全修补的 FreeBSD 12.2 位于 releng/12.2。

如果你难以确定需要哪个分支，不妨浏览 https://svnweb.freebsd.org/。分支字面上告诉 svnlite(1) 从该站点抓取哪个子目录。

最后，locadir 是我希望存放源代码的本地目录。

这台主机运行的是 FreeBSD 11.1。我想要冒险一点，升级到 FreeBSD 11-stable。以下是我的操作方法：

```
# svnlite checkout https://svn0.us-east.FreeBSD.org/base/stable/11 /usr/src/

Error validating server certificate for 'https://svn0.us-east.freebsd.org:443':
  - The certificate is not issued by a trusted authority. Use the
    fingerprint to validate the certificate manually!
Certificate information:
  - Hostname: svn0.freebsd.org
  - Valid: from Jul 29 22:01:21 2013 GMT until Dec 13 22:01:21 2040 GMT
  - Issuer: svn0.freebsd.org, clusteradm, FreeBSD.org, CA,
    US(clusteradm@freebsd.org)
  - Fingerprint: 1C:BD:85:95:11:9F:EB:75:A5:4B:C8:A3:FE:08:E4:02:73:06:1E:61
(R)eject, accept (t)emporarily or accept (p)ermanently? p
```

这是什么新的疯狂举动？我们试图获取 FreeBSD 源代码，结果却遇到了证书错误？

将显示的证书指纹与 FreeBSD.org 网站上的服务器指纹进行对比。如果匹配，请输入 p 永久接受证书。源代码文件的文件名将从你的终端流过。

svnlite(1) 完成后，查看一下 `/usr/src`。

```
# ls /usr/src/
COPYRIGHT	cddl	sbin
LOCKS	contrib	secure
MAINTAINERS	crypto	share
Makefile	etc	sys
Makefile.inc1	gnu	targets
Makefile.libcompat	include	tests
Obsoletedfiles.inc	kerberos5	tools
README	lib	usr.bin
README.md	libexec	usr.sbin
UPDATING	release	
bin	rescue
```

这是 FreeBSD 源树的顶层目录，其中包含了构建你所选 FreeBSD 版本所需的所有代码。

## 更新源代码

所以你昨天构建了 FreeBSD？很酷。但现在你想构建今天的版本。

好消息是，Subversion 只需更新你已下载的代码，而无需重新下载整个源代码树。更好的消息是，源代码在 .svn 目录中记录了你的获取来源以及它本应来自哪个分支。这使得更新比初始下载简单得多。

FreeBSD 已将 Subversion 命令集成到源代码中。你所需要做的只是在 /etc/src.conf 中设置 SVN_UPDATE，告知系统它可以调用 svnlite(1) 进行更新。

```
# echo 'SVN_UPDATE=yes' >> /etc/src.conf
```

现在运行 `make update` 以获取最新的源代码。

```
# cd /usr/src
# make update
```

你会看到类似的更新流过。不过，这些更新会比最初的下载快得多。

## 从源码构建 FreeBSD

一旦你获得了最新的源代码，请查看 /usr/src/UPDATING。该文件的开头按倒时间顺序列出了关于 FreeBSD 变更的警告和特别通知，这些内容对从源码构建的人特别有用。这些说明会告诉你，在重建系统之前是否必须采取某些特定措施，或者是否有重大系统功能发生了变更。如果你希望系统在升级后正常工作，请严格按照这些说明操作。

UPDATING 文件的末尾提供了从源码构建 FreeBSD 的官方说明。本书中描述的步骤自 FreeBSD 6-current 以来一直使用，与 5-current 相比变化微乎其微，但我仍建议你将书中的说明与 UPDATING 中的内容进行双重核对。

如果你使用自定义内核，请也检查新的 GENERIC 或 NOTES 内核配置文件，查看是否有新的选项或有趣的内核变更。

> 自定义你的 FreeBSD 构建
> 回想一下第 16 章，当我们讨论 /etc/make.conf 时？FreeBSD 使用单独的文件来处理构建 FreeBSD 本身的自定义设置。虽然 /etc/make.conf 中的设置会影响系统中构建的所有软件，但 /etc/src.conf 中的任何内容仅影响从源码构建 FreeBSD。

如果你在 FreeBSD 社区待上一段时间，你会听到各种关于人们使用特殊方法构建 FreeBSD 的故事。你会听到轶事证据，证明某种方法比标准方法更快、更高效，或者以某种神秘的方式“更好”。虽然你当然可以自由选择任何你喜欢的构建方法，但 FreeBSD 项目支持的唯一方法是记录在 `/usr/src/UPDATING` 末尾的方法。如果你遵循其他程序并遇到困难，你将被引导去参考已文档化的程序。

## 构建 World

首先，构建新的用户空间：

```
# cd /usr/src
# make buildworld
```

`make buildworld` 命令从源码构建构建系统编译器所需的基本工具，然后构建编译器及相关库。最后，它使用新工具、编译器和库来构建核心 FreeBSD 安装中包含的所有软件。（这很像从“挖掘铁矿石”这样的指令开始构建汽车。）buildworld 将其输出放置在 `/usr/obj` 下。根据硬件不同，可能需要一到几个小时。如果你的硬件足够强大，当 buildworld 运行时，你可以继续正常工作；虽然构建消耗系统资源，但它不会占用你的注意力。

当 buildworld 完成后，确认其没有错误完成。如果构建结束时出现一堆类似于内核编译失败时的消息，请勿继续升级。如果你无法弄清楚构建失败的原因，请前往第 1 章查看如何获取帮助。切勿尝试安装损坏或不完整的升级。

### 并行 MAKE WORLD

经验丰富的系统管理员可能已经使用过 `make(1)` 的 `-j` 标志来提高构建速度。这会启动多个构建


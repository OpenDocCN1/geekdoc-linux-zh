
此端口名为 `apache`，处理 2.2.4 版本。它是该版本的第二个修订，它将出现在 `/var/db/pkg` 中，名为 `apache-2.2.4_2`。FreeBSD 将此端口放在 `/usr/ports/www`。`MASTER SITES` 变量通常列出更新使用的镜像列表的互联网站点。不需要每次 Apache 添加或删除镜像都更新几十个端口，Ports Collection 定义了一个包含镜像列表的内部变量，因此只需在一个处进行更新。

在 `Makefile` 的后续部分，你会找到维护者的电子邮件地址、端口的简要描述等。然后你会发现如下条目：

```
.if defined(WITH_EXCEPTION_HOOK)
CONFIGURE_ARGS+= --enable-exception-hook
.endif

.if defined (WITH_LDAP) || defined (WITH_LDAP_MODULES)
USE_OPENLDAP=
  --with-ldap \
  --with-ldap-lib="${LOCALBASE}/lib" \
  --with-ldap-include="${LOCALBASE}/include
.endif
```

`.if defined` 语句是端口的构建选项。此示例中的第一行是你需要以设置此功能的变量。我知道异常钩子是什么，坦白说，我并不在乎。你对 Apache 非常熟悉，但你可能非常在意这一点。FreeBSD 为你提供了一种简单的方法在构建时添加此功能。同样，如果你使用 LDAP 支持，在编译 Apache 时在命令行上定义 `WITH_LDAP=YES`，当你构建该端口时，它会要求 OpenLDAP 作为依赖项。

这很麻烦吗？是的。但替代方案是查看原始软件发行版，学习该特定软件作者希望如何配置这些设置。确实，经验丰富的系统管理员知道如何为他们喜爱的软件这样操作。但他们不知道如何对 Ports Collection 中 17,000 多个软件包进行操作。

如果你使用 `make install` 的子命令来构建端口（例如 `make patch` 和 `make install`），你必须在每个 `make` 命令中包含你想要的所有任何选项。否则，端口可能无法正确构建。例如，如果你想构建带有 LDAP 支持的 Apache，但要在安装之前应用自定义补丁，请运行：

```
# make patch WITH_LDAP=YES
```

应用补丁后，运行：

```
# make install WITH_LDAP=YES
```

否则，你虽然带有需要 LDAP 的自定义选项对软件打了补丁，但你实际上并没有以带有 LDAP 支持的方式构建它。你的软件在内部将是不自洽的。

自定义软件构建中最困难的部分是决定你想要哪些选项。遗憾的是，这个问题没有简单的答案，所以最好检查软件手册或网站来帮助你做决定。我曾多次安装了某件软件，然后用正确的选项重新安装了它。

## 卸载与重新安装

安装端口的一点是，已安装的端口被视为一个包。你可以使用 `pkg_delete(1)` 卸载端口，并通过 `pkg_info(1)` 了解相关信息。由于端口的信息记录在 `/var/db/pkg` 下，你也会内容文件并调查端口包含的每一个文件。

你也可以从端口目录卸载端口。例如，FreeBSD 包含了多个不同版本的 Apache Web 服务器。你可能需要评估几个不同的版本，并反复安装和卸载。在端口目录运行 `make install` 会将程序从主系统中删除。

卸载端口后，编译后的程序和源文件仍存在于端口下的 `work` 子目录下。运行 `make reinstall` 将重新安装已卸载的程序。你可以根据需要无限次卸载和重新安装。

## 跟踪端口构建状态

Ports Collection 如何跟踪已经完成了哪些工作？如果你运行 `make extract` 然后运行 `make install`，FreeBSD 如何知道它已经完成？Ports Collection 使用隐藏文件来记录已完成的操作。你可以对端口目录进行“长列表”查看看到：

```
# cd /usr/ports/games/oneko/work

# ls -la

total 502

-rw-r--r-- 1 root wheel 0 Apr 22 14:59 .build_done.oneko._usr_X11R6

-rw-r--r-- 1 root wheel 0 Apr 22 14:59 .configure.done.oneko._usr_X11R6

-rw-r--r-- 1 root wheel 0 Apr 22 14:59 .extract_done.oneko._usr_X11R6

-rw-r--r-- 1 root wheel 0 Apr 22 14:59 .install_done.oneko._usr_X11R6

-rw-r--r-- 1 root wheel 0 Apr 22 14:59 .patch_done.oneko._usr_X11R6
```

以点开头的文件名是隐藏文件，它们不会出现在普通的目录列表中。Ports Collection 使用这些文件来跟踪构建过程处于哪个阶段。每个端口都会使用这些文件。查看 `.install_done.oneko._usr_X11R6`，这意味着安装过程已经完成。

在多次 `make install/uninstall` 循环后，我曾多次遇到端口拒绝重新安装自己的情况。这通常是由隐藏文件指示安装已完成导致的。删除该文件，重新安装就可以继续进行。

## 清理端口

端口可能会占用大量空间。像 Xorg 这样的软件可能会占用数百兆字节，而 OpenOffice 构建时需要近几个 GB 的空间！Ports Collection 包含一种方法来移除你不再使用的预安装文件。

一旦你按要求安装并配置了程序，就不再需要源码副本或用于构建软件的中间文件了。你可以通过 `make clean` 移除它们。这会删除当前端口及其所有依赖的 `work` 目录，因此在执行此操作之前，请确保你对新程序满意。可以在安装时立即运行 `make install clean` 来实现。

你可能还想移除原始的 `distfiles`，它们存储在 `/usr/ports/distfiles`。`make distclean` 命令会移除当前端口和所有依赖的 `distfiles`。

要清理整个 ports 树，请直接在 `/usr/ports` 中运行 `make -DNOCLEANDEPENDS`。但这需要一些时间，对于许多用户来说……

## 构建软件包

如果你有很多运行 FreeBSD 的系统，你可能希望构建包而不是在每台机器上进行编译。这节省了时间并确保了所有配置一致。如果你使用 ports 来创建包，FreeBSD 会在端口目录下创建一个包。

## 修改安装路径

如果你有很多运行 FreeBSD 的系统，你可能希望构建包而不是在每台机器上进行编译。这节省了时间并确保了所有配置一致。如果你使用 ports 创建包，FreeBSD 会在端口目录下创建一个包。

## 永久设置选项

如果你厌倦了构建端口时输入相同的选项，可以将它们列在 `etc.conf` 中，因为 `make (1)` 会将文件中的任何选项应用于端口。如果一个变量对软件没有意义，包含它也没有。

## 本地 distfile 仓库

如果你有多台维护端口的机器，最好是创建一个本地 distfile 仓库。你可以从一台机器上从互联网下载 distfiles，然后其他机器通过局域网访问这些文件，从而加快构建并减少外部带宽使用。将环境变量 `MASTER_SITE_OVERRIDE` 设置为中心 distfile 仓库的位置；现在当你构建端口时，系统会首先检查那里。这可以是本地匿名 FTP 服务器，甚至是 NFS 共享路径。

## 端口与包的安全

跟踪端口安全性是很困难。每个软件供应商都有自己处理安全问题的流程。端口的更新可能意味着存在安全问题，也可能意味着有新版本可用。你如何知道哪些端口是不安全的？

FreeBSD 提供了 `portaudit(1)`，这是一个将你的端口与漏洞数据库进行对比的工具。如果在端口发现了安全问题，FreeBSD 团队会更新 portaudit 安全数据库以描述该问题。当你下次运行 `portaudit(1)` 时，就会收到该通知。先安装 portaudit：

```
# cd /usr/ports/ports-mgmt/portaudit

# make all install clean
```

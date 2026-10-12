
### 列表 18.11 继续

```
#           already existing logins from the bindery (this will also
#           reset all the passwords to "DEFAULT_PASSWORD")
#
# DEFAULT_PASSWORD: the common password for all automatically created
# logins (only needed if FLAG is not "0"); everything about
# password in section 12 applies to this.
#
# .....................................................................

15  99  top-secret
```

第 15 节用于指定 Linux 用户到 NetWare 用户的自动映射。随附的 Red Hat 配置文件会导致每次重启 mars_nwe 服务器时都进行用户映射。从注释中你还可以了解到，密码每次都会重置为提供的默认密码。这远非最优，建议将标志值从 99 改为 0，如 IPX-HOWTO 中推荐的那样。

mars_nwe 服务器可以配置为在启动时执行一系列健全性检查。列表 18.12 显示了配置文件中的这一节，在 Red Hat 提供的文件中，该标志已设置。

### 列表 18.12 /etc/nwserv.conf 文件第 16 节—启动时健全性检查

```
# ====================================================
# Section 16: Tests on startup
#
# If you want some sanity checks at startup, set this flag to 1.
# "mars_nwe" will try to create missing directories (with the "right"
# permissions, of course) if you enable this.
#

16  1
```

是否启用此选项取决于个人喜好。如果你习惯服务器在运行时为你创建缺失的目录，则打开启动测试。如果你宁愿让系统失败并强制你纠正情况，则将其设为零。

第 21 节是大多数管理员感兴趣的配置文件的最后一节。本节在列表 18.13 中显示，定义了你希望 IPX 客户端能够访问的任何打印机。语法相当基础，如注释中所述。

### 列表 18.13 /etc/nwserv.conf 文件第 21 节—打印队列定义

```
# =================================================================
# Section 21: print queues (optional)
#
# Which of the printers connected to your Linux-box should be accessible
# from the DOS-clients?
# Multiple entries are allowed.
#
# .................................................................
#
# Syntax:
#
#   21      QUEUE_NAME      QUEUE_DIR      PRINT_COMMAND
#
# QUEUE_NAME: the name of the print queue on client-side (to make it
#             perfectly clear: _not_ the Linux-queue)
# QUEUE_DIR: spooling directory for the print-jobs; this directory must
#            exist before printing (_not_ the spooling-directories of
#            the Linux-lpd)
# PRINT_COMMAND: command used for serving the print-jobs under Linux
#                 (see "man lpr" and "man magicfilter" for details)
#
# Examples:
#   21      LASER      SYS://PRINT/L      lpr -Plaser
#   21      OCTOPUSS   SYS://PRINT/O      lpr -Php_deskjet
# .................................................................
21   LP   SYS://PRINT/LP   lpr
```

配置文件中还有许多其他部分，然而其中大部分与本讨论无关。它们在 /etc/nwserv.conf 文件的注释中有所描述，我鼓励你研究它们。这些部分定义了软件使用的各种文件的路径、调试选项以及服务器运行的其他方面。

## 启动 mars-nwe 服务器

现在你有了配置文件，可以准备启动服务器了。在你的 Red Hat 系统上，你可以通过使用位于 /etc/rc.d/init.d 的 mars-nwe 脚本按如下方式执行：

```
/etc/rc.d/init.d/mars-nwe start
```

假设没有发出错误消息，你应该通过尝试从网络上的 IPX 客户端连接来测试你的服务器。假设连接成功，你还应该从同一 IPX 客户端创建打印捕获并测试打印。此测试可以通过多种方式进行。最简单的方法之一是使用本章前面关于将 Linux 用作 NetWare 客户端的信息来尝试连接到你的 mars_nwe 服务器。另一个选项，如果你将 Linux 用作现有 NetWare 环境中的额外 NetWare 服务器，则可以尝试从已配置适当 NetWare 客户端软件的客户端连接。如果两者都不可行，你必须从头开始配置客户端。执行此操作的细节应包含在你的客户端软件文档中，超出了本文的范围。

必须记住，使 Linux 能够在 NetWare 环境中充当客户端或服务器的软件仅使用绑定模式。如果你的 NetWare 环境基于 Novell 目录服务（NDS）实现服务，这通常适用于围绕 Novell 版本 4 或更高版本构建的网络，这里描述的实用程序将无法工作。然而，如果你只需要客户端服务，并非一切都丢失，因为 Caldera 为 Linux 提供了一套支持 NDS 的 NetWare 客户端。有关于此客户端软件的更多信息，请访问 Caldera 网站 http://www.caldera.com/。

在从客户端和服务器两个角度介绍了 NetWare 环境中的 Linux 后，我们现在可以转向本章涵盖的另一个网络操作系统环境，AppleTalk。

## Linux 在 AppleTalk 环境中

与 NetWare 连接软件不同，与 AppleTalk 网络共享资源所需的软件包未包含在 Red Hat 发行版 CD 上，但可从 Red Hat contrib ftp 站点获得。你需要的软件包是

```
ftp://contrib.redhat.com/libc6/i386/netatalk-1.4b2+asun2.1.0-5.1386.rpm
```

你可以使用以下命令安装它：

```
rpm -i netatalk-1.4b2+asun2.1.0-5.1386.rpm
```

netatalk 软件包是由密歇根大学研究系统 Unix 小组开发的 AppleTalk 协议套件的实现。它可在多种 UNIX 系统以及 Linux 上运行。有关更多信息、补丁以及访问该软件包开发人员的途径，请参阅 netatalk 主页 http://www.umich.edu/~rsug/netatalk/。

本节介绍与网络上的 AppleTalk 客户端共享资源的先决条件，首先是内核所需的修改，然后是配置文件和打印服务的步骤。

## 配置内核 AppleTalk 支持

如果你运行的是随 Red Hat 6.0 安装介质提供的默认内核，则无需修改内核，因为尽管 Red Hat 未包含 netatalk 软件包，但他们已编译了 AppleTalk 协议的支持。你可以通过检查 /lib/modules/2.2.5-15/misc 目录下是否存在 appletalk.o 模块来验证此支持是否可用。然而，如果你已更新内核，则需要自行添加 AppleTalk 支持。

这是通过回答配置问题“Appletalk DDP”为“是”来完成的，这会导致在你的内核 .config 文件中设置 CONFIG_ATALK 变量。此代码可以集成到内核中，也可以作为模块构建，后者是首选方法，因为它允许根据需要加载或卸载支持。假设你将 AppleTalk 支持作为模块构建，然后你可以使用 insmod 命令加载它：

```
insmod appletalk
```

这应导致记录一条消息，说明已加载的 AppleTalk 驱动程序的版本。

## 在 Linux 上配置 AppleTalk 服务

确保你的内核中具有 AppleTalk 支持并已安装 netatalk rpm 后，你现在可以开始配置希望在 Linux 系统上为网络上的 AppleTalk 客户端提供的服务。这将涉及五个文件的工作，其中四个特定于 netatalk 软件包，第五个是 /etc/services 文件。因为它是最容易处理的文件，我们将从 /etc/services 开始。

为了让 AppleTalk 客户端连接到你的系统，你必须在 /etc/services 文件中定义多个服务。默认情况下，这些服务已存在，你只需验证它们即可。列表 18.14 显示了确保你的 /etc/services 文件正确设置以支持 netatalk 的步骤。

### 列表 18.14 确保系统文件中对 AppleTalk 服务的支持

```
[tschenk@madmax chapter18]$ cd /etc

[tschenk@madmax /etc]$ grep ddp /etc/services
rtmp 1/ddp # Routing Table Maintenance Protocol
nbp 2/ddp # Name Binding Protocol
echo 4/ddp # AppleTalk Echo Protocol
zip 6/ddp # Zone Information Protocol

[tschenk@madmax /etc]$ grep 548 /etc/services
```

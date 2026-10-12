
## /etc/rc.d/rc.serial

与 rc.local 脚本类似，rc.serial 通常在运行级别 1 或 3 结束时运行一次，以初始化串行端口。

## Managing init Files

管理 init 文件

随 Red Hat Linux 提供的 init 版本使用了大量文件、符号链接和目录。本节讨论了一些更常用的工具，它们有助于简化 init 文件的管理。

## Managing run levels with chkconfig

使用 chkconfig 管理运行级别

chkconfig 实用程序使您能够维护在运行级别中启动或停止服务所需的各种符号链接。chkconfig 可以管理 /etc/rc.d/init.d 目录中所有脚本的运行级别配置。以下各节将向您展示如何使用 chkconfig。

## Listing manageable services

列出可管理的服务

要查看在每个运行级别中将启动或停止的服务以及它们在哪个运行级别启动或停止，请运行以下命令

```
chkconfig --list
```

此命令列出您可以使用 chkconfig 管理的所有服务，并告诉您在每个运行级别中哪些服务将被启动（打开）或停止（关闭）。您还可以通过从命令行指定服务名称（即 /etc/rc.d/init.d 中的脚本名称）来检查特定服务的运行级别配置。例如：

```
chkconfig --list httpd
```

前述命令显示了我 Red Hat Linux 服务器的以下输出：

```
httpd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

正如您所见，httpd 服务在运行级别 3、4 和 5 中处于开启状态，在 0、1、2 和 6 中处于关闭状态。

## Adding a new service

添加新服务

如果您刚刚在 /etc/rc.d/init.d 目录中添加了新脚本，并且希望使其提供的服务可用于特定运行级别，可以按如下方式运行 chkconfig 命令：

```
chkconfig --add service_name [--level runlevel]
```

例如，以下命令将名为 named 的服务添加到当前运行级别：

```
chkconfig --add named
```

换句话说，前述命令在当前运行级别目录中创建一个符号链接，该链接以 S {two-digit number} 为前缀，指向 /etc/rc.d/init.d/named 脚本。如果您想将服务添加到除当前运行级别之外的运行级别，可以使用 --level 选项指定所需的运行级别。例如，以下命令将 named 服务添加到运行级别 4：

```
chkconfig --level 4 --add named
```

## Deleting an existing service

删除现有服务

要从运行级别中删除现有服务，请使用以下命令：

```
chkconfig --del service_name [--level run_level]
```

例如，以下命令从当前运行级别中删除 named 服务：

```
chkconfig --del named
```

要从除当前运行级别之外的运行级别中删除服务，请使用 --level 选项。例如，以下命令从运行级别 5 中删除 named 服务：

```
chkconfig --del named --level 5
```

## Managing run levels with ntsysv

使用 ntsysv 管理运行级别

ntsysv 实用程序使您能够通过简单的菜单界面在任何运行级别中打开或关闭各种服务。当您不带任何参数运行该命令时，它会显示一个菜单屏幕。此可滚动菜单屏幕显示当前运行级别中所有服务的状态。要打开服务，您需要选择它；要关闭服务，只需取消选择它。完成所有更改后，您可以通过单击 OK 按钮保存更改，或通过单击 Cancel 按钮放弃更改。如果您想处理不同的运行级别配置，只需使用 --level 选项运行 ntsysv 命令并指定运行级别。例如，以下命令让您处理运行级别 1 的配置：

```
ntsysv --level 1
```

## Managing run levels with Linuxconf

使用 Linuxconf 管理运行级别

您还可以使用 Linuxconf 实用程序来配置运行级别。为此，请执行以下步骤：

- 1. 选择 Control ↩ Control Panel ↩ Control Service 活动选项。
- 2. 启用或禁用一个或多个服务。
- 3. 接受更改。
- 4. 在退出 Linuxconf 之前激活更改。

## Creating a new service for a run level

为运行级别创建新服务

如果您从知名厂商安装服务器软件包，最有可能的是它们会为您提供一个不错的 RPM 包，其中还包括放入 /etc/rc.d/init.d 的必要服务脚本。然而，有时您会发现一些有用的软件不带易于使用的安装程序和所有花哨的功能，您最终不得不自定义软件或至少修改其在系统上的工作方式。在这种情况下，您可能需要为新软件创建服务脚本。

在本节中，我将向您展示如何轻松创建新的服务脚本以放入 /etc/rc.d/init.d 目录。首先，查看 /etc/rc.d/init.d 目录中的现有服务脚本。列表 4-2 显示了这样一个名为 httpd 的脚本，用于启动和停止 Apache Web 服务器。

## Listing 4-2 An example /etc/rc.d/init.d/httpd script

列表 4-2 一个示例 /etc/rc.d/init.d/httpd 脚本

```
#!/bin/sh
#
# Startup script for the Apache Web Server.
#
# chkconfig: 345 85 15
# description: Apache is a World Wide Web server. \
#               It is used to serve HTML files and CGI.
# processname: httpd
# pidfile: /var/run/httpd.pid
# config: /etc/httpd/conf/httpd.conf

# Source function library.
. /etc/rc.d/init.d/functions

# See how we were called.
case "$1" in
    start)
        echo -n "Starting httpd: "
        daemon httpd
        echo
        touch /var/lock/subsys/httpd
        ;;
    stop)
        echo -n "Shutting down httpd: "
        [ -f /var/run/httpd.pid ] && {
            kill `cat /var/run/httpd.pid`
            echo -n httpd
        }
        echo
        rm -f /var/lock/subsys/httpd
        rm -f /var/run/httpd.pid
        ;;
    status)
        status httpd
        ;;
    restart)
    $0 stop
    $0 start
    ;;
    reload)
        echo -n "Reloading httpd: "
        [ -f /var/run/httpd.pid ] && {
            kill -HUP `cat /var/run/httpd.pid`
            echo -n httpd
        }
        echo
        ;;
    *)
        echo "Usage: $0 {start|stop|restart|reload|status}"
        exit 1
esac

exit 0
```

前述 sh 脚本实际上是一个简单的 case（条件）语句。以下列表向您展示了如何从现有服务脚本创建新服务脚本的示例。假设您的新服务名为 webmonitor，并且可执行文件存储在 /usr/sbin/webmonitor 中。根据需要为自己的脚本更改这些值。

![](img/9eb7e89292d2f85707b4d49102c865b7_112_0.png)

> 使用相同的名称作为脚本和可执行程序是标准做法。

以下是如何从 /etc/rc.d/init.d 目录中的现有脚本创建 /etc/rc.d/init.d/webmonitor 脚本：

- 1. 从 /etc/rc.d/init.d 复制现有脚本作为 /etc/rc.d/init.d/webmonitor。为简单和易于理解，我假设您复制了列表 4-2 中显示的 /etc/rc.d/init.d/httpd 脚本。
- 2. 使用您喜欢的文本编辑器（如 vi），搜索并将所有 “httpd” 实例替换为字符串 “webmonitor”。
- 3. 如果您将可执行文件保存在 `/sbin`、`/usr/sbin`、`/bin` 或 `/usr/bin` 以外的任何目录中，请更改 daemon webmonitor 行以反映 webmonitor 可执行文件的路径。例如，如果您将可执行文件保存在 `/usr/local/web/bin` 目录中，您必须将 daemon webmonitor 行更改为 daemon `/usr/local/web/bin/webmonitor`。
- 4. 如果 `/usr/sbin/webmonitor` 未创建 PID 文件（`/var/run/webmonitor.pid`），您必须将 kill `cat /var/run/webmonitor.pid` 行替换为 killproc webmonitor 并删除 rm -f `/var/run/webmonitor.pid` 行。
- 5. 运行 chmod 750 `/etc/rc.d/init.d/webmonitor` 以更改文件权限，使 root 用户可以读取、写入和执行脚本。
- 6. 使用 chkconfig、ntsysv 或 Linuxconf 实用程序将此新服务添加到所需的运行级别，如本章前面各节所述。

## Chapter 5

第 5 章

## Configuring the X Window System

配置 X Window 系统

## IN THIS CHAPTER

本章内容

- Knowing what XFree86 is
- Preparing your system for XFree86
- Installing XFree86
- Configuring XFree86

- 了解 XFree86 是什么
- 为 XFree86 准备系统
- 安装 XFree86
- 配置 XFree86

X Window 系统是一个硬件无关的客户端/服务器窗口系统，为 GNOME 和 KDE 等图形用户界面（GUI）提供基础平台。使用 GUI，您甚至可以使用 WINE 等软件模拟器在 X Window 系统下运行 Microsoft Windows 应用程序。

X Window 系统是斯坦福大学、施乐公司和麻省理工学院（MIT）等许多著名计算机研究机构研究和开发的最终成果。MIT 于 1984 年作为名为 Athena 的项目的一部分发布了 X Window 系统的一个版本。X Window 系统目前由 Open Group 开发和分发。X Window 系统通常被称为 X Windows，或简称为 X。本章中我使用了这两个术语。

在本章中，我讨论了如何在 Red Hat Linux 系统上设置 X。我还向您展示如何安装和配置 XFree86，它是 X Window 系统最常用的版本，也是通常与 Red Hat Linux 一起使用的版本。我还将向您展示如何使用各种工具自定义和个性化 X Window 环境。

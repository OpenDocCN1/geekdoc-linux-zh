

## Slackware
`/etc/rc.d/rc.4` 文件控制 X 的启动，包括启动 XDMCP 服务器。该文件测试这三个主要服务器是否存在，并启动它找到的列表中第一个，使用 GDM、KDM，然后是 XDM 的顺序。你必须移除排名较高的服务器，移除它们的执行位，或编辑启动脚本文件以改变哪个启动。

## OpenSUSE
`/etc/sysconfig/displaymanager` 文件设置了几个与 XDMCP 操作相关的变量，包括 `DISPLAYMANAGER` 变量，该变量指定要使用哪个服务器。将此变量设置为适当的名称，例如使用 KDM 时设置为 “kdm”。

在实践中，XDM 是最简单的显示管理器；它仅提供一个登录提示。KDM 和 GDM 都支持额外的用户选项，例如选择运行哪个桌面环境。它们也可能提供关机选项等，尽管这些通常对所有非本地用户都是禁用的。KDM 配置基本上是 XDM 配置的超集，但 GDM 使用其自己独特的配置文件。GDM 缺乏 XDM 和 KDM 的一些基于 IP 的审计功能，因此如果你使用 GDM，你应该特别谨慎地设置防火墙，以防止外部计算机访问 XDMCP 端口（UDP 端口 177）。

在某些情况下，特定的服务器在某些系统或发行版上可能非常挑剔。如果你遇到问题导致某个服务器无法工作，请尝试另一个。它可能比默认服务器更容易修改以接受远程登录。

在所有情况下，更改 XDMCP 配置后，你必须重新启动服务器。理论上，向进程传递 `SIGHUP` 信号应该能完成工作，但实践中这有时不起作用。（阶段 3 描述了通过 `k11` 实用程序向进程传递信号。）你可能需要注销，切换到文本模式运行级别（在大多数发行版上输入 `telinit 3` 应该可以做到；Debian 和 Gentoo 是两个例外），然后返回 GUI 登录运行级别（大多数发行版为 5，但 Slackware 为 4）。在某些发行版中，例如 Gentoo 和 Debian，你可以通过其 SysV 初始化脚本重启 XDMCP 服务器，例如先执行 `/etc/init.d/xdm stop` 然后执行 `/etc/init.d/xdm start`。此操作将终止你的 X 会话，因此在此操作前请关闭所有程序。

在所有情况下，XDMCP 通常仅在系统配置为启动 X 并在控制台上显示 GUI 登录屏幕时运行。如果你想配置系统以接受来自远程用户的 XDMCP 登录但不在本地运行 X，你可以这样做；然而，你必须如以下章节所述修改 XDMCP 配置。

## 配置 XDM

配置 XDM 以接受远程登录从 `/etc/X11/xdm-config` 文件开始。关键更改在以下行中，该行通常出现在文件末尾附近：

```
DisplayManager.requestPort: 0
```

此行告诉 XDMCP 不要监听其常规端口。这种配置在管理本地 X 服务器更直接的工作站上很常见。将此行中的 0 更改为 177，或在行首添加井号 (#) 或感叹号 (!) 注释掉该行。

除了 xdm-config，你还必须编辑 /etc/X11/xdm/Xaccess 文件，该文件控制哪些 XDMCP 客户端可以访问 XDMCP 服务器。该文件可能包含如下的行，但它们很可能被注释掉：

```
+   * 
+   * CHOOSER BROADCAST
```

这些行告诉系统接受来自任何主机的登录，并为任何请求的客户端提供选择器（本地网络上可用 XDMCP 服务器的列表）。默认被注释掉的配置拒绝所有计算机访问，因此取消注释这些行即可启用访问。不过，代替使用星号 (*)，你可能希望按名称指定计算机。星号可以代表名称的一部分。例如，*.luna.edu 授予 luna.edu 域中任何计算机访问权限。

/etc/X11/xdm/Xservers 文件列出了 XDM 应管理的显示。典型的配置包含类似以下的行：

```
:0 local /bin/nice -n -10 /usr/X11R6/bin/X -deferglyphs 16
```

![](img/f430a19bdf014c43ad7c2d594afd5b21_129_0.png)

此行告诉 XDM 运行 /usr/X11R6/bin/X，并在此服务器上每当 XDMCP 服务器本身运行时显示 XDMCP 登录提示。如果你不想在本地启动 X 但希望接受远程 XDMCP 登录，请注释掉此行。当你重启运行级别 5 时，系统不应启动 X，但应接受远程 XDMCP 登录。

## 配置 KDM

KDM 的配置文件与 XDM 使用的相同，除了某些 KDM 配置将这些文件放在新位置和新名称下。具体来说，kde-config 可能替代 xdm-config，并可能位于 /opt/kde/bin/ 或 /usr/bin。Xaccess 和 Xservers 可能位于 /opt/kde/share/config/kdm、/etc/kde/kdm、/etc/kde3/kdm 或某些其他目录。如果你找不到这些文件，请尝试使用你的包管理器的工具定位安装 KDM 的包，然后查看包内容。例如，在 Red Hat 或 Fedora Core 系统上，你可能会输入以下命令：

```
$ whereis kdm
kdm: /usr/bin/kdm
$ rpm -qif /usr/bin/kdm | grep Xaccess
/etc/kde/kdm/Xaccess
```

除了这些你可以像调整 XDM 配置文件那样调整的配置文件，KDM 还提供 KDM 特定的配置文件。其中最重要的文件是 kdmrc，可能存储在 /etc/kde/kdm、/etc/kde3/kdm、/etc/X11/kdm 或其他位置。此文件指向其他配置文件——可能直接或间接包括 XDM 配置文件。该文件还包含一个名为 [Xdmcp] 的部分，其中设置了各种 XDMCP 选项。确保此文件中存在以下行：

```
Enable=true
Port=177
```

## 配置 GDM

GDM 使用完全独特的配置系统。GDM 配置文件通常位于 /etc/X11/gdm，因此首先检查该目录。如果你在那里找不到文件，请使用你的包管理器尝试定位它们，如前一节中为 KDM 所述。主要的 GDM 配置文件称为 `gdm.conf`，与 XDMCP 服务器操作最相关的部分称为 [xdmcp]。要启用远程登录，确保此部分包含以下行：

```
Enable=true
Port=177
```

如果你想在不启动本地 X 的情况下接受远程 XDMCP 登录，请定位 `gdm.conf` 中的 [servers] 部分。此部分通常包含如下的行：

```
0=Standard vt7
```

在行首添加井号 (#) 注释掉此行，这样 GDM 在重启时就不会在本地系统上启动 X。（你可能需要切换到运行级别 3 然后切回运行级别 5 以在不启动 X 的情况下重启 GDM。）

代替在文本编辑器中编辑配置文件，你可以使用 GUI 工具。在 xterm 窗口中输入 `gdmsetup`，或从桌面环境菜单中选择 GDM 配置工具的选项，通常称为登录屏幕、GDM 配置器或类似名称。结果是 GDM 设置窗口，如图 2.6 所示。XDMCP 标签页包含几个 XDMCP 选项，但最重要的 XDMCP 选项是安全标签页上的启用 XDMCP 复选框。也要确保程序设置为监听 UDP 端口 177（在 XDMCP 标签页上设置）。

## 使用 XDMCP 客户端

一旦你重新配置并重启了 XDMCP 服务器，是时候用 XDMCP 客户端试试了——也就是说，一个 X 服务器。许多操作系统都有 X 服务器可用，不仅仅是 Linux。例如，如果你想从 Windows 客户端访问 `gandalf`，可以使用 Windows 的 Cygwin/X（`http://x.cygwin.com`）或 XManager（`http://www.netzarang.com/products/xmg_detail.html`）。

![](img/f430a19bdf014c43ad7c2d594afd5b21_131_0.png)

不过，为了练习的目的，我将假设你可以访问能够运行 XFree86 或 X.org-X11 的计算机，例如另一台 Linux 计算机。使用这样的系统通过 XDMCP 访问另一个系统的诀窍是以正常方式不启动 X，因为那样会启动本地窗口管理器并可能显示系统自己的 XDMCP 登录提示。相反，你从文本模式登录或自定义启动脚本启动 X 并传递 −query *host.name*、−broadcast 或 −indirect *host.name* 选项，这使 X 以各种方式尝试查找并使用 XDMCP 服务器。

- **查询** −query *host.name* 选项告诉服务器直接连接到指定的 XDMCP 服务器。如果一切正常，你将看到 XDMCP 登录提示并能够访问系统。
- **广播** −broadcast 选项告诉本地 X 服务器广播查询可用的 XDMCP 服务器。X 连接到第一个可用的服务器。（不过，一些 X 服务器会显示 XDMCP 服务器列表，允许你选择想要使用哪一个。）
- **间接** −indirect *host.name* 选项要求你指定的主机在其本地网络段上显示可用 XDMCP 服务器列表。如果你试图选择位于防火墙后面的机器，该防火墙阻止广播但不阻止 XDMCP 登录或其他 X 相关活动，那么这个选项最有用。


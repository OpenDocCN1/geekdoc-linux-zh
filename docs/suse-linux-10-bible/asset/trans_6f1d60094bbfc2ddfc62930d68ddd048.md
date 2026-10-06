

# 第 8 章 ✦ X Window 系统 201

## 远程图形化登录

你也可以从 bible 远程以图形化方式登录到 wiley，看到与你坐在 wiley 显示器前时完全一模的的内容。

要实现这一点，你需要在 wiley 上进行一些配置；其 kdm（或者如果你没有使用 KDE，则是 gdm 或 xdm）配置文件需要进行修改，以允许远程登录。

- 1. 对于 wiley 上的 kdm，编辑文件 `/etc/opt/kde3/share/config/kdm/kdmrc`，并在 `[Xdmcp]` 节头部下修改以下几行：

```
Enable=false
Enter=true
```

- 2. 现在，假设 bible 上没有运行图形界面（你已经执行了 `start 3` 命令并登录在文本控制台上），执行以下操作：

```
userbible:-> X -query wiley
```

你应该能看到 wiley 的图形化登录界面；你可以作为 wiley 上的任何用户登录，并在你的桌面环境中工作。

如果 bible 上正在运行图形界面，但你希望能够以图形化方式登录 wiley（并在两个会话之间切换），这也是可能的。只需指定 bible 上一个未被使用的显示器即可：

```
userbible:-> X -query wiley :1
```

这会在 bible 的第二个显示器上启动一个全新的 X 会话，并显示 wiley 的登录界面（第一个显示器编号为 0，第二个为 1）。你甚至可以从现有的图形会话运行上述命令。bible 上现有的显示器仍然存在，你可以通过 `Ctrl+Alt+F7` 切换回去。你可以通过 `Ctrl+Alt+F8` 切换到新显示器。

> 要自动执行类似的操作，可以使用 XConfig 环境变量设置，或使用 yast2 远程管理面板。通过更改 `/etc/sysconfig/displaymanager` 文件中 `DISPLAYMANAGER_REMOTE ACCESS` 的值改为 "yes"，或者使用 yast2 网络服务*远程管理面板，来设置合适的 `UseConfig` 变量。

## 来自 Windows 的图形连接

Windows 有许多 ssh 客户端，最著名的是 PuTTY。如果你想从远程 Windows 机器查看 Linux 桌面，一种简单的方法是使用 PuTTY 配合虚拟网络计算 (VNC)。你需要在 Linux 上安装 `tightvnc` 软件包，并在 Windows 上安装 PuTTY 和 VNC 查看器。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_245_0.png)

# 202 第二部分 ♦ SUSE 系统

这些应用程序位于你的 SUSE 发行版介质的 `dosutils` 目录中，但你始终可以直接从它们的官网获取最新、最好的版本。PuTTY 可以在 www.chiark.greenend.org.uk/~sgatham/putty/ 获取。Windows 版 VNC 查看器可以在 www.realvnc.com 获取。看起来 3.3.5 版本的 VNC 查看器与当前 SUSE 版本包含的 `tightvnc` 软件包配合得最好。

使用 PuTTY 从 Windows 登录你的 Linux 机器。登录后，执行以下操作：

```
user@bible:->vncserver
访问你的桌面需要密码。
Password:
```

当你输入密码后，你将看到类似下面的的内容：

```
New 'X desktop is bible:1
Creating default startup script /home/user/.vnc/xstartup
Starting applications specified in /home/user/.vnc/xstartup
Log file is /home/user/.vnc/bible:1.Log
```

你可以在 Windows 上启动 VNC 查看器并连接到 `bible:1`（或相应的 IP 地址后加上 `:1`）。数字是显示器编号；VNC 服务器连接到下一个可用的显示器编号，你必须提供相同的编号才能连接。你将看到一个 Linux 桌面（实际上运行的是 `twm` 作为窗口管理器）。如果你通常使用 KDE 并且想看到熟悉的 KDE 桌面，你需要编辑 `~/.vnc/xstartup` 文件，将 `twm &` 替换为 `startde &`。

注意，你也可以通过（支持 Java 的）浏览器使用地址 `http://bible:5801` 连接到 VNC 服务器——端口号是 5800 加上显示器编号。

你可以通过在 YaST 中激活远程管理功能来实现同样的操作。

## 桌面共享

krfb 桌面共享程序也包含在 SUSE 的 KDE 部分；它允许你使用 VNC 协议与其他用户共享当前的会话。krfb 程序会创建一个会话密码并提供限时邀请。其他人可以通过网络上的任何其他 VNC 客户端连接到该会话，在这种情况下，他们字面上是在共享同一个桌面会话——两个用户都可以使用键盘和鼠标，效果会出现在两个显示器上。

# 第 8 章 ♦ X Windows 系统 203

当然，你也可以在 Windows 上运行 VNC 服务器，并使用 Linux 的 `vncviewer` 或 `krdc` 程序访问 Windows 桌面，或者你可以使用这些程序从另一台 Linux 机器访问你的 Linux 桌面。

或者，你可以在 Windows 中运行一个完整的 X 服务器。替代方案包括基于 Java 的 `weirdx`（包含在 SUSE 发行版的 `docile` 目录中）以及 `cygwin/X`（它是 Cygwin 的一部分，在 Windows 上提供了完整的 Unix 环境）。

## Cygwin/X

Cygwin/X 可从 http://x.cygwin.com/ 获取，在 Windows 上易于安装和运行。当你运行安装程序时，你会发现由于依赖关系，你必须安装 Cygwin 环境大部分才能运行 X。然后你可以点击 Cygwin 图标获取 shell，输入（例如）`X-query`，即可以图形化方式登录远程 Linux 机器。

Windows 上也有许多实惠的 X 服务器实现。其中最好且最实惠的是 Labtam 的 XConnect 软件，可以在 www.labtam-inc.com 获取。其他公司，例如 Hummingbird (www.hummingbird.com/products/nc/exceed/)，为需要互操作的 Windows 用户提供了类似的功能。

## 无盘 X 终端

作为其他地方运行程序的显示器并不需要大量的物理资源；利用旧硬件来完成此点的想法非常有趣。我们不会详细讨论这一点，但人们对使用 Linux 的瘦客户端（client-thin）桌面计算方法兴趣日益增加。

在真正的客户端情况下，客户端机器使用网络启动从 NFS（网络文件系统）获取其内核和目录树，并在服务器上运行程序，只有显示在本地。在某些变体中，部分应用程序在本地执行。

这种方法最著名的方法是 Linux Server Project (LTSP)，网址 www.ltsp.org。目前 LTSP 未包含在 SUSE 发行版中。然而，传闻（已证实）Novell 的 Linux 团队对改进 LTSP 并将其作为解决方案的一部分非常感兴趣。

LTSP 由一个通过 NFS 导出的客户端目录结构和一个适配内核组成。客户端通过 PXE 启动（Intel 的预执行环境）或 etherboot（允许网卡通过软盘或添加到网卡的启动 ROM 从网络启动）启动。LTSP 的安装和设置相对简单，具有巨大的优势。客户端不需要配置——如果硬件故障，你只需替换客户端即可一切正常。你的用户文件位于服务器上。

KDE 一直是 SUSE 的默认图形环境。目前的 3.2 版本提供了一个非常完整且功能丰富的桌面环境。它提供的包括：

- 应用程序之间一致的视觉效果
- 一个带有级联图形窗口的开始按钮
- 图标
- 面板栏
- 多虚拟桌面
- 主题
- 剪贴板
- 拖放支持
- 应用程序之间的复制粘贴支持

此外，SUSE 将 YaST 集成到 KDE 菜单中，并对 OpenOffice 的部分集成做出了贡献。图 8-3 显示了默认的 KDE 桌面。

集成桌面环境的功能是以资源为代价的；在实际运行 KDE之前需要启动大量的基础设施。对于内存有限的机器，更简洁的 X 窗口系统环境（如本章讨论的窗口管理器）可能是是更好的选择。

我们的目的并不是记录 KDE 的所有功能。这样做是多此一举（因为 KDE 的功能确实如设计初衷那样直观），而且会占用过多空间。然而，我们讨论了一些初看并不易发现的特别实用的功能。


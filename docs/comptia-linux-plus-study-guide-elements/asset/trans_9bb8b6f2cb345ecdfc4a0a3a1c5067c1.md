
虽然大多数人认为客户端运行在用户所坐的计算机上，而服务器运行在远程系统上，但在 X 系统中情况并非如此。在 X 中，服务器运行在用户本地的系统上。**要理解这一点，请从程序的角度来思考。** 对于文字处理器而言，显示器和键盘是需要使用的服务，就像可通过网络访问的打印机一样。

假设你的本地网络包含两台机器。名为 zeus 的计算机是一台强大的机器，托管着重要的程序，如文字处理器和数据分析工具。名为 apollo 的计算机则是一台功能弱得多的系统，但它配备了足够的显示器和键盘。因此，你希望在 apollo 前操作并运行位于 zeus 上的程序。这两个系统都运行 Linux。要完成此任务，请按照以下步骤操作：

-   1. 登录 apollo，如果 X 尚未运行，请启动它。
-   2. 在 apollo 上打开一个终端（例如 xterm）。
-   3. 在 apollo 的终端中输入 `xhost +zeus`。此命令指示 apollo 接受源自 zeus 的数据以显示在其 X 服务器中。
-   4. 从 apollo 登录到 zeus。例如，你可以使用 Telnet 或 Secure Shell (SSH)。结果应该是你能够在 zeus 上的 shell 中键入命令。
-   5. 在 zeus 上，输入 `export DISPLAY=apollo:0.0`。（这假设你正在使用 Bash；如果你使用的是 tcsh，命令将是 `setenv DISPLAY apollo:0.0`。）此命令告知 zeus 使用 apollo 来显示 X 程序。
-   6. 在 zeus 命令提示符下，输入运行程序所需的内容。例如，你可以输入 **office** 来启动 OpenOffice.org。你应该会在 apollo 的显示器上看到程序打开，但它们是在 zeus 上运行的——它们的计算使用 zeus 的 CPU；它们可以读取在 zeus 上可访问的文件，等等。
-   7. 完成后，关闭你启动的程序，注销 zeus，并在 apollo 上输入 `xhost -zeus`。这将增强安全性，使得 zeus 上的不法者无法修改你在 apollo 上的显示。

有时，你可以跳过其中一些步骤。例如，根据其配置方式，SSH 可以转发 X 连接，这意味着 SSH 会拦截显示 X 信息的尝试，并将这些请求传递给发起连接的系统。当这种情况发生时，你可以跳过第 3 步和第 5 步，以及第 7 步中的 xhost 命令。使用 SSH 转发 X 需要服务器端的支持，如前文“设置远程访问服务器”中所述。在客户端也需要类似的配置（使用 /etc/ssh/ssh_config 中的 ForwardX11 选项），或者你在建立初始连接时将 -X 选项传递给 ssh。（请注意，这是大写的 -X；小写的 -x 会禁用客户端的 X 转发！）

作为一种额外的安全措施，如今的许多 Linux 发行版都配置 X 以忽略真正的网络连接。如果你的发行版是这样配置的，前面的步骤将不起作用；当你尝试从远程系统启动 X 程序时，你会收到错误消息。要解决此问题，根据 X 的启动方式，你必须进行额外的更改：

**GDM**
在旧版本的 GDM 中，检查 GDM 配置文件（通常是 `/etc/X11/gdm/gdm.conf`）；查找 `DisallowTCP=true` 这一行，并将其更改为 `DisallowTCP=false`。在新版本的 GDM 中，编辑 `/etc/gdm/gdm.schemas`，查找读作 `<key>security/DisallowTCP</key>` 的行。在此行下方几行处，将键的值从 `true` 更改为 `false`。

**KDM 或 XDM**
这两个 XDMCP 服务器都依赖于 Xservers 文件中的设置（对于 XDM 在 `/etc/X11/xdm` 中，对于 KDM 在此位置或其他变化极大的位置中）。查找以 `:0` 开头的行。该行包含 KDM 或 XDM 用于启动 X 服务器的命令。如果该行包含字符串 `-nolisten tcp`，请从该行中移除该字符串。这样做会消除导致 X 忽略常规网络连接选项。

**特殊的 OpenSUSE 配置**
在 OpenSUSE 中，你必须编辑 `/etc/sysconfig/displaymanager` 并将 `DISPLAYMANAGER_XSERVER_TCP_PORT_6000_OPEN` 选项设置为 `yes`。

**从文本模式登录启动 X**
如果你使用文本模式登录并输入 `startx` 来启动 X，你可能需要修改 `startx` 脚本本身，该脚本通常存储在 `/usr/bin` 中。在此脚本中搜索字符串 `-nolisten tcp`。 chances are 此字符串将出现在变量赋值（如赋给 `defaultserverargs`）中，或者可能出现在对 X 服务器程序的直接调用中。从此变量赋值或程序调用中移除 `-nolisten tcp` 选项。

完成这些更改后，你需要重启 X。此后，X 应能响应远程访问请求。

![](img/a78bc63f22351f522ba5ec1fa0c060d2_450_0.png)

> 发行版维护者禁用 X 响应远程请求的能力是有原因的。如果 X 响应远程网络请求，入侵者利用 bug 或错误配置通过屏幕上显示虚假消息来欺骗用户的风险会大大增加。因此，只有在你确定这样做是必要时，才应禁用此保护。你可能能够使用 SSH 链接而无需禁用此保护。

远程运行 X 程序的另一个选项是使用虚拟网络计算 (VNC) 系统（http://www.realvnc.com/）。VNC 在远程计算机上运行一个特殊的 X 服务器，而在你所在的计算机上运行一个特殊的 VNC 客户端。你使用客户端直接联系服务器。这种在常规 X 远程访问正常状态下的客户端和服务器角色的反转在某些情况下是有益的，例如当你试图通过某些类型的防火墙访问远程系统时。VNC 也是一个跨平台协议；使用 VNC 可以从 Linux 控制 Windows 或 Mac OS 系统，但在 X 中这是不可能的。（Windows 和 Mac OS 的 X 服务器是可用的，允许你从这些非 Linux 操作系统控制 Linux 系统。）第 11 章更详细地描述了 VNC。

## 远程 GUI 登录

第 1 章“Linux 入门”描述了 X Display Manager Control Protocol (XDMCP) 服务器（如 XDM、KDM 或 GDM）的基本配置，以管理本地 GUI 登录。这些协议也支持远程 GUI 登录——你可以使用一个极其精简的本地系统来访问更强大的远程计算机。一些办公室使用这种类型的配置，将计算能力集中在少数几台计算机上，并允许用户从可能无法处理现代软件需求的旧硬件或专用硬件上登录。基于 XDMCP 的登录与通过 Telnet 或 SSH 会话发起的登录不同，因为你不需要先发起该文本模式登录。在极端情况下，你可以坐在客户端前，像该 XDMCP 客户端系统就是那台强大的远程计算机一样，只需登录一次。

### 配置 XDMCP 服务器

要启用远程 GUI 访问，你必须对第 1 章中描述的标准 XDMCP 配置进行一些更改。你在 XDMCP 服务器计算机上进行第一次更改——即托管用户帐户、应用程序和数据文件的系统，而不是用户的桌面终端。

最简单的情况是 XDM。对于此服务器，你必须首先修改 */etc/X11/xdm/xdm-config*。查找类似于以下内容的行：

```
DisplayManager.requestPort: 0
```

这一行告诉 XDM 不要访问常规服务器端口。为了使用 XDM 进行远程登录，你必须将 0 更改为 177，即传统的 XDMCP 端口。

必须对 */etc/X11/xdm/Xaccess* 进行第二次更改。此文件控制哪些计算机可以访问 XDM 服务器，以及以何种方式访问。一个完全开放的系统包含使用星号 (*) 表示任何人均可访问系统的行：

```
*
* CHOOSER BROADCAST
```

第一行告诉 XDM 任何人均可连接，第二行告诉 XDM 任何人可以请求一个 *chooser*——即显示接受 XDMCP 连接的本地系统的界面。要限制选择，你应该列出单独的计算机或计算机组，而不是使用星号通配符：

```
*.pangeeaa.edu
tux.example.com
*.pangeeaa.edu CHOOSER BROADCAST
```

此示例允许 pangeeaa.edu 域中的任何计算机连接或接收 chooser，并允许 tux.example.com 连接但不接收 chooser。

KDM 服务器配置与 XDM 非常相似，但可能会使用不同的配置文件，如第 1 章中所述。检查 */etc/X11/kdm/*、*/etc/kde/kdm/* 或浏览 KDM 软件包内容所建议的其他位置。你可能还需要查找


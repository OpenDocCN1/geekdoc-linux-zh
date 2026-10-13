
你需要密码来访问桌面。

密码：

输入密码以允许远程访问并按回车。脚本随后将加载并启动 `xvnc` X11 服务器（基于 XFree86 3.3.2 的自定义 X11R6.3 服务器）。如果你想在联网的 Win32 计算机的远程桌面工作，必须下载 Win32 vnc 软件并将其复制到远程计算机上。Win32 软件必须使用 `WinZip` 等存档工具进行提取。

解压 Win32 vnc 软件并使用 `vnc` Setup 安装软件。要启动服务器，从开始菜单中的 `vnc` 文件夹点击“Install Default Registry Settings”菜单项。点击图 D.10 显示的 WinVNC 3.3.2 菜单项。

### 图 D.10 Win32 vnc

Win32 软件为 Windows 桌面上的开始菜单提供了易用的菜单项。

就是这些！如果你需要自定义设置或更改访问 Win32 桌面的密码，请点击 WinVNC 设置菜单项。你将看到一个如图 D.11 所示的对话框，可以使用它来更改网络或密码设置。

### 图 D.11

使用 WinVNC 设置对话框为你的 Win32 桌面配置 WinVNC。

![](img/fbfff30e42d507bc7531108a281d6cf4_1222_0.png)

要从 Linux 远程访问 Win32 桌面，请使用 `vncviewer` 命令，后跟 Win32 计算机的主机或 IP 地址以及桌面编号（根据 `vnc` readme，该编号始终为 0）。在 X11 终端中输入命令：

```
# vncviewer ascentia.home.org:0
```

### 附录
第五部分

系统提示输入远程 `vnc` 服务器的密码：
`vncviewer`: VNC server supports protocol version 3.3 (viewer 3.3)
Password:

输入密码并按回车后，会出现一个带有远程桌面的 X11 窗口（如图 D.12 所示）。你可以启动远程应用程序并像操作自己的计算机一样进行工作！

#### 注意
`vncviewer` 客户端和 `vncserver` 脚本还识别几个 X11 选项，例如 `geometry` 设置。例如，如果你在远程 Linux 计算机（通过 Telnet 会话）启动 `vncserver`，可以使用 `-geometry` 指定远程查看桌面的尺寸。要启动 800×600 像素的服务器，使用如下命令：

```
# vncserver -geometry 800x600 hostname:display
```

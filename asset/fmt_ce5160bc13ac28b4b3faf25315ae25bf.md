
你还将对 Mac-on-Linux 模拟器进行基本介绍，它允许你在 X 桌面上的窗口中运行 Mac OS。最后，你将快速了解你的 Power Mac 上的其他操作系统，例如 BSD（*Berkeley Software Distribution*）UNIX。

### 使用 Xvnc

位于英国剑桥的 AT&T 实验室分发一个名为 `xvnc` 的免费软件包。这种虚拟网络软件使您能够运行使用与桌面不同的操作系统的远程计算机。这意味着，如果你的局域网中有使用 Windows 或 Mac OS 的计算机，你可以将每台计算机显示在 Linux 桌面的窗口中。这也意味着，你可以坐在运行 Windows 或 Mac OS 的计算机前，从远程桌面在窗口中运行你的 Linux 计算机。

`xvnc` 是安装在系统上的 X 服务器的一种特殊变体。`xvnc` 的版本适用于许多计算机，例如：

- DEC Alpha OSF1 3.2
- Java
- Macintosh OS（68K 和 PPC）
- Palm OS
- PocketPC
- Solaris 2.5 (SPARC)
- Win32（如 Windows 9x/2000/NT）

`xvnc` 软件包提供了一个名为 `vncserver` 的 shell 脚本、`xvnc` 修改后的 X 服务器，以及一个名为 `vncviewer` 的远程桌面查看客户端。所有 Linux PPC 发行版都有 `xvnc` 的版本。

安装软件后（很可能使用 `rpm` 命令或 `yast`），你可以使用 `vncserver` 脚本在你的系统上启动 `xvnc`。此脚本允许你使用其 `-geometry` 和 `-depth` 设置来设置默认屏幕大小和颜色深度。例如，要启动提供 800x600 桌面和数千种颜色的会话，请使用 `vncserver` 脚本，如下所示：

```
$ vncserver -geometry 800x600 -depth 16
```

你会被提示输入密码：

```
Password:
Enter a password used to allow remote access and press Enter. You will again be
asked to verify the password, like this:

Verify:
New 'X' desktop is cube:1

Creating default startup script /home/bball/.vnc/xstartup
Starting applications specified in /home/bball/.vnc/xstartup
Log file is /home/bball/.vnc/cubie:1.log
```

注意，服务器返回一个 DISPLAY 编号（在此示例中为 1）。希望远程连接的用户需要知道此显示编号以及你的密码，才能连接到你的虚拟会话。

你的会话设置位于主目录中名为 `.vnc` 的目录中。名为 `xstartup` 的文件提供了有关会话使用的 X 窗口管理器的说明。你可以编辑此文件以启动你选择的任何窗口管理器，如下所示：

```
#!/bin/sh

xrdb $HOME/.Xresources
/opt/kde2/bin/startkde
```

在此示例中，指定了 K 桌面环境。当你或远程用户连接时，这是该会话使用的窗口管理器。注意，使用 vnc 可能是资源的消耗；这就好比你在内存中运行了另一个 X 会话！

图 17.1 显示了一个远程 PPC Linux 会话（运行 twm 窗口管理器），从另一个（基于 Intel 的）Linux X 会话的桌面查看。

Mac OS `xvnc` 软件包也支持远程查看。从 `xvnc` 首页下载 Mac OS 版本。你需要解压软件。接下来，双击 VNC PPC 文件夹中的 VNC 服务器安装程序脚本。软件将安装在你的系统文件夹中，并附带一个 VNC 控制项控制板。

为了启用远程查看会话，首先使用“监视器”控制板为桌面选择分辨率。你的远程会话将自动使用当前监视器的设置大小和颜色深度。接下来，双击 `VNCServer PPC` 应用程序，并从“文件”菜单中选择“选项”菜单项。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_451_0.png)

单击密码字段（如图 17.2 所示），并输入密码以保护您的系统免受远程访问。

输入完密码后，单击“确定”按钮。您的 Mac OS 桌面现在已准备好查看。在远程计算机上（例如另一台运行 Linux 的 Power Mac），使用 `vncviewer` 命令以及默认显示器编号（Windows 或 Mac OS 始终为 0）连接至桌面，操作如下：

```bash
$ vncviewer titanium:0

VNC server supports protocol version 3.3 (viewer 3.3)
Password:
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_451_1.png)

VNC 身份验证成功

桌面名称 *titanium*

已连接至 VNC 服务器，使用协议版本 3.3

VNC 服务器默认格式：

每像素 16 位。

每个像素最高有效字节优先。

真彩色：最大红 31 绿 31 蓝 31，红移位 10 绿移位 5 蓝移位 0

使用默认色谱，即为 TrueColor。像素格式：

每像素 16 位。

每个像素最高有效字节优先。

真彩色：最大红 31 绿 31 蓝 31，红移位 10 绿移位 5 蓝移位 0

按回车键后，您将看到一个桌面，如图 17.3 所示。

#### 停止 Linux VNC 会话

在 Windows 或 Mac OS 等系统上停止 VNC 软件的操作非常简单，只需使用服务器菜单即可。然而，在 Linux 下，您必须终止 VNC 服务器进程。一种快速的方法是使用权重 `killall` 命令，该命令通过名称来“杀死”进程。例如，要停止正在运行的 `Xvnc` 服务器，您可以使用 `killall` 命令，操作如下：

```bash
$ killall Xvnc
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_452_0.png)

您可能还会在主目录下的 `~/.vnc` 目录中找到该会话的进程 ID 和日志文件。VNC 软件还会在 `/tmp` 目录下创建临时文件。另一种，或许更优雅的方式是终止正在运行的会话，方法是使用 `vncserver` 命令的 `-kill` 选项，后跟当前的显示器编号。

#### 使用 MOL

Mac-on-Linux 仿真器是一个 X11 客户端，它使用您系统的 Mac OS ROM（*只读存储器*）文件在桌面上的窗口中运行 Mac OS。这个软件包是由 Samuel Rydh 领导的一个项目以及众多 PPC Linux 黑客的成果，它本地运行，速度快得惊人！

下载后，以 root 身份使用 `rpm` 命令安装 `mol` 的二进制版本，操作如下：

```bash
# rpm -ivh mol*rpm
mol
########################################
```

如果您使用 Mac OS 8.6 或更高版本，请使用 `strip_nwrom` 命令在 `/usr/lib/mol/rom` 目录下创建一个名为 `rom.nw` 的文件。您可以从现有的 System Folder 或 Mac OS 系统恢复 CD-ROM 获取此文件。使用该命令如下：

```bash
# mount -t hsfs /dev/cdrom /mnt
# /usr/bin/strip_nwrom "/mnt/System Folder/Mac OS ROM" /usr/lib/mol/rom/rom.nw
```

在此示例中，恢复 CD-ROM 已挂载在 `/mnt` 目录下。您的下一个任务是编辑文件 `/etc/molrc`。特别是，您需要编辑列出您可用 Mac OS 分区的部分。您可以（以 root 身份）使用 `pdisk` 命令找到此信息，操作如下：

```bash
# pdisk -l
```

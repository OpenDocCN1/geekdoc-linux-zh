
```
service iptables save
```

规则将被放置在`/etc/sysconfig/iptables`文件中。请记住，如果你再次运行`lockit`，它将覆盖此文件。此外，检查 IP 转发是否开启。你可以在网关主机上通过`netcfg`执行此操作。检查路由面板并点击顶部的“网络转发”（Network Forwarding）框。这将`/proc/sys/ipv4/ipforward`的值设置为`1`。如果你想手动执行，可以使用命令：

```
echo 1 > /proc/sys/ipv4/ipforward
```

如果你使用的是 IPTables，遵循相同的步骤，只需不使用`lockit`而使用`iptables`命令来实现防火墙规则。为第一个以太网设备（`eth0`）添加伪装的规则如下：

```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

### 使用远程打印机

一旦设置好网络，你就可以使用任何 Linux 主机访问连接到网络上主机的打印机，无论是 Linux、Windows 还是 Novell 系统。连接打印机的 Linux 主机首先需要按照第 4 章所述使用`printerconf`安装打印机。另一台 Linux 主机可以通过安装远程打印机来访问该打印机。例如，如果一台 Epson 打印机连接并安装在`turtle.mytrek.com`主上，那么`rabbit.mytrek.com`主机就可以直接打印到`turtle`主机上的 Epson 打印机。事实上，你可以将所有打印机连接到一台主机，并让所有其他主机通过它打印。

你使用`printerconf`安装远程打印机。从 Gnome 菜单选择“打印机配置”（Printer Configuration）并点击按钮。将显示一系列对话框，用于输入打印机名称、远程打印机类型、打印机的远程队列名称以及连接打印机的远程主机。对于其他 Linux 系统，会显示远程主机的主机名和 IP 地址（见图 7-9）。确保也按照第 4 章所述输入设备驱动程序和名称信息。

### 配置 Unix 打印队列

配置您的远程 tcp 服务器和队列。如果未指定队列，您将使用远程服务器上的默认队列。如果您在连接旧版 tcp 服务器时遇到问题，请选择`RFC1179 兼容性`。

服务器：`rabbit.myext.com`

队列：`LPT1`

[x] `RFC1179 兼容性`

![](img/6cd7e3ee37600d2fcd508ba45f870a38_131_0.png)

该方法在 Windows 和 Netware 系统上的工作原理类似。然而，要访问 Windows 系统，您必须设置并运行 Samba。Samba 将作为 Linux 网络与 Windows 窗口之间的接口，允许访问 Windows 宿主机上的设备，如打印机、CD-ROM 和文件系统。Samba 在第 37 章中有详细描述。

要从 Linux 宿主机访问连接到 Windows 系统的打印机，您可以使用 Linux 宿主机上的`printconf`工具将打印机配置为远程 Windows 打印机。在`printconf`工具中，选择 Queue（队列），然后从弹出菜单中选择 Windows Printer（Windows 打印机）。将显示五个项目。在 Share（共享）框中，您输入 Windows 宿主机的名称，前面加上`//`，然后用单个斜杠分隔。例如，主机`lizard`上名为`myepson`的打印机的共享名称为：

```
//lizard/myepson
```

然后输入 Windows 宿主机的 IP 地址。工作组（workgroup）是 Windows 宿主机所属组。尽管您可以为每个用户创建密码，但简单的方法是指定一个没有密码的来客用户。请确保在 Windows 宿主机上设置适当的共享和密码权限。图 10 显示了远程 Windows 打印机项目。

![](img/6cd7e3ee37600d2fcd508ba45f870a38_131_1.png)

如果您允许 Windows 宿主机访问连接到 Linux 系统的打印机，必须在 Samba 中配置打印机。您需要首先通过以下命令启用`swat`的使用：

```
chkconfig swat on
```

然后在 Gnome 系统菜单上选择 Samba Configuration（Samba 配置）。这会在您的浏览器中打开一个网页，顶部有一排 Samba 按钮。点击 Printers（打印机）按钮显示一个带有选择打印机按钮的页面，然后点击 Choose Printer（选择打印机）按钮。尽管您可以设置所有用户，但一种简单的方法是选择您的打印机，然后允许来客用户以`nobody`用户身份登录。对于来客用户，将“guest ok”（允许来客）选择 Yes（是）。一旦完成更改，点击 Commit Changes（提交更改）。图 7-11 显示了一个 Samba 打印机页面，其中已选择打印机`mepson`并允许了来客访问。

![](img/6cd7e3ee37600d2fcd508ba45f870a38_132_0.png)

图 7-11：Samba 打印机

一旦执行了更改，可以通过以下命令重启 Samba 使其生效：

```
service smb restart
```

注意：Macintosh 系统上的打印机使用名为 NetTalk 的不同网络协议连接（参见第 32 章）。

### 设置 Web 服务器

对于标准安装，Red Hat 会安装 Apache Web 服务器。网络上的任何用户都可以通过其运行的主机名称访问 Web 服务器。在本例中，Web 服务器运行在网关宿主机`turtle.mytrek.com`上。通常会为主主机设置别名，例如`www.mytrek.com`。在 Web 浏览器中输入此地址将显示 Apache Web 服务器的主文档页。您的网站页面保存在在`/var/www/html`中。您可以在这里添加自己的页面，构建您的网站。Apache 手册也会位于那里。

## 第三部分：Red Hat 桌面工作站

### 章节列表

- 第 8 章：Gnome
- 第 9 章：K 桌面环境：KDE
- 第 10 章：窗口管理器
- 第 11 章：窗口
- 第 12 章：Samba 配置
- 第 13 章：应用程序
- 第 14 章：办公软件
- 第 15 章：数据库
- 第 16 章：编辑器

## 第 8 章：Gnome

### 概述

Gnome 是一个功能强大的桌面环境，旨在让 Linux 变得易于使用。Gnome 提供了丰富的用户界面，允许用户轻松地操作操作系统。Gnome 包含许多应用程序，如文本编辑器、文件管理器、网络浏览器等。Gnome 的界面是可定制的，用户可以根据自己的喜好调整外观。Gnome 是一个开源项目，由社区共同开发和维护。Gnome 已在许多 Linux 发行版中使用，如 Fedora、Ubuntu、Debian 等。通过 Gnome，用户可以享受到现代、直观的桌面体验。Gnome 的核心设计理念是简洁和高效，让用户能够专注于任务本身，而不是复杂的配置。

### Gnome 界面

Gnome 界面由面板（panel）和桌面组成，如图 8-1 所示。面板显示为屏幕底部的一条长条，它包含菜单、程序和应用程序（applets）。应用程序是设计在面板内运行的小型程序。面板上有一个带有大脚印的按钮，这是 Gnome 应用程序菜单，即主菜单。它的功能类似于 Windows 中的“开始”菜单，列出了你可以在桌面上运行的应用程序项。你可以水平或垂直方向显示面板，并且它们具有自动隐藏功能以实现全屏显示。

![](img/6cd7e3ee37600d2fcd508ba45f870a38_135_0.png)

图 8-1: Gnome

屏幕其余部分是桌面。在这里，你可以放置目录、文件或程序。你可以直接在桌面上创建它们，也可以从文件管理器窗口将其拖入。使用鼠标中键点击并拖拽操作可以在桌面上创建指向已安装程序的链接。初始状态下桌面只包含一个主目录的图标。点击它可以打开一个该目录的文件管理器窗口。在桌面任何地方点击右键会显示桌面菜单（见表 8-1），你可以打开新窗口、创建新文件夹并管理软磁盘和 CD-ROM。

表 8-1: Gnome 1.4 桌面菜单 (Nautilus)

| 菜单项 | 说明 |
|---|---|
| 新窗口 (New Window) | 在桌面上启动一个新的 Nautilus 文件管理器窗口，显示你的主目录。 |
| 新终端 (New Terminal) | 启动一个新的 Gnome 窗口并导航到桌面目录。 |
| 新文件夹 (New Folder) | 在桌面上创建一个新目录。 |
| 按名称清理 (Clean Up by Name) | 整理你的桌面图标。 |
| 磁盘 (Disks) | 显示子菜单，列出你可以选择挂载的软磁盘和 CD-ROM 设备。挂载的磁盘将以 CD-ROM 或软磁盘图标显示在桌面上，你可以使用它们进行访问或稍后卸载。 |

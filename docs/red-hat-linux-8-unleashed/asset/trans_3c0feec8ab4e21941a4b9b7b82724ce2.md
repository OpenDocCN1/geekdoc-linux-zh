

## 第 12 章打印服务

ASCII 测试页是一个文本页面；PostScript 测试页是一个带有轮廓边框、Red Hat 标志和彩色方框（如果你使用彩色打印机）的文本页面。

> 注意
> 通过编辑 `/etc/lpd.perms` 文件可以启用广泛的本地和网络打印机安全功能。此文件用于为系统上的打印服务设置详细的权限信息。更多信息请参阅 `lpd.perms` 手页。

## 会话消息块打印

打印到 SMB 打印机需要 Samba 以及其相关的实用程序，如 `smclient` 和相关的 `smbprint` 实用。你可以使用 Red Hat 自带的软件打印到 Windows 网络上的共享打印机，或者将连接到 Red Hat 系统的打印机设置成 SMB 打印机。有关 Samba 的详细信息，请参阅第 13 章“网络连接”。本节描述了如何创建一个本地打印机，以便使用 SMB 打印到远程打印机。

设置 SMB 或共享打印机通常在 Windows 操作系统下通过控制面板中的“网络设备”配置设置来完成。启用打印机共享后，重启计算机。在“我的电脑”的“打印机”文件夹中，右键点击你想共享的打印机名称/图标，并在弹出菜单中选择“共享”。设置“共享为”项；然后输入一个描述性名称（例如 HP400）和密码。

在运行 Linux 时，你必须输入名称和密码来配置打印机。你还需要知道打印机的组名、IP 地址、打印机名称，以及手头的用户名和密码。要找到这些信息，选择“开始”、“设置”、“打印机”，在窗口中右键点击共享打印机的列表，并从弹出窗口中选择“属性”。与之前一样，创建一个本地打印机队列并为其分配一个名称，然后在“设置打印机队列名称和类型”对话框中选择“打印机”。点击“下一步”按钮，然后如图 12-11 所示输入所需信息。

创建一个与远程打印机特征匹配的打印机队列。例如，如果远程打印机是 HP 400 Deskjet，请选择配置列表中列出的该设备驱动程序。）创建或编辑本地或远程打印机队列后，不要忘记保存并重启`/etc/printcap` 中的新条目可能如下：

```
hp400deskjet:
:mx#0:\n:sd=/var/spool/hp400deskjet:\n:af=/var/spool/lpd/hp400deskjet/hp400deskjet.acct:\n:sh:
:lp|/usr/share/printconf/util/smbprint:
:lpd-bounce=true:
:if=/usr/share/printconf/util/mf_wrapper:
```

（此处为图片占符）

图 12.11 使用所需信息为 Windows 创建共享远程打印机。

在此示例中，你可以看到 `lp:` 字段中使用了 SMB 打印过滤器 (`smbprint`)。

## 网络连接打印机的配置与打印

Red Hat Linux 支持其他远程打印方法，例如使用基于 Novell 的打印队列或使用带有 HP JetDirect 适配器直接连接到网络的打印机。某些制造商还提供针对 Linux 的特定驱动程序和帮助。例如，HP/Compa 在 http://h20000.www2.hp.com/bizsupport/index.jsp 为早期版本的 Red Hat Linux 提供了图形化打印机配置工具和软件驱动程序。

你可以使用 Red Hat Linux 快速方便地设置网络连接打印。例如，GEARNET 的 PS101 打印服务器适配器与 Linux 配合良好。这个微型设备（自托管打印服务器）是一个直接连接到 Centronics 接口的适配器，消除了并行端口电线的使用。PS101 提供单一连接，使用 Red Hat Linux 可以快速设置网络连接打印。你可以使用 Red Hat Linux 快速方便地设置网络连接打印。要查看此信息，使用 `nmap` 命令如下：

```
$ nmap -s 192.168.2.52
扫描结果 如下：

| 端口/状态 | 服务 |
|---|---|
| 21/tcp | open ftp |
| 23/tcp | open telnet |
| 80/tcp | open http |
| 139/tcp | open netbios |
| 515/tcp | open printer |
| 9100/tcp | open jetdirect |

```
配置打印机，编辑 `/etc/lpd.conf` 文件；默认情况下，未启用任何选项。

```
# checkpc -V
LPRng-3.8.9, Kerber5, Copyright 1998–2002 Patrick Powell, <papowell@lpr.com>
Checking for configuration files '/etc/lpd.conf'

```
找到 '/etc/lpd.conf', mod 0100644
检查打印cap 文件 '/etc/printcap'
检查 lpd 专用打印cap 文件 '/etc/lpd_printcap'
DaemonUID 4, DaemonGID 7
使用配置文件 '/etc/lpd.conf'
LPD 锁文件 '/var/run/lpd.515'
```

配置打印机，编辑 `/etc/lpd.conf` 文件；默认情况下，未启用任何选项。

## 控制台配置

`redhat-config-printer-tui` 工具允许你创建或编辑打印机。按下回车键后，将如图 12.12 所示的主界面。使用 Tab 键和空格键在控制会话中导航并选择打印机。

（此处为图片占符）

图 12.12 使用 redhat-config-tui 创建或编辑打印机。

## 使用打印命令

配置打印机后，你可以从 Red Hat 桌面使用图形客户端打印。如果你不使用桌面而喜欢使用命令行，主要命令如下：

- `lpr`: 打印调度命令；用于使用特定打印机打印文档
- `lpq`: 打印队列显示命令；用于查看等待打印的文档列表
- `lprm`: 打印队列管理命令；用于从打印机删除打印作业
- `lpc`: 打印机控制程序；用于 root 用户管理调度、lpd 守护进程和打印机活动

这些命令提供了从命令行启动和控制打印机所需的所有功能。默认情况下，Red Hat Linux 使用 Patrick Powell 的 LPRng 调度，它是 4.3BSD 打印系统的改进全面修订版本。通过编辑 `/etc/lpd.conf` 文件来配置此打印系统；默认情况下，Red Hat Linux 未启用任何选项。你可以如下使用 LPRng 的 `checkpc` 命令获取打印状态：

```
# checkpc -V
LPRng-3.8.9, Kerber5, Copyright 1998–2002 Patrick Powell, <papowell@lpr.com>
Checking for configuration files '/etc/lpd.conf'

```
找到 '/etc/lpd.conf', mod 0100644
检查打印cap 文件 '/etc/printcap'
检查 lpd 专用打印cap 文件 '/etc/lpd_printcap'
DaemonUID 4, DaemonGID 7
使用配置文件 '/etc/lpd.conf'
LPD 锁文件 '/var/run/lpd.515'
```


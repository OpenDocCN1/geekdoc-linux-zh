
## 使用 CUPS 管理打印机

通用 Unix 打印系统（CUPS）是一种替代 LPRng 的打印服务方案。它基于 GNU 通用公共许可证（GPL）免费开放。尽管 CUPS 现已包含在大多数发行版中，但你也可以从 www.cups.org 下载 CUPS 的最新源代码版本。该网站还提供了关于安装和管理打印机的详细文档。LPRng 源自旧的 Berkeley 行式打印机守护进程（LPD），而 CUPS 则基于较新的 Internet 打印协议（IPP）。Internet 打印协议旨在为 Internet 建立打印标准（更多信息请访问 www.pwg.org/ipp）。与主要关注行式打印机的旧版基于 LPD 的打印系统不同，基于 IPP 的系统提供了对网络、PostScript 和 Web 的支持。CUPS 的运行方式类似于 Internet 服务器，并采用与 Apache Web 服务器非常相似的配置设置。其网络支持允许客户端直接访问远程服务器上的打印机，而无需自行配置打印机。只需在打印服务器上维护配置即可。

在 Red Hat 使用的 RPM 版本中，`/etc/rc.d/init.d` 目录中安装了 cups 启动脚本。你可以使用 `service` 命令和 `cups` 脚本来启动、停止和重启 CUPS。当你更改配置或安装打印机时，请务必重启 CUPS 以使更改生效。在 Red Hat 中，你可以使用以下命令：

```
service cups restart
```

## 使用 CUPS 安装打印机

使用 CUPS 配置和安装打印机最简单的方法是使用 `redhat-config-printer`，如第 4 章所述。你也可以使用 CUPS 配置工具，这是一种基于 Web 浏览器的配置工具。为确保浏览器访问，请确保首先使用“打印机系统切换器”选择 CUPS；或者，如果你使用 `xinetd` 来运行 CUPS，请使用 `chkconfig` 命令启用 `cups`。

```
chkconfig cups on
```

要在 Red Hat 上启动 Web 界面，请在 Web 浏览器中输入以下 URL。

```
http://localhost:631
```

这将打开一个管理界面，你可以在此管理并添加打印机。首先，系统会要求你输入管理员的用户名（通常是 root）和密码（通常是 root 用户的密码）。

你通过一系列 Web 页面在 CUPS 上安装打印机，每个页面都请求不同的信息。要安装打印机，请单击“Add Printer”按钮以显示一个页面，在该页面中输入打印机名称和位置（参见图 25-1）。位置是指打印机所连接的主机。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_583_0.png)

图 25-1: CUPS 添加打印机页面

后续的页面将提示你输入打印机型号和驱动程序，你需要从可用列表中进行选择。添加打印机后，你可以对其进行配置。单击管理页面中的“Manage Printers”条目会列出你已安装的打印机。然后，你可以单击某个打印机，显示一个页面，让你可以控制该打印机。你可以停止打印机、配置其打印设置、修改其安装设置，甚至可以删除该打印机。单击“Configure Printer”按钮会显示一个页面，你可以指定分辨率或纸张大小来配置打印机的打印方式。

打印机的配置信息将存储在 `/etc/cups/printers.conf` 文件中。你可以直接检查此文件，甚至进行修改。以下是一个打印机配置条目的示例。请注意，它是由 `redhat-config-printer` 创建的。当前状态为 Idle（空闲），队列中没有任务：

```
<DefaultPrinter myepson>
Info Created by redhat-config-printer 0.6.x
DeviceURI parallel:/dev/lp0
Location
State Idle
Accepting Yes
JobSheets none none
QuotaLimit 0
PageLimit 0
KLimit 0
</Printer>
```

`DeviceURI` 条目指定了所使用的设备，在本例中为 `lp0` 并行设备。对于远程打印机，此条目将包含 Internet 地址及其协议。例如，CUPS 服务器（ipp）上的远程打印机会表示为如下形式（Windows 打印机会使用 `smb` 协议）：

```
DeviceURI ipp://mytstuff.com/printers/queue1
```

注意 你可以使用 `lpadmin` 命令从命令行执行管理任务。有关更多详细信息，请参阅 CUPS 文档。

## 在 CUPS 上配置远程打印机

要安装连接到 Windows 系统或另一台运行 CUPS 的 Linux 系统的远程打印机，你需要使用特殊的 URL 协议指定其位置。对于 Windows 打印机，首先你需要安装、配置并运行 Samba。CUPS 使用 Samba 来访问 Windows 打印机。在 CUPS 上安装 Windows 打印机时，使用 `smb` URL 协议指定其位置。允许登录打印机的用户输入在主机名之前，并用 @ 符号与其分隔。在大多数配置中，这是 guest 用户。这里显示了连接到名为 `lizard` 的 Windows 主机的名为 `myhp` 的 Windows 打印机的位置条目。其 Samba 共享引用将是 `//lizard/myhp`。

```
smb://guest@lizard/myhp
```

为了在 Samba 中启用 CUPS，你还必须将 `/etc/samba/smb.conf` 文件中的打印选项设置为 `cups`，如下所示：

```
printing = cups
printcap name = cups
```

为了让 CUPS 与 Samba 协同工作，你必须将 `smbspool` 链接到 CUPS 的 `smb` 后台目录：

```
ln -s /usr/bin/smbspool  /usr/cups/backend/smb
```

要访问连接到运行 LPRng 的 Linux 或 Unix 系统的打印机，请使用 `lpd` 协议指定其位置。在以下示例中，打印机 `mylaser` 连接到 Linux 主机 `rabbit.mytrek.com`：

```
lpd://rabbit.mytrek.com/mylaser
```

## CUPS 打印机类

CUPS 提供了一种功能，允许你选择一组打印机来打印作业，而不是只选择一个。这样，如果一台打印机忙碌或故障，可以自动选择另一台打印机来执行该作业。这种打印机分组被称为 *类*（classes）。安装打印机后，你可以将它们分组到不同的类中。例如，你可能希望将所有喷墨打印机归为一个类，将激光打印机归为另一个类；或者，你可能希望将连接到特定打印机服务器上的打印机归入它们自己的类。要创建一个类，请在管理页面中选择 Classes（类），并输入类的名称。然后你可以向其中添加打印机。

## CUPS 配置

CUPS 配置文件位于 `/etc/cups` 目录中。这些文件列在表 25-1 中。`classes.conf`、`printers.conf` 和 `client.conf` 文件可以通过 Web 界面进行管理。`printers.conf` 文件包含已安装的不同打印机的配置信息。如果你愿意，也可以手动编辑这些文件中的任何一个。

### cupsd.conf

CUPS 服务器使用位于 `/etc/cups` 中的 `cupsd.conf` 文件进行配置。你必须手动编辑配置选项；服务器不能通过 Web 界面进行配置。你的 CUPS 安装会安装一个带有注释的 `cupsd.conf` 文件版本，其中列出了每个选项，尽管大多数选项会被注释掉。被注释的行前面有一个 `#` 符号。每个选项都有详细的文档说明。服务器配置使用 Apache Web 服务器语法，由一组指令组成。与 Apache 一样，其中的几个指令可以将其他指令分组到块中。

表 25-1: CUPS 配置文件

| 文件名 | 描述 |
|---|---|
| classes.conf | 不同本地打印机类的配置 |
| client.conf | 列出特定客户端的特定选项 |
| cupsd.conf | 配置 CUPS 服务器，cupsd |
| printers.conf | 可用本地打印机的打印机配置 |

## CUPS 指令

某些指令允许你在特定位置设置访问控制。这些位置可以是打印机，也可以是资源，例如管理工具或后台目录。位置控制通过 `Location` 指令实现。`Allow From` 和 `Deny From` 指令可以允许或拒绝特定主机的访问。CUPS 支持 Basic（基本）和 Digest（摘要）两种身份验证形式，在 `AuthType` 指令中指定。Basic 身份验证使用用户名和密码。例如，要使用 Web 界面，你会被提示输入 root 用户和 root 用户密码。Digest 身份验证利用用户名和密码

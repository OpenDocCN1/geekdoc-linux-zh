

后续页面会提示你输入打印机型号和驱动程序，你可以从可用列表中选择。一旦添加了打印机，你就可以对其进行配置。点击管理页面中的“管理打印机”条目会列出已安装的打印机。然后你可以点击一台打印机来显示一个页面，让你控制该打印机。你可以停止打印机，配置其打印，修改其安装，甚至删除打印机。点击“配置打印机”按钮会显示一个页面，你可以在其中通过指定分辨率或纸张大小来配置打印机的打印方式。

打印机的配置信息将存储在 /etc/cups/printers.conf 文件中。你可以直接查看此文件，甚至进行更改。下面是一个打印机配置条目的示例。请注意，它是使用 redhat-config-printer 创建的。它当前处于空闲状态，队列中没有任何内容：

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
Klimit 0
</Printer>
```

DeviceURI 条目指定所使用的设备，在本例中为 lp0 并行设备。对于远程打印机，此条目将包含 Internet 地址以及协议。例如，CUPS 服务器上的远程打印机（ipp）将如图所示进行指示（Windows 打印机将使用 smb 协议）：

```
DeviceURI ipp://mysuff.com/printers/queue1
```

> 注意 你可以使用 lpadmin 命令从命令行执行所有管理任务。有关更多详细信息，请参阅 CUPS 文档。

## 在 CUPS 上配置远程打印机

要安装连接到 Windows 系统或运行 CUPS 的另一台 Linux 系统的远程打印机，你需要使用特殊的 URL 协议指定其位置。对于 Windows 打印机，你首先需要安装、配置并运行 Samba。CUPS 使用 Samba 访问 Windows 打印机。当你在 CUPS 上安装 Windows 打印机时，你使用 smb URL 协议指定其位置。允许登录打印机的用户在主机名之前输入，并用 @ 符号与之分隔。在大多数配置中，这是 guest 用户。名为 myhp 的 Windows 打印机连接到名为 lizard 的 Windows 主机的位置条目如图所示。其 Samba 共享引用为 //lizard/myhp。

```
smb://guest@lizard/myhp
```

要启用 Samba 上的 CUPS，你还必须将 /etc/samba/smb.conf 文件中的 printing 选项设置为 cups，如下所示：

```
printing = cups
printcap name = cups
```

要启用 CUPS 与 Samba 协同工作，你必须将 smbspool 链接到 CUPS smb  spool 目录：

```
ln -s /usr/bin/smbspool  /usr/cups/backend/smb
```

要访问连接到运行 LPRng 的 Linux 或 Unix 系统的打印机，请使用 lpd 协议指定其位置。在以下示例中，打印机 mylaser 连接到 Linux 主机 rabbit.mytrek.com：

```
lpd://rabbit.mytrek.com/mylaser
```

## CUPS 打印机类

CUPS 提供了一种让你选择一组打印机来打印作业而不是只选择一台打印机的方法。这样，如果一台打印机忙碌或停机，另一台打印机可以自动被选中来执行作业。这样的打印机分组称为类。一旦你安装了打印机，你就可以将它们分组到不同的类中。例如，你可能希望将所有喷墨打印机分组到一个类中，将激光打印机分组到另一个类中，或者你可能希望将连接到特定打印机服务器的打印机分组到自己的类中。要创建类，请在管理页面上选择“类”并输入类的名称。然后你可以向其中添加打印机。

## CUPS 配置

CUPS 配置文件放置在 /etc/cups 目录中。这些文件列在表 25-1 中。classes.conf、printers.conf 和 client.conf 文件可以通过 Web 界面进行管理。printers.conf 文件包含已安装的不同打印机的配置信息。如果需要，可以手动编辑这些文件中的任何一个。

### cupsd.conf

CUPS 服务器使用位于 /etc/cups 中的 cupsd.conf 文件进行配置。你必须手动编辑配置选项；服务器无法通过 Web 界面进行配置。你的 CUPS 安装会安装一个带注释的 cupsd.conf 文件，其中列出了每个选项，尽管大多数选项将被注释掉。注释行以 # 符号开头。每个选项都有详细说明。服务器配置使用 Apache Web 服务器语法，由一组指令组成。与 Apache 一样，其中几个指令可以将其他指令分组到块中。

| Filename | Description |
|---|---|
| classes.conf | Configurations for different local printer classes |
| client.conf | Lists specific options for specified clients |
| cupsd.conf | Configures the CUPS server, cupsd |
| printers.conf | Printer configurations for available local printers |


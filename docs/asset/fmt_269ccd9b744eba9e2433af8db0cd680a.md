
# 使用 chkconfig 查看服务状态

您可以使用 `chkconfig` 查看所有服务的状态，包括通过 `xinetd` 启动的服务。例如，您可以通过键入以下命令查看所有服务的状态：

```
chkconfig --list | more
```

以下是典型的输出：

```
apm 0:off 1:off 2:on 3:on 4:on 5:on 6:off
kudzu 0:off 1:off 2:off 3:on 4:on 5:on 6:off
syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
rawdevices 0:off 1:off 2:off 3:on 4:on 5:on 6:off
netfs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
network 0:off 1:off 2:on 3:on 4:on 5:on 6:off
random 0:off 1:off 2:on 3:on 4:on 5:on 6:off
saslauthd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
microcode_ctl 0:off 1:off 2:on 3:on 4:on 5:on 6:off
keytable 0:off 1:on 2:on 3:on 4:on 5:on 6:off
```

```
anacron    0:off 1:off 2:on 3:on 4:on 5:on 6:off
atd        0:off 1:off 2:off 3:on 4:on 5:on 6:off
irda       0:off 1:off 2:off 3:off 4:off 5:off 6:off
snmpd      0:off 1:off 2:off 3:off 4:off 5:off 6:off
... many lines of output deleted ...
```

输出显示了每个服务在 0 到 6 各运行级别的状态。对于每个运行级别，服务要么是 `on` 要么是 `off`。在列表的最后，`chkconfig` 显示 `xinetd` 控制的服务列表。每个基于 `xinetd` 的服务也标记为 `on` 或 `off`，具体取决于 `xinetd` 是否配置为启动该服务。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_632_0.png)

请注意，服务通常可以配置为在 `xinetd` 下运行或以独立方式运行。例如，在 8.1 版本之前，Red Hat Linux 使用 `xinetd` 控制启动 FTP 服务。然而，从 8.1 版本开始，非常安全的 FTP 服务器 `vsftpd` 被设置为独立服务器。如今，如果您必须启动 FTP 服务，请键入 `service vsftpd start`。要在启动时自动启动 FTP 服务，请键入 `chkconfig vsftpd on`。

## 使用 Red Hat 服务配置实用程序

如果您不喜欢键入 `chkconfig` 命令，您可以使用图形服务配置实用程序程序来配置服务。要运行服务配置实用程序，请以 root 身份登录并从 GNOME 或 KDE 桌面选择 主菜单→系统设置→服务器设置→服务。然后您可以从服务配置窗口打开或关闭服务（如图 1-2 所示）。

图 1-2：从服务配置窗口，您可以设置服务在启动时自动启动。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_632_1.png)

服务配置实用程序以滚动列表的形式显示服务名称。列表中的每一行都显示一个服务的名称，并在名称前有一个方框。方框中的复选标记表示该服务已被选中，以便在当前运行级别下启动时启动。首次出现对话框时，许多服务已被选中。

您可以上下滚动列表并单击方框以选择或取消选择服务。如果单击方框，复选标记会交替打开和关闭。要了解有关服务的更多信息，请单击服务名称，简要说明会出现在窗口右侧。例如，图 1-2 显示了 `atd` 服务的帮助文本。此外，该实用程序还会显示所选服务当前是否正在运行。

在选择系统启动时要启动的所有服务后，单击工具栏上的“保存”以保存更改。然后选择“文件→退出”以退出。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_633_0.png)

默认情况下，服务配置实用程序为当前运行级别配置所选服务。这意味着如果您从图形桌面执行此操作，系统处于运行级别 5，并且您配置的服务将设置为在运行级别 5 启动。如果您想为不同级别设置服务，请从“编辑运行级别”菜单中选择该运行级别。

表 1-1 显示了服务的列表以及每个服务的简要说明。第一列显示服务的名称，该名称与提供该服务所需运行的程序的名称相同。当您在系统上运行服务配置实用程序时，您可能看不到其中所有服务，因为服务的确切列表取决于安装在您的 Red Hat Linux 系统上的内容。

Table 1-1

Red Hat Linux 中的一些常见服务

| 服务名称 | 描述 |
|---|---|
| aep1000 | 加载并卸载名为 AEP1000 的加速加密处理卡的驱动程序，该卡可以快速进行加密（仅在系统已安装该卡时使用）。 |
| anacron | 执行按计划定期运行的命令。 |
| apmd | 监视高级电源管理（APM）BIOS 并记录电力状态（交流电或电池备份）。 |
| atd | 运行由 `at` 和 `cron` 命令安排的命令。 |
| autofs | 自动挂载文件系统（例如，当您将 CD-ROM 插入 CD-ROM 驱动器时）。 |
| 服务名称 | 描述 |
|---|---|
| bcm5820 | 加载并卸载 Broadcom 的 BCM5820 Cryptonet SSL（安全套接字层）加速芯片的驱动程序（仅在已安装硬件时使用此服务）。 |
| crond | 根据 `crontab` 命令设定的周期性计划运行用户指定的程序。 |
| cups | 运行通用 UNIX 打印系统（CUPS）守护进程（`cupsd`）。 |
| cups-lpd | 使应用程序能够使用旧版 LPD（行式打印机守护进程）协议与 CUPS 通信。 |
| finger | 回答 `finger` 协议请求（用于用户信息，例如登录名和上次登录时间）。您必须启用 `xinetd` 才能运行此服务。 |
| firstboot | 首次启动 Red Hat Linux 时运行，并允许您设置日期和时间、创建用户帐户、注册 Red Hat Network 并安装其他 CD-ROM。 |
| gpm | 启用在文本模式屏幕中使用鼠标。 |
| httpd | 这是 Apache 万维网（WWW）服务器。 |
| imap | 允许远程 IMAP（Internet 消息访问协议）客户端下载邮件消息。您必须启用 `xinetd` 才能运行此服务。 |
| imaps | 允许支持安全套接字层（SSL）的远程 IMAP（Internet 消息访问协议）客户端安全地下载邮件消息。您必须启用 `xinetd` 才能运行此服务。 |
| innd | 这是 InterNetNews 守护进程——您可用于在系统上支持本地新闻组的 Internet 新闻服务器。 |
| ipop3 | 允许远程 POP3（邮局协议版本 3）客户端下载邮件消息。您必须启用 `xinetd` 才能运行此服务。 |
| iptables | 使用 `iptables` 自动化数据包过滤防火墙。 |
| irda | 支持 Linux 中与 IrDA 兼容的红外设备的通信。（IrDA 是红外无线通信的标准，速度范围从 2400bps 到 4Mbps。） |
| irqbalance | 将中断分配给多处理器系统中的处理器，以在处理器之间平衡负载。 |
| isdn | 启动和停止 ISDN（综合业务数字网）服务——通过普通电话线路的数字通信服务（仅在您拥有 ISDN 服务时启用）。 |
| keytable | 按 `/etc/sysconfig/keyboard` 文件中指定的方式加载所选键盘映射。您应让此服务在系统上保持运行。 |
| kudzu | 探测新硬件并配置已更改的硬件。 |

## 表 1-1（续）

| 服务名称 | 描述 |
|---|---|
| lisa | 启动和停止 LAN 信息服务器（LISa）守护进程，该守护进程可以通过在 TCP 端口 7741 广播来显示局域网（LAN）中主机信息。欲了解有关 LISa 的更多信息，请访问 `lisa-home.sourceforge.net`。 |
| messagebus | 运行 D-BUS 守护进程，使应用程序能够接收系统事件的通知，例如新硬件设备的添加。欲了解有关 D-BUS 的更多信息，请参阅 `www.freedesktop.org/software/dbus/`。 |
| named | 这是域名系统（DNS）的服务器，可将主机名转换为 IP 地址。如果您愿意，可以在系统上运行一个副本。 |
| netfs | 使您能够挂载和卸载所有网络文件系统（NFS、Samba 和 Netware）。 |
| network | 使您能够激活或停用配置为在系统启动时启动的所有网络接口。 |

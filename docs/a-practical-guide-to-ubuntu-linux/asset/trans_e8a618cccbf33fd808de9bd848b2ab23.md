
一旦你重启 cupsd，远程系统就可以使用 `Listen` 指令指定的 IP 地址和端口号在本地系统的打印机上打印。如果服务器运行着防火墙，则你需要允许远程系统通过防火墙连接；请参见第 549 页。

或者，你可以使用 CUPS 的访问控制列表（ACL）仅允许指定的机器连接到本地打印机。访问控制列表定义在 `<Location>` 容器内部（Apache 的等效方法请参见第 918 页）。以下示例仅允许 IP 地址为 192.168.1.101 的系统和本地系统打印指定的打印机：

```
<Location /printers>
Order Allow,Deny
Allow from localhost
Allow from 192.168.1.101
</Location>
```

`/printers` 表示该容器引用所有本地打印机。或者，你也可以通过指定 `/printers/printer-name` 来按打印机单独控制访问权限（其中 `printer-name` 是打印机名称），或者通过指定 `/paths/path.ppd`（其中 `path.ppd` 是打印机使用的 PPD 文件的全名，参见第 561 页）。

`Order Deny,Allow` 指令默认允许访问，仅对 `Deny from` 指令中指定的客户端拒绝访问。`Order Allow,Deny` 指令默认允许打印请求，并允许来自指定地址的请求。你可以在 `Allow from` 和 `Deny from` 指令中使用域名、通配符和 IP 掩码。这些指令的工作方式与在 Apache 中相同。更多信息请参阅第 931 页的“Order”。

使用 `Order Deny,Allow` 指令，`Deny from` 指定了 CUPS 不接受连接的唯一 IP 地址。当你使用 `Order Allow,Deny` 指令时，`Allow from` 指定了 CUPS 接受连接的唯一 IP 地址。

## 从 Windows 打印

本节解释了如何从 Windows 机器使用 Linux CUPS 服务器上的打印机。与使用 Samba 从 Windows 打印相比，CUPS 更容易管理并且可以更安全。

## 使用 CUPS 打印

现代版本的 Windows（2000 及更高版本）支持 IPP，因此你可以直接与 CUPS 通信。要使用此功能，你需要在 Linux 打印服务器上配置 CUPS 以允许远程 IPP 打印；你还需要在 Windows 系统上创建一个新的打印机，指向 Linux 打印服务器的 IP 地址。

## 从 Windows 打印

首先，设置 `/etc/cups/cupsd.conf` 文件以允许客户端进行网络打印，如第 55 页的“共享 CUPS 打印机”部分所示。配置 CUPS 允许来自 Windows 机器打印与允许来自 Linux 客户端系统打印完全相同。如有必要，请按照第 549 页的说明打开防火墙。从 Windows XP 开始，转到控制面板 > 打印机并点击“添加打印机”。在介绍窗口中点击“下一步”，选择“网络打印机或连接到另一计算机的打印机”。点击“下一步”。选择“连接家庭或办公室网络上的打印机”，并在标记为 URL 的文本框输入以下信息：

```
`http://hostname:631/printers/printer-name`
```

其中 `hostname` 是 Linux CUPS 服务器系统的名称或 IP 地址，`printer-name` 是该系统上打印机的名称。例如，对于 IP 地址为 192.168.0.12 的名为 dog 的系统上名为 dog88 的打印机，你可以输入 `http://dog:631/printers/dog88` 或 `http://192.168.0:631/printers/dog88`。如果你使用主机名，它必须在 Windows 机器的 hosts 文件中定义。Windows 要求你指定打印机的制造商和型号，或为打印机提供驱动程序。如果你提供了打印机驱动程序，请使用 Windows 版本的驱动程序。

在 Windows 复制某些文件后，打印机出现在“打印机”窗口中。右键点击打印机并选择“设为默认打印机”。你可以通过右键点击打印机并选择“属性”来指定打印内容、位置和其他属性。

## 使用 Samba 打印

本节假设 Samba（第 797 页）已安装并运行在你想要从 Windows 使用的 Linux 系统上。Samba 必须配置为将进行打印的 Windows 用户映射到 Linux 用户（包括将 guest 用户映射到 Linux 用户 nobody）。确保这些用户使用 Samba。Windows 通过 SMB 共享打印机，从而在 Windows 系统之间以与文件共享相同的机制透明地共享打印机。Samba 允许 Windows 用户连接到 Linux 系统的打印机，就像使用其他共享打印机一样。因为所有 Linux 打印机通常都是 Postscript 打印机，所以 Linux 服务器似乎共享了 Postscript 打印机。Windows 不包含通用的 Postscript 打印机驱动程序。相反，Windows 必须为 Postscript 打印机选择一个驱动程序。Apple Laser 驱动程序是一个很好的选择。

当你安装 Samba 时，`postinst` 脚本创建一个名为 `/var/spool/samba` 的目录，该目录由 root 账户所有，任何人都可以读写。该目录设置了粘滞位（sticky bit，第 74 页），允许启动打印任务的 Windows 用户删除该任务，但拒绝删除其他用户的打印任务。确保此目录存在并具有正确的所有权：

```
$ ls -ld /var/spool/samba
drwxrxr-x 2 root root 4096 [日期] /var/spool/samba
...
[global]
  printing = cups
  printcap = cups
```

在 `/etc/samba/smb.conf` 文件的 `[global]` 部分放置以下两行：

```
[global]
  printing = cups
  printcap = cups
```

打印机的共享列在 `smb.conf` 的 `[printers]` 部分。在接下来的示例中，`path` 使用 spool 目录而不是普通共享。设置允许任何人（包括 guest）使用打印机。smb.conf 文件中的 `[printers]` 部分包含以下条目，适用于大多数设置：

```
comment = All Printers
path = /var/spool/samba
browseable = no
guest = no
writable = no
printable = yes
```

理想情况下，每个计划打印的用户都有一个账户。否则，多个用户共享同一个账户（例如 nobody 账户），他们可以删除彼此的打印任务。

## 到 Windows

Windows 通过 SMB 共享打印机，从而在 Windows 系统之间以与文件共享相同的机制透明地共享打印机。Samba 允许 Windows 用户连接到 Linux 系统的打印机，就像使用其他共享打印机一样。因为所有 Linux 打印机通常都是 Postscript 打印机，所以 Linux 服务器似乎共享了 Postscript 打印机。Windows 不包含通用的 Postscript 打印机驱动程序。相反，Windows 必须为 Postscript 打印机选择一个驱动程序。Apple Laser 驱动程序是一个很好的选择。

理想情况下，每个计划打印的用户都有一个账户。否则，多个用户共享同一个账户（例如 nobody 账户），他们可以删除彼此的打印任务。

Windows 通过 SMB 共享打印机，从而在 Windows 系统之间以与文件共享相同的机制透明地共享打印机。Samba 允许 Windows 用户连接到 Linux 系统的打印机，就像使用其他共享打印机一样。因为所有 Linux 打印机通常都是 Postscript 打印机，所以 Linux 服务器似乎共享了 Postscript 打印机。Windows 不包含通用的 Postscript 打印机驱动程序。相反，Windows 必须为 Postscript 打印机选择一个驱动程序。Apple Laser 驱动程序是一个很好的选择。

Windows 通过 SMB 共享打印机，从而在 Windows 系统之间以与文件共享相同的机制透明地共享打印机。Samba 允许 Windows 用户连接到 Linux 系统的打印机，就像使用其他共享打印机一样。因为所有 Linux 打印机通常都是 Postscript 打印机，所以 Linux 服务器似乎共享了 Postscript 打印机。Windows 不包含通用的 Postscript 打印机驱动程序。相反，Windows 必须为 Postscript 打印机选择一个驱动程序。Apple Laser 驱动程序是一个很好的选择。

Windows 通过 SMB 共享打印机，从而在 Windows 系统之间以与文件共享相同的机制透明地共享打印机。Samba 允许 Windows 用户连接到 Linux 系统的打印机，就像使用其他共享打印机一样。因为所有 Linux 打印机通常都是 Postscript 打印机，所以 Linux 服务器似乎共享了 Postscript 打印机。Windows 不包含通用的 Postscript 打印机驱动程序。相反，Windows 必须为 Postscript 打印机选择一个驱动程序。Apple Laser 驱动程序是一个很好的选择。

## 章节总结

如 CUPS 等打印系统负责设置打印机。它还将打印任务从应用程序或命令行通过适当过滤器移动到相应打印机的队列中，然后打印这些任务。

CUPS 是一个基于 IPP（互联网打印协议）的跨平台打印服务器。它处理通过打印队列进行设置和发送任务。配置打印机最简单的方法是通过“打印”窗口（system-config-printer）。你也可以使用 Web 界面配置 CUPS，通过将 Web 浏览器指向连接打印机上的 `localhost:631` 来访问该界面。从 Web 界面，你可以配置打印队列并修改打印任务。

你可以从命令行使用传统的 UNIX 命令向打印机发送任务、显示队列并从队列中移除任务。此外，CUPS 提供了 `lpinfo` 和 `lpadmin` 工具，允许你从命令行配置打印机。

CUPS 和 Samba 允许你从 Windows 机器在 Linux 上打印，反之亦然。

## 练习题

- 使用什么命令可以将文件发送到默认打印机？
- 使用什么命令可以取消所有打印任务？
- 使用什么命令列出待处理的任务？
- 使用 Samba 共享 Linux 打印机的目的是？
- 列出 CUPS 支持的三种打印协议。哪一个是 CUPS 原生协议？

## 高级练习题

- 使用什么命令列出 CUPS 可用的打印机驱动程序？
- 如何在不使用打印队列的情况下将文本文件发送到第一个并行口？为什么这样做不好？
- 假设你有一个使用名为 Postscript 打印机定义 `newprinter.ppd` 的 USB 打印机。使用什么命令将打印机添加到第一个 USB 端口？
- 如何定义配额，允许每个用户每周向 `Jeter` 打印机最多打印 50 页？
- 在 `/etc/cups/cupsd.conf` 的 `<Location>` 容器内定义一组访问控制规则，允许任何位于本地系统或 `mydomain.com` 域内的人打印所有打印机。

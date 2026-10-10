
此示例共享主目录，并将其设置为用户可写。以下是如何为每个用户指定单独的 Windows 主目录：

```
[homes]
  browseable = no
  writable = yes
  path = /path/to/windows/directories
```

### 通过编辑 [printers] 部分共享打印机

[printers] 部分的工作方式与 [homes] 部分非常相似，但它定义了用于网络共享的打印机。如果存在该部分，用户将能够访问 Fedora `/etc/printcap` 文件中列出的任何打印机。

与 [homes] 部分类似，当收到打印请求时，系统会扫描所有部分以查找打印机。如果未找到共享项（在命名谨慎的情况下，除非你为特定打印机创建了部分，否则不应该存在），则系统会扫描 `/etc/printcap` 文件以查找打印机名称，随后使用该名称发送打印请求。

为了确保打印正常工作，必须在你的 Fedora 计算机上正确设置打印服务。典型的 [printers] 部分如下所示：

```
[printers]
  comment = Fedora Printers
  browseable = no
  printable = yes
  path = /var/spool/samba
```

/var/spool/samba 是专为 Samba 打印设置的暂存路径。

### 使用 testparm 命令测试 Samba

创建 `/etc/smb.conf` 文件后，你可以检查其正确性。使用 `testparm` 命令来完成此操作。该命令解析 `/etc/smb.conf` 文件并检查是否存在任何语法错误。如果没有发现错误，你的配置文件应该能正常工作。然而，它并不保证文件中指定的服务一定会正常工作。它只是确保文件书写正确。

与所有配置文件一样，如果你正在修改一个现有且可工作的文件，总是明智的做法将可工作的文件复制到另一个位置并修改该副本。然后你可以使用 `testparm` 实用工具检查文件。命令语法如下：

```
# testparm /path/to/smb.conf.back-up
Load smb config files from smb.conf.back-up
Processing section "[homes]"
Processing section "[printers]"
Loaded services file OK.
```

此输出表明 Samba 配置文件是正确的。只要 Fedora 机器上的所有服务都正确运行，Samba 就应该能正常工作。现在，将旧的 `smb.conf` 文件复制到新位置，将新文件放在原处，并使用命令 `/etc/init.d/smb restart` 重启 Samba。此时，你的新 Samba 配置或修改后的配置应该已就位。

### 启动 smbd 守护进程

现在你的 `smb.conf` 文件已正确配置，你可以启动 Samba 服务器守护进程。你可以使用 `/usr/sbin/smbd` 命令来完成，该命令（不带任何选项）将以默认设置启动 Samba 服务器。你在此命令中更改的最常见选项是 `smb.conf` 文件的位置；如果你不想使用默认位置 `/etc/smb/smb.conf`，则需更改此选项。`-s` 选项允许你更改 Samba 使用的 `smb.conf` 文件；此选项对于测试新的 `smb.conf` 文件是否实际有效也很有用。另一个有用的选项是 `-l` 选项，它指定 Samba 用于存储信息的日志文件。

要从命令行启动、停止或重启 Samba，请使用 `service` 命令、`system-config-services` 客户端，或使用带有适当关键字（如 `start`）的 `/etc/rc.d/init.d/smb` 脚本，如下所示：

```
# /etc/rc.d/init.d/smb start
```

### 使用 smbstatus 命令

`smbstatus` 命令报告当前 Samba 连接的状态。其语法如下：

```
/usr/sbin/smbstatus [options]
```

表 19.2 列出了部分可用选项。

| 选项 | 结果 |
| :----- | :----- |
| -b | 简要输出。 |
| -d | 详细输出。 |
| -s /path/to/config | 如果启动时使用的配置文件不是标准文件，则使用此选项。 |
| -u username | 显示特定用户的连接状态。 |
| -p | 列出当前的 smb 进程。这在脚本中可能很有用。 |

### 使用 smbclient 命令连接

`smbclient` 命令允许其他 Linux 主机上的用户访问你的 `smb` 共享。你无法在主机上挂载该共享，但可以以类似使用 FTP 客户端的方式使用它。`smbclient` 命令可以使用多个选项。

最常用的是 `-I`，后跟你要连接的计算机的 IP 地址。运行 `smbclient` 命令不需要 root 权限：

`smbclient -I 10.10.10.20 -U username\password`

这将提供以下提示符：

`smb: <当前共享上的目录>`

从这里开始，命令几乎与标准的 UNIX/Linux FTP 命令相同。请注意，你可以在 `smbclient` 命令中省略密码。然后系统会提示你输入 Samba 共享密码。

### 挂载 Samba 共享

将 Samba 共享挂载到 Linux 主机有两种方法。挂载共享与挂载可用的媒体分区或远程 NFS 目录相同，不同之处在于你使用 SMB 来访问 Samba 共享。（参见第 35 章“管理系统”，了解如何挂载分区。）第一种方法使用标准的 Linux mount 命令：

```
mount -t smbfs //10.10.10.20/homes /mount/point -o username=ahudson, dmask=777, fmask=777
```

> 注意
> 如果你的名称服务正在运行，或者主机在你的 `/etc/hosts` 文件中，你可以使用主机名代替 IP 地址。

此命令在你的主机上挂载 ahudson 的主目录，并授予所有用户对该挂载点的完全权限。这些权限等同于 `chmod` 命令上的权限。

第二种方法产生相同的结果，使用 `smbmount` 命令如下：

```
# smbmount //10.10.10.20/homes /mount/point -o username=ahudson, dmask=777, fmask=777
```

要卸载共享，请使用标准的：

```
# umount /mount/point
```

这些挂载命令也可以用于将真正的 Windows 客户端共享挂载到你的 Fedora 主机。使用 Samba，你可以配置服务器提供 Windows 能提供的任何服务，除了你之外，没有人会知道。

## Fedora 的网络和远程打印

第 8 章“使用 Fedora 打印”讨论了如何设置和配置本地打印机及相关打印服务。本节涵盖为共享和网络访问配置打印机的内容。

世界各地的办公室都受益于使用打印服务器和共享打印机。在我的办公室里，我有两台通过 Mac mini（装有 Fedora PFC）连接到网络的打印机，这样我的妻子可以通过无线链接从楼下打印，而我可以从办公室的三台计算机打印。这是一件简单的事情，即使在小型环境中也能带来实际的生产力效益。

设置远程打印服务涉及配置打印服务器，然后在网络中的一台或多台计算机上创建远程打印机条目。本节介绍了一种快速方法，用于启用从一个 Linux 工作站到局域网中另一台 Linux 计算机的打印。你还将了解使用 Samba 及其实用工具进行 SMB 打印的内容。最后，本节讨论了如何配置网络附件打印机并使用它们打印单个或多个文档。

## 在局域网启用网络打印

要在局域网中设置从一个 Linux 工作站到另一个 Linux 主机的打印，你需要 root 权限以及对两台计算机的访问权限，但过程简单且易于执行。

首先，登录或通过 ssh 连接到连接打印机的计算机。这台计算机是打印服务器。使用主机名或 ifconfig 命令获取主机名或 IP 地址，并记下或标注打印机队列的名称。如果系统使用 Lpd 而不是 CUPS（通用 UNIX 打印系统），你需要编辑名为 /etc/lpd.perms 的文件。滚动到文件末尾，查找远程权限条目：

```
# allow local job submissions only
REJECT SERVICE=X NOT SERVER
```

默认情况下未启用远程打印，因此你必须用井号（#）注释掉服务拒绝行：

```
# allow local job submissions only
#REJECT SERVICE=X NOT SERVER
```

保存文件，然后重启 lpd 守护进程。

这允许来自任何远程主机的、具有正确队列名称（本地打印机名称）的传入打印请求被路由到打印机。完成后，注销并前往局域网中另一台未连接打印机的远程计算机。

![](img/34e72348d53ca54c2a1d9c871316691b_460_0.png)




## 启动 smbd 守护进程

既然你的 smb.conf 文件已正确配置，就可以启动 Samba 服务器守护进程了。这可以通过 `/usr/sbin/smbd` 命令完成，该命令（不带选项）会以所有默认设置启动 Samba 服务器。此命令中最常更改的选项是 smb.conf 文件的位置；如果你不想使用默认位置 `/etc/smb/smb.conf`，可以更改此选项。`-s` 选项允许你更改 smb.conf 文件的位置；此选项对于测试新的 smb.conf 文件是否实际有效也很有用。另一个有用的选项是 `-l` 选项，它指定 Samba 用于存储信息的日志文件。

要从命令行启动、停止或重启 Samba，请使用 `/etc/init.d/samba` 脚本并附带适当的关键字，例如 `start`，如下所示：

```
$ sudo /etc/init.d/samba start
```

## 使用 smbstatus 命令

`smbstatus` 命令报告 Samba 连接的当前状态。语法如下：

```
/usr/bin/smbstatus [options]
```

表 16.2 显示了一些可用选项

### 表 16.2 smbstatus 选项

| 选项 | 结果 |
|---|---|
| -b | 简洁输出 |
| -d | 详细输出 |
| -s /path/to/config | 如果启动时使用的配置文件不是标准配置文件，则使用此选项 |
| -u username | 显示特定用户连接的状态 |
| -p | 列出当前的 smb 进程，这在脚本中很有用 |

## 使用 smbclient 命令连接

`smbclient` 命令允许其他 Linux 主机上的用户访问你的 smb 共享。你不能在主机上挂载该共享，但可以像使用 FTP 客户端一样使用它。`smbclient` 命令可以使用多个选项。最常用的是 `-I`，后跟你要连接的计算机的 IP 地址。`smbclient` 命令不需要 root 权限即可运行：

## 挂载 Samba 共享

有两种方法可以将 Samba 共享挂载到你的 Linux 主机。挂载共享与挂载可用的媒体分区或远程 NFS 目录相同，不同之处在于 Samba 共享是使用 SMB 访问的。第一种方法使用标准的 Linux `mount` 命令：

```bash
$ sudo mount -t smbfs //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,\
  fmask=777
```

> **注意**
> 
> 如果你的名称服务正在运行或者该主机在你的 `/etc/hosts` 文件中，你可以用 IP 地址代替主机名。

此命令将 ahudson 的主目录挂载到你的主机上，并给予所有用户对该挂载点的完全权限。这些权限等同于 `chmod` 命令的权限。

第二种方法使用 `smbmount` 命令产生相同的结果，如下所示：

```bash
$ sudo smbmount //10.10.10.20/homes /mount/point -o username=ahudson,dmask=777,\
  fmask=777
```

要卸载该共享，请使用以下标准命令：

```bash
$ sudo umount /mount/point
```

你还可以使用这些挂载命令将真正的 Windows 客户端共享挂载到你的 Ubuntu 主机上。使用 Samba，你可以将服务器配置为提供 Windows 可以提供的任何服务，并且除了你之外没有人会知道。

## 使用 SWAT 配置 Samba

Samba 开发团队通过 *Samba Web 管理工具（SWAT）* 大大简化了 Samba 的管理工作。SWAT 是一个基于 Web 的配置和维护界面，尽可能接近点选式的 Samba 环境。本节提供一个简单示例，演示如何使用 SWAT 设置对用户主目录的 SMB 访问，以及如何共享目录。

> **注意**
> 
> 使用 SWAT 需要你安装 `openbsd_inetd` 和 `swat` 软件包，因此请确保在继续之前已安装这些软件包。
> 
> 此外，你需要通过使用命令 `sudo passwd root` 为 root 账户设置密码来启用该账户。不启用 root 账户将阻止你有效地使用 SWAT。

在开始使用 SWAT 之前，你需要执行几个步骤。首先，确保你已安装 Samba 和 swat 软件包。然后启用 SWAT 对你的


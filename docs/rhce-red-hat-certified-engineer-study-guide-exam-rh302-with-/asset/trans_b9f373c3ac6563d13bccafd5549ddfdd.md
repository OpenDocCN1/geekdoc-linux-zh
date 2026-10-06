

# Samba 服务指令

这里是一组用于设置共享目录的典型指令：

```
[cdrom]
comment = CDROM mounted in /mnt/cdrom
path = /mnt/cdrom
read only = Yes
browseable = Yes
valid users = fred, bob
```

这些指令建立了一个名为 `cdrom` 的共享，提供了对 Samba 服务器上 `/mnt/cdrom` 目录的只读访问。只有用户 `fred` 和 `bob` 可以访问该共享。如果你想创建一个公共可用的共享，请省略 `valid users` 指令并指定 `public = yes`。如果你想向组中的所有成员授予访问权限，请指定 `@group`，其中 `group` 是组名。

如果你希望能够对共享进行写入，请省略 `read only` 并指定 `writable = yes`。如果你不想在浏览器列表中（如 Windows 网络邻域）中显示共享，请指定 `browseable = No`。以下是一个打印机共享示例：

```
[printers]
comment = All Printers
path = /var/spool/samba
public = yes
guest ok = yes
admin users = bob
create mask = 0700
print ok = Yes
browseable = Yes
printable = yes
```

Samba 允许为用户方便地建立家目录。要此操作，请使用 `smb.conf` 文件中的 `homes` 节。例如：

```
[homes]
comment = Home Directories
read only = No
create mask = 0750
browseable = No
```

如果你希望 Samba 充当登录服务器，你应该定义一个 `netlogon` 共享。例如：

```
[netlogon]
comment = Samba Network Logon Service
path = /home/netlogon
guest ok = Yes
browseable = No
locking = No
```

# 客户端配置与使用

如果 Samba 服务器配置正确，你应该能够能够在 Windows 9x 客户端的“网络邻域”中查看可浏览的共享，将它们映射到驱动器器，并按照通常方式拖放文件。

要从 Linux 宿主机访问 Samba 服务器或 Windows 9x/NT 服务器，请执行如下形式的命令：

```
smbount //server/share /mount_point
```

其中 `server` 是服务器名称，`share` 和 `mount_point` 是应成为挂载点的本地目录。

共享以执行 `smbount` 命令的用户相关的权限进行挂载。为了允许非特权用户使用共享，你可以修改 `smbnt` 和 `smbumbd` 的权限以设置uid（模式 4755）。但是，你可能倾向于安装 `smclient` 并指示用户使用 `smclient`；要使用 `smclient` 访问共享，请执行如下形式的命令：

```
smclient //server/share
```

其中 `server` 是服务器主机，`share` 是共享名称。

# 高级服务器配置

运行 Windows 95 OSR2、Windows 98 以及带有 Service Pack 3 及更高版本的 Windows NT 的 SMB 客户端使用加密密码，这与 Samba 的默认配置不兼容。你可以通过多种方式兼容此类客户端：

- 配置客户端宿主机使用明文密码。然而，这样做可能会损害安全性。
- 使用 Windows NT 主域控制器 (PDC) 进行身份验证，并配置 Samba 使用加密密码。
- 配置 Samba 使用加密密码并维护一个包含加密密码的文件。

有关配置 Samba 使用加密密码的信息，请参阅位于 `/usr/doc/samba/docs` 的 `ENCRYPTION` 文件。

# 管理

Samba 的主管理脚本是 `/etc/rc.d/init.d/smb`。通过带有适当参数调用此脚本，你可以控制 Samba 服务器。

# 启动与重启 Samba

启动 Samba 服务器，执行命令：

```
/etc/rc.d/init.d/smb start
```

重启 Samba 服务器，执行命令：

```
/etc/rc.d/init.d/smb restart
```

# 停止 Samba

停止 Samba 服务器，执行命令：

```
/etc/rc.d/init.d/smb stop
```

# 检查 Samba 状态

检查 Samba 服务器的状态，执行命令：

```
/etc/rc.d/init.d/smb status
```

# 日志

Samba 的启动和关闭记录在系统日志 `/var/log/messages` 中。此外，Samba 将消息记录到自己的日志文件中。Samba 日志的位置和名称在 `/etc/samba.conf` 文件中配置。通常，它们位于 `/var/log/samba`。如果 Samba 运行异常，请检查这些日志文件寻找问题线索。

# 服务故障排除

Samba 包含了用于诊断和故障排除的工具。在修订 Samba 配置文件后，你应该执行命令：

```
testparm
```

该命令检查 Samba 配置文件是否存在错误。为了确保可靠运行，你应该在启动 Samba 前纠正错误。

要列出服务器上的可用共享，执行如下形式的命令：

```
smclient -L server -N
```

其中 `server` 是服务器主机名。例如，要列出本地主机的共享，执行命令：

```
smclient -L localhost -N
```

如果没有可见共享，WINS 服务器可能没有响应。要进行调查，执行如下形式的命令：

```
nmblookup -B server _SAM
```

其中 `server` 是服务器主机。有关故障排除的更多信息，请参阅位于 `/usr/doc/samba/docs` 的 `DIAGNOSIS` 文件。




## 第 4 章 | 用户权限与许可

如果你的账户列在 `/etc/group` 的 admin 组中，你就可以运行任何管理命令。从你的普通账户开始，以下命令将在 `fdisk` 工具中打开 `/dev/sda` 硬盘。`sudo` 命令会提示你输入用户密码，即 root 密码：

```
$ sudo /sbin/fdisk /dev/sda
```

当然，任何发现 admin 组中成员用户名和密码的黑客都拥有完全的管理员权限。不过坦率地说，由于用户名不是 root，黑客可能并不知道自己拥有了什么权限。

尽管如此，这就是为什么你作为安全管理员可以配置 `/etc/sudoers` 以获得更细粒度的权限的原因之一。这是非常值得的。默认情况下，它只有 root 用户可以访问，并且被配置为只读权限。因此，你无法在任何文本编辑器中编辑它。要编辑它，你需要以 root 用户身份运行 `vis` 命令。正如其名所示，它会在 `vi` 编辑器中打开 `/etc/sudoers`，这需要对该编辑器有一定的了解。许多（如果不是大多数）入门级 Linux 都详细描述了 `vi` 编辑器的用法。

红帽企业 Linux 5 版本的此文件非常有指导意义。检查文件中的行，这些行通常是被注释掉的。这一行允许所有系统的 `users` 组成员运行所示的命令。注意每个命令都需要完整路径；即使它们位于 `/sbin/` 二进制目录中也是如此。

```
%users ALL=/sbin/mount /mnt/cdrom /sbin/mount /mnt/cdrom
```

如果你在红帽系统上进行测试，尝试更改上述显示的默认选项以包含相关命令。例如，以下替换代码允许 `users` 组成员在 `/dev/sda` 硬盘上使用 `fdisk`（仅限该硬盘），并使用 `yum` 命令更新和安装包：

```
%users ALL=/sbin/fdisk /dev/sda, /usr/bin/yum
```

关于 `/etc/sudoers` 的更多细节在此文件的红帽版本中更早通过别名（aliases）出现。威力在于为一组用户和管理命令设置别名。这里只是一个例子：假设你想设置一个具有重新设定优先级或杀死进程权限的管理员。以下命令允许将指令将适当的管理工具分配给 `PSMGMT` 别名：

```
Cmnd_Alias PSMGMT=/bin/nice,
/bin/kill, /usr/bin/kill, /usr/bin/killall
```

然后可以使用以下指令将该权限分配给具有在所有系统中使用这些命令权限的用户组：

```
%users ALL = PSMGMT
```

## 98 第 2 部分 | 分层安全与 Linux

| 表格 4-8 /etc/sudoers 中的命令组。 | |
| 变量 | 命令 |
| :--- | :--- |
| NETWORKING | route, ifconfig, ping, dhclient, net, iptables, rfcomm, wdial, ifconfig, mii-tool |
| SOFTWARE | rpm, update, yum |
| SERVICES | service, chkconfig |
| LOCATE | updated |
| STORAGE | fdisk, sfdisk, parted, partprobe, mount, um |
| DELEGATING | sudo, chown, chmod, chgrp |
| PROCESSES | nice, kill, killall |
| DRIVERS | modprobe |

标准红帽版本的 `/etc/sudoers` 在此处包含了更广泛的分配给命令别名的管理工具示例：

```
# %sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING,
PROCESSES, LOCATE, DRIVERS
```

如果被激活，此行将启用一系列广泛的管理命令的权限。表 4-8 列出了与每个变量相关的命令。它也应该让你对 Linux 中哪些基础管理命令是重要的有一个良好的了解。如果你详细了解 Linux，你可能会发现这个列表是不完整的。例如，你可以为 `iwconfig`、`iwlist` 和 `iwpy` 等命令设置它们自己的无线网络组。你可能想将 `immod` 和 `rmod` 命令添加到 `DRIVERS` 组中。

### 使用 sudo 命令

普通用户可以在 `/etc/sudoers` 文件中配置权限。上述 admin 组的成员可以从普通账户运行管理命令。例如，如果你的账户是 admin 组的成员，你可以打开本地系统上的第二个 SATA 硬盘。

### 权限与许可

普通用户可以在 `/etc/sudoers` 文件中配置权限。上述 admin 组的成员可以从普通账户运行管理命令。例如，如果你的账户是 admin 组的成员，你可以打开本地系统上的第二个 SATA 硬盘。

### 设置用户 ID (Set User ID)

普通用户可以在 `/etc/sudoers` 文件中配置权限。上述 admin 组的成员可以从普通账户运行管理命令。例如，如果你的账户是 admin 组的成员，你可以打开本地系统上的第二个 SATA 硬盘。

### 设置组 ID (Set Group ID)

普通用户可以在 `/etc/sudoers` 文件中配置权限。上述 admin 组的成员可以从普通账户运行管理命令。例如，如果你的账户是 admin 组的成员，你可以打开本地系统上的第二个 SATA 硬盘。

### 粘滞位 (Sticky Bit)

普通用户可以在 `/etc/sudoers` 文件中配置权限。上述 admin 组的成员可以从普通账户运行管理命令。例如，如果你的账户是 admin 组的成员，你可以打开本地系统上的第二个 SATA 硬盘。


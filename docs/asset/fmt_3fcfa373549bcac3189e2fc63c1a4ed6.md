
不同的系统管理命令涉及软件包，包括 `tar`, `star`, `gzip` 和 `bzip2`。作为管理员，你需要了解如何操作。

# 160 第 9 章：RHCSA 级系统管理任务

## 实验答案

### 实验 I

为了尽量减少困扰，你可以在不打开标准 KVM 窗口的情况下启动 `gamma.example.net` 系统。一种方法是使用 `virsh start gamma.example.net` 命令。然后你可以通过 SSH 连接并管理 gamma 系统。

你可以通过从物理宿主机系统运行 VNC 客户端（如 Remote Desktop Viewer 或 TigerVNC Viewer）来启动 `gamma.example.net` 系统的活动 GUI 界面，以此验证实验成功。

要做到这一点，你需要确保满足以下条件：

- VNC 服务器以用户账户身份运行。
- 相应的 TCP 端口已打开，第一个用户至少需要 `5900` 和 `5901`。
- VNC 服务器已在 `/etc/sysconfig/vncservers` 文件中配置过。
- 你已从目标用户的账户启动了 VNC 服务器。例如，从 `tester` 账户，你可以运行 `vncserver :1` 命令来启用对给定 TCP 端口的访问。

请注意，远程桌面服务器配置工具在基于 KVM 的虚拟机上存在问题。这并不是错误，至少在我个人看来如此，因为基于 KVM 的虚拟机已经使用 VNC 进行正常操作。就本实验而言，TigerVNC 服务器是在基于 KVM 的虚拟机上配置 VNC 的首选方法。如果成功，你应该能够使用 TigerVNC 客户端从物理宿主机连接。根据上述条件，你可以通过导航到 `192.168.1` 连接到 `tester` 账户的 GUI。

### 实验 II

在开始此实验之前，你可能需要安装 `tar` 命令。当 `tar` 命令保留了 ACL 和 SELinux 设置时，你可以使用 `gzip` 命令创建压缩包：

```bash
# star -czvf /home/backup/archive.tar.gz /home/
```

然后你可以使用 `gzip` 或 `bzip2` 命令对压缩包并传输到 `/var/backup` 目录。

### 实验 III

创建此类脚本的最简单方法是在 `/etc/cron` 目录下：

```bash
#!/bin/bash
ps
```

### 实验 IV

为了这个目的，在 `/etc/cron` 目录下创建一个：

```bash
# create a break 9,11 * * * root /usr/bin/wall
```

确保 `root` 用户可以执行该。

### 实验 V

此实验包含了 `/var/log` 文件中的三个简单任务，可以帮助你识别可能存在的问题。在 `anaconda_ifcfg.log` 文件中：

```bash
# grep HWADDR /root/if0
```

如果你已经更改了 GRUB 配置，你应该通过以下命令满足需求：

```bash
# grep UUID /var/log/dmesg
```

对于 DVD 的虚拟机，你应该看到以下错误行：

```
(WW) warning, (EE) error, (NI) not implemented, (??) unknown.
[23.951] (EE) open /dev/fb0: No such device
[24.963] (EE) QEMU 0.12.1 failed to initialize for relative axes.
```

img/ad9f3468206ad4765a06e762bd96b65_198_0)

## 10 安全概述

### 考试目标

- 使用 `iptables` 实现包过滤并配置网络地址转换 (`NAT`)
- 配置基于主主机和基于用户的安全
- 自测

# 第 10 章：安全概述

本章提供了安全相关目标的简要总结。事实上，你可能需要指定模式；`-s 地址` 选项可以指定源地址。同样，`-d 地址` 选项可以设置目标地址的模式。

你还可以指定协议和端口号。例如，`-m tcp -p tcp --dport 22` 用于查找发送到端口 `22` 的传输控制协议 (`TCP`) 包。事实上，这是 RHEL 6 的默认规则之一，它支持安全 Shell (`SSH`) 访问。总之，从 `/etc/sysconfig/iptables` 文件获取此选项：

当然，你可以使用 `iptables -A` 命令在链末尾添加规则；当指定了数字或模式时，可以使用 `iptables -D` 命令删除规则。（`ip6tables` 的原理类似。）

使用 `iptables` 实现包过滤并配置网络地址转换 (`NAT`)

目前的实现是基于 `iptables` 和 `ip6tables`。这些命令包含了三个基本选项：`filter`（过滤）、`nat`（转换）和 `mangle`（（标记）。在 RHCSA 目标中可以忽略 `mangle` 选项。`filter` 选项匹配协议等模式。`nat` 选项配置网络地址转换，通过修改网络数据包头部，使请求看起来来自另一个系统。

配置基于主主机和基于用户的安全

大多数基于 `iptables` 的防火墙规则基于 `filter` 选项，规则在链中组合。要列出当前活动的防火墙规则，使用 `iptables -L` 列出。如果你想清空系统中的防火墙规则，使用 `-F` 命令进行刷新。基于主主机和基于用户的安全也可以通过其他方式配置。你可以根据 `iptables` 防火墙规则在特定端口设置基于主机的的安全。某些服务

# 166 第 10 章：安全概述

包含 `/etc/xinetd.d` 目录下的配置文件，可以通过扩展互联网服务守护进程 `xinetd` 进行管理。其他服务与 TCP Wrappers 库文件 `libwrap.so.0` 关联，并可以通过 `/etc` 目录下的 `hosts.allow` 和 `hosts.deny` 文件进行管理。

要检查是否可以使用 TCP Wrappers 来保护服务，库依赖项命令 `ldd` 可以提供帮助。例如，如果你运行 `ldd /usr/sbin/vsftpd | grep libwrap.so.0` 命令，你应该会看到以下 64 位输出以确认：

```
libwrap.so.0 => /lib64/libwrap.so.0
```

记住，TCP Wrappers 会首先搜索 `/etc/hosts.allow`。如果配置了允许访问的规则，则 `/etc/hosts.deny` 中的任何相关规则都将被忽略。以下是一个可以在每个文件中可能配置的规则示例：

```
sshd : ALL EXCEPT 192.168.122.130
```

如果你将此规则添加到 `/etc/hosts.deny`，则仅允许来自指定 IP 地址的访问，该地址对应于 `whitehat.example.net` 系统。还可以通过 PAM 根据 `/etc/pam.d` 目录下的文件配置基于用户的访问。以下是来自 `/etc/pam.d/vsftpd` 的条目说明了拒绝来自 `/etc/vsftpd/ftpasswd` 用户中列出的用户访问的规则：

```
auth required pam_listfile.so item=user sense=deny \
file=/etc/vsftpd/ftpasswd onerr=succeed
```

如果你理解命令行，你会发现上面的反斜杠转义了回车符的含义，回车符在功能上等同于换行。当然，该行位于配置文件中；遗憾的是，反斜杠在该特定文件中同样有效。

为了解释，PAM 使用身份验证管理（`auth`）测试。系统必须通过测试才能继续。后续的规则基于 `/lib64/security` 目录下的 `pam_listfile.so` 库。关于该库如何工作的详细信息，可以在 `pam_listfile` 手页中找到。`item=user` 选项指定 PAM 将检查用户。如果有匹配，则应该拒绝该用户的访问（`sense=deny`）。文件是 `/etc/vsftpd/ftpasswd`。如果无法打开文件，则允许用户访问（`onerr=succeed`）。

![](img/ad9f3468206ad4765a06e762bd96b965_201_0.png)

## 认证总结

`iptables` 命令是 Linux 基于 IPv4 网络的一个关键安全功能。在 `/etc/sysconfig/iptables` 文件中配置的规则可以检查每个网络数据包的头部。根据网络设备、协议、IP 地址和端口号等特征，可以接受、拒绝或丢弃包。对于 IPv6 网络，相应的命令是 `iptables`，配置在 `/etc/sysconfig/ip6tables` 文件中。这些命令也可以用于网络地址转换（`NAT`），帮助保护私有网络上系统的身份。

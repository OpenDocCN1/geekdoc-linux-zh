
| 共享名称 | 类型 | 注释 |
| --- | --- | --- |
| homes | Disk | 用户主目录 |
| IPC$ | IPC | IPC 服务 (Samba 服务器) |
| ADMIN | Disk | IPC 服务 (Samba 服务器) |
| hp-ns1 | Printer | |
| Domain=[ESTREETJ] OS=[Unix] Server=[Samba 3.0.8-4] | | |

| | 注释 |
| --- | --- |
| PINE | Samba 服务器 |
| MAPLE | Windows XP |
| NS1 | Samba 服务器 |

| | 注释 |
| --- | --- |
| Workgroup | Master |
| ESTREET | PINE |

在本示例中，Samba 服务器运行在本地计算机上。共享目录、打印机以及工作组中的条目都会显示在这里。如果 Samba 服务器未运行，你将看到“拒绝连接”（`Connection refused`）的消息，你需要按照本章前面的描述来启动 Samba 服务。

# 防火墙打开了吗？

如果 Samba 服务器正在运行，它应该开始在你的局域网（LAN）上广播其可用性。如果你尝试从局域网上的 Windows 或 Linux 客户端访问服务器，但收到“拒绝连接”错误，那么问题可能是你的 Linux Samba 服务器上的防火墙阻止了对 NetBIOS 服务的访问。

# 交叉引用

第 27 章介绍了防火墙。■

如果你有一个安全的局域网，可以输入以下内容（作为 root 用户）临时刷新防火墙过滤规则：

```
# iptables -F
```

# 第 16 章：运行文件服务器

尝试从 Windows 或 Linux 客户端连接 Samba 服务器。如果你发现无法连接到服务器，请重新开启回退机制：

```
# /etc/init.d/iptables restart
```

你可能需要在防火墙中打开端口 137、138 和 139，以便 Samba 服务器能够接受此类服务的连接。但请记住，打开这些端口可能会为 Windows 系统带来一系列安全问题。（请参考第 27 章获取有关修改防火墙的信息。）

# 用户密码正常吗？

尝试以特定用户访问共享 Samba 目录（从本地或局域网上的其他 Linux 系统）。你可以使用 `smbclient` 命令来执行此操作。这里是一个示例：

```
# smbclient //localhost/tmp -U chris

added interface ip=10.0.0.1 bcast=10.0.0.255 nmask=255.255.255.0

Password: ********

Domain=[ESTREE] Server=[Samba 2.2.7a]

smb:\> 
```

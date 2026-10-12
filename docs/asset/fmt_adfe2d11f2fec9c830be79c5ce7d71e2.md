
`user = mapping`

其中 `user` 是 OPENUSE 用户账户，`mapping` 是 Windows 账户映射。显然，如果 Windows 账户和 OPENUSE 账户是同一个，你就不需要进行映射。

下一步是为 Samba 账户分配密码。使用 `smbpasswd` 程序为 Samba 账户分配密码。第一次创建 Samba 账户时，你必须使用 `-a` 选项：

```
testing:home/rich # smbpasswd -a rich

NEW PASSWORD:

RETYPE PASSWORD:

testing:home/rich #
```

一旦创建账户，你就可以使用该帐户/密码组合从任何 Windows 工作站或服务器登录。如果你已经使用该帐户和相同的密码登录了 Windows 工作站或服务器，那么当你映射到 Samba 资源时，将不会提示输入密码！

## 启动 Samba 服务器

如果你选择自动启动 Samba，则服务器服务（`smbd` 和 `nmbd`）将启动，并且会在每次你重启 OPENUSE 系统时重新启动。如果你选择手动启动 Samba，则必须在命令行中手动输入两个命令来启动：

```
rich:$-> su

password:

testing:home/rich # rcsmb start

testing:home/rich # rcnmb start
```

注意，你必须是 root 用户才能启动 Samba 服务服务。你可以使用 `su` 命令行切换到 root 用户账户。

第一个命令启动 Samba SMB 服务，允许远程 Microsoft（以及 Samba）客户端连接到共享资源。第二个命令启动 Samba 浏览服务。该服务在 Microsoft 网络上发布你的 Samba 服务器。你不需要发布你的 Samba 服务器，这提供了一种小程度的安全性。只有知道你的服务器名称和共享名称的客户端才能映射到 Samba 共享。

Samba 软件提供了几个命令行工具来管理 Samba 服务器。`smbstatus` 命令可以快速验证当前连接到服务器共享资源的任何客户端：

```
testing:/etc/samba # smbstatus

Samba version 3.0.23d-6-1083-SUSE-SL10.2

| PID | Username | Group | Machine |
| :--- | :--- | :--- | :--- |
| 5029 | rich | users | daniel (10.0.1.33) |

| Service | pid | machine | Connected at |
| :--- | :--- | :--- | :--- |
| rich | 5029 | daniel | Tue Jan 9 21:03:36 2007 |
| IPC$ | 5029 | daniel | Tue Jan 9 21:03:28 2007 |

Locked files:

| PidUid | DenyMode | Access | R/W | Oplock |
| :--- | :--- | :--- | :--- | :--- |
| 5029 1000 | DENY_NONE | 0x100001 | RDNLY | NONE |

| SharePath | Name | Time |
| :--- | :--- | :--- |
| /home/rich | . | Tue Jan 9 21:03:36 2007 |

testing:/etc/samba #
```

该命令会识别各个网络客户端，也会识别系统中当前正在使用的任何文件。

`smbclient` 命令提供了一种连接到 Microsoft 网络资源的快速命令行方法。你可以用它列出你 Samba 服务器上的客户端：

```
linux:/home/rich # smbclient -L localhost -N

Domain=[MYDOMAIN] OS=[Unix] Server=[Samba 3.0.23d-6-1083-SUSE-SL10.2]

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| profiles | Disk | Network Profiles Service |
| users | Disk | All users |
```

## 安全网络服务

```
groups          Disk        All groups

print$          Disk        Printer Drivers

netlogon       Disk        Network Logon Service

IPC             IPC         IPC Service (Samba 3.0.23d-6-1083-SUSE-SL10.2)\Domain=[MYDOMAIN] OS=[Unix] Server=[Samba 3.0.23d-6-1083-SUSE-SL10.2]
```

```
Server          Comment

TESTING         Samba 3.0.23d-6-1083-SUSE-SL10.2

Workgroup       Master

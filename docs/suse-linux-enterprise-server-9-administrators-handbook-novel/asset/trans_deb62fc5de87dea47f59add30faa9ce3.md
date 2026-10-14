
## 第二部分

## 用户访问与安全管理

- 4. 用户和组管理
- 5. 用户环境管理与安全
- 6. 文件系统安全
- 7. 系统管理与监控

## 用户和组管理

作为多用户系统的系统管理员，您负责的任务之一就是管理并控制用户对系统资源的访问。由于 SLES 是一个多用户系统，本章将帮助您了解用户和组是如何标识的，如何使用这些信息来确定对数据和应用程序的访问权限，以及如何有效地管理用户和组信息。本章涵盖以下主题：

- 用户和组 ID
- 系统用户与普通用户
- `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 文件
- 使用 YaST 和命令行工具创建和更新用户和组信息的方法
- 用户账户安全注意事项

### 用户和组 ID

在 SLES 中，每个用户和组都被分配一个唯一的数值，因为操作系统处理数字比处理文本字符串更容易。与用户关联的数字称为用户 ID（UID），与组分配的数字称为组 ID（GID）。默认情况下，SUSE LINUX（所有版本）为普通（非系统）用户分配的 UID 从 1000 开始，GID 分配从 100 开始。

Linux 标准将 UID 范围 0 到 99 保留给系统本身，并将范围 100 到 499 保留给特殊系统用户（如服务和应用程序）。为了留出未来扩展的空间，SUSE LINUX 因此将普通用户 ID 值从 1000 开始（并结束于 60000；默认情况下，最大上限为 65535）。表 4.1 显示了 SLES 创建的系统用户、其 UID 和其主 GID。

> **注意**
>
> 每个 Linux（和 Unix）系统都有一个特殊的特权用户称为 **root**。root 用户始终具有 UID 为 0（零）。Linux 中没有特殊的或保留的组名。

> **警告**
>
> 因为操作系统通过 UID 识别用户，所以具有相同 UID 的不同用户名被视为同一用户。因此，您可以通过为这些用户分配 UID 0 来设置额外的 root 用户。同理，如果您（或恶意者）将某个用户的 UID 改为 0，您就授予了该人对系统的无限权限。作为预防措施，您应定期审计 `/etc/passwd`（如果您使用它们进行身份验证，则包括您的 LDAP/NIS 数据库），以确保只有 root 和指定用户具有 UID 和 GID 设置为 0。第 13 章“系统安全”中提到的 Bastille 可用于自动检测未经授权的重复 root 账户。
>
> 如果您需要设置多个管理员，最好将这些用户分配到一个特殊的组（如 root 组），该组已被授予必要的权限，或者最好使用 sudo（在第 5 章“用户环境管理与安全”中讨论）。

**表 4.1**
SLES 默认系统用户设置

| 用户名 | UID | 主 GID | 描述 |
|---|---|---:|---:|
| root | 0 | 0 | The root (super) user |
| bin | 1 | 1 | Used by system services, such as lpd |
| daemon | 2 | 2 | Background service |
| lp | 4 | 7 | Printing daemon |
| mail | 8 | 12 | Mailer daemon |
| news | 9 | 13 | News system |
| uucp | 10 | 14 | Unix-to-Unix CoPy system |

**表 4.1**
SLES 默认系统用户设置（续）

| 用户名 | UID | 主 GID | 描述 |
|---|---|---:|---:|
| games | 12 | 100 | Games account |
| man | 13 | 62 | Manual pages viewer |
| at | 25 | 25 | Batch jobs daemon |
| postgres | 26 | 26 | PostgreSQL Server |
| mdom | 28 | 28 | Mailing list agent (Majordomo) |
| wwwrun | 30 | 8 | WWW daemon apache |
| squid | 31 | 65534 | WWW-proxy squid |
| amanda | 37 | 6 | AMANDA (backup utility) admin |
| irc | 39 | 65534 | IRC (Internet Relay Chat) daemon |
| ftp | 40 | 49 | FTP account<br>FTP server daemon |
| named | 44 | 44 | Name server (DNS) daemon |
| gdm | 50 | 15 | Gnome Display Manager daemon |
| postfix | 51 | 51 | Postfix daemon |
| mysql | 60 | 2 | MySQL database admin |
| vscan | 65 | 102 | Vscan account used by samba-vscan |
| pop | 67 | 100 | POP admin |
| sshd | 71 | 65 | SSH daemon |
| Mailman | 72 | 67 | GNU mailing list manager |
| Snort | 73 | 68 | Snort network monitor |
| Ntp | 74 | 65534 | NTP (Network Time Protocol) daemon |
| ldap | 76 | 70 | User for OpenLDAP |
| Hacluster | 90 | 90 | High-Availability cluster heartbeat processes |
| Cyrus | 96 | 12 | User for cyrus-imapd |
| Stunnel | 100 | 65534 | Daemon user for stunnel (universal SSL tunnel) |
| quagga | 101 | 101 | Quagga routing daemon |
| dhcpd | 102 | 65534 | DHCP server daemon |
| radiusd | 103 | 103 | Radius daemon |
| nobody | 65534 | 65533 | Special user for assigning NFS permissions |

当您登录 Linux 时，您的活动或当前 GID 设置为用户数据库（如 `/etc/passwd`）中指定的主（或默认）GID，即使您可能是多个组的成员。操作系统根据当前 GID 计算用户对文件的访问权限。您可以使用 `newgrp` 命令将活动 GID 更改为新的 GID，如下所示：

```bash
newgrp groupname
```

> **注意**
>
> 尽管通常用于将您的 UID 切换为 root 用户，`su` 命令可用于将您的活动 UID 切换为另一个用户（`su username`）。如果您当前是 root，则不需要密码；否则，您需要提供该用户的密码。

如果未给出 `groupname`，则 GID 将切换回主 GID。成功切换到新组后——您必须是该组的成员，或是 root 才能这样做——从那时起您的所有操作都将具有该新组的权限。例如，如果您创建新的文件或目录，则新文件或目录的组将为“groupname”。

执行 `newgrp` 命令后，您仍保持登录状态，当前目录不变，并创建一个新的 shell。某些 `newgrp` 实现在命令以错误终止时（例如指定了未知组时）始终会用新 shell 替换当前 shell。请考虑可能产生的混淆：您是否在新 shell 中并需要使用 `exit` 命令返回到原始 shell，还是仍在原始 shell 中，而 `exit` 命令会终止当前会话？SUSE 的实现通过在命令失败时不创建新 shell 来避免此问题。

要返回到之前的 GID 和 shell，请使用 `exit` 命令而不是 `newgrp`；否则，您将启动另一个 shell。以下说明了 `newgrp` 命令的效果：

```text
Athena:/home/admin # #display my UID, GID, and groups I belong to
Athena:/home/admin # id
uid=0(root) gid=0(root) groups=0(root),64(pkcs11)
Athena:/home/admin # #show my currently running processes
Athena:/home/admin # ps
    PID TTY          TIME CMD
   7853 pts/1    00:00:00 bash
   7875 pts/1    00:00:00 ps
Athena:/home/admin # change group to wheel
Athena:/home/admin # newgrp wheel
Athena:/home/admin # check my current settings:
Athena:/home/admin # #wheel is now my current GID
Athena:/home/admin # id
uid=0(root) gid=10(wheel) groups=0(root),10(wheel),64(pkcs11)
Athena:/home/admin # #and I have one extra bash shell running!
Athena:/home/admin # ps
    PID TTY          TIME CMD
   7853 pts/1    00:00:00 bash
   7877 pts/1    00:00:00 bash
   7885 pts/1    00:00:00 ps
Athena:/home/admin # #return to previous setting
Athena:/home/admin # exit
exit
Athena:/home/admin # #and the extra bash shell is gone too
Athena:/home/admin # id
uid=0(root) gid=0(root) groups=0(root),64(pkcs11)
Athena:/home/admin # ps
    PID TTY          TIME CMD
   7853 pts/1    00:00:00 bash
   7886 pts/1    00:00:00 ps
```

当您返回到原始 shell 时，其先前的环境（如 shell 变量和工作目录）得以保留；您将返回到在启动新 shell 之前所处的确切状态。

> **注意**
>
> 如果组有密码并且用户未在 /etc/group 文件中列为该组的成员，则会提示用户输入密码。创建组密码的唯一方法是使用 passwd 实用程序，然后将密码从 /etc/shadow 剪切并粘贴到 /etc/group。组密码已过时且不常使用，但它们为未列为成员的用户提供了承担该组身份的手段。

Linux 将 GID 范围 0 到 10 保留给系统组。与 UID 类似，默认情况下，用户创建的组从 GID 1000 开始，GID 值最高可达 60000。表 4.2 显示了 SLES 创建的系统组及其 GID。

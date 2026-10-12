
| 段落 | `smbstatus` 命令 | 520 |

| 段落 | 挂载 SAMBA 共享 | 520 |

## 定义关键术语

定义本章中的以下关键术语并在词表中检查你的答案：

服务器消息块 (`SMB`)、分布式文件系统 (`DFS`)、网络文件系统 (`NFS`)、通用互联网文件系统 (`CIFS`)、网络基本输入/输出系统 (`NetBIOS`)、活动目录

## 复习题

这些复习题的答案位于附录 A。

1. ______ 软件包提供了 SAMBA 客户端工具。

2. 下列哪些字符可以用于 `/etc/SAMBA/smb.conf` 文件中的行注释？（选择两个）

   a. `#`
   b. `*`
   c. `;`
   d. `/`

3. 当放置在 `smb.conf` 文件的 `[global]` 节时，下列哪项用于指定 SAMBA 服务器的描述？

   a. `comment =`
   b. `server =`
   c. `description =`
   d. `server string =`

4. `smb.conf` 文件的 ______ 节用于默认共享 SAMBA 用户的目录。

5. 当放置在 `smb.conf` 文件中的目录共享节时，下列哪项用于以只读方式共享目录？

   a. `read-only = yes`
   b. `unwritable = yes`
   c. `writable = no`
   d. `changeable = no`

6. `smb.conf` 文件 SAMBA 共享节中的 ______ 设置允许来宾帐户访问。

   a. `guest = yes`
   b. `unsecure = yes`
   c. `guest ok = yes`
   d. `guest access = yes`

7. 为以下 SAMBA 打印机共享填全缺失的设置：

```
[hp-101]
 = /var/spool/SAMBA/
browseable = yes
printable = yes
printer name = hp-101
```

8. 启动 SAMBA 服务器会导致两个：______

9. 填写以下空白以创建一个新用户：

   a. `-c`
   b. `-a`
   c. `-n`
   d. `-s`

10. `smb.conf` 文件的 ______ 节用于指定共享。

本章涵盖：

- 配置 NFS 服务器
- 配置 NFS 客户端
- NFS 共享

# NFS 配置

`NFS`（网络文件系统）是一种已流行 40 年的协议。它最初由太阳公司创建，用于从一个系统共享文件。在本章中，你将学习如何设置 `NFS` 服务器并连接到它。

## 基础主题

注意的是，`LPIC-2` 考试重点是 `NFS3`。大多数 Linux 发行版都带有 `NFS4`。本章侧重于 `NFS3`；包含少量的 `NFS4` 涵盖是因为有一个 `LPIC-2` 目标：“熟悉 `NFS4`”。

# 配置 NFS 服务器

在大多数 Linux 发行版中，`NFS` 软件是默认安装的；你可以通过 `nfs`、`nfsserver` 或 `nfs-kernel-service` 启动脚本启动 `NFS`（取决于发行版）。在某些情况下，你可能需要安装 `nfs-utils` 或 `nfs-kernel-server` 包，但通常 `NFS` 软件是默认安装的。

`NFS` 有一个小技巧：它需要另一个服务 `RPC`（远程过程调用）。`RPC` 在 `NFS` 客户端和服务器的交互中充当中间人。`RPC` 服务由一个名为 `portmap` 的工具提供；如果 `portmap` 服务未运行，你可能会得到类似的错误信息：

```
Cannot register service: RPC: Unable to receive; errno = Connection refused rpc.quotad: unable to register (RQUOTPROP, RQUOTAV, upd).
```

# /etc/exports 文件

`NFS` 服务器的主要配置是 `/etc/exports` 文件。这是你用于指定与 `NFS` 客户端共享哪些目录的文件。该文件的格式为

```
目录 主机 (选项)
```

目录的值应替换你想共享的目录（例如：`/usr/share/doc`）。主机应该是可以解析为 IP 地址的客户端主机名。选项值用于指定如何共享资源。

例如，`/etc/exports` 文件中的以下条目将以读写方式将 `/usr/share/doc` 共享给 `NFS` 客户端 `jupiter`，以只读方式共享给 `NFS` 客户端 `mars`：

```
/usr/share/doc jupiter(rw) mars(ro)
```

## LPIC-2 认证指南

注意，`jupiter` 和 `mars` 名字之间有一个空格，但主机与其对应的选项之间没有空格。新手管理员的一个常见错误是提供类似下面的条目：

```
/usr/share/doc jupiter (rw)
```

上一行将通过默认选项将 `/usr/share/doc` 目录共享给 `juniper` 主机，且所有其他主机都能够以 `rw`（读写）权限访问该目录。

在 `/etc/exports` 文件中指定主机名时，允许使用以下方法：

- `hostname`—可以解析为 IP 地址的主机名。
- `netgroup`—使用组名标识的 NIS 网络组。
- `domain`—使用通配符的域名。例如，`*.onecoursesource` 将包含 `onecoursesource.com` 域中的任何机器。
- `Network`—使用 `VLSM`（可变长度子网掩码）或 `CIDR`（无类域间路由）通过 IP 地址定义的网络。例如：`192.168.1.0/255.255.255.0` 或 `192.168.1.0/24`。

有许多不同的 `NFS` 共享选项，包括：

- `rw`—以读写方式共享。请记住标准的 Linux 权限仍然有效。重要：这是一个默认选项。
- `ro`—以只读方式共享。
- `sync`—文件数据更改立即写入磁盘，这会影响性能，但导致数据丢失的可能性较低。在某些发行版中这是默认选项。
- `async`—`sync` 的反；文件数据更改最初写入内存。这会提高性能，但更有可能导致数据丢失。在某些发行版中这是默认选项。
- `root_squash`—将 `NFS` 客户端的 `root` 用户和组账户映射到匿名账户（通常是 `nobody` 或 `nfsnobody` 账户）。更多细节请见下一节“用户 ID 映射”。重要：这是一个默认选项。
- `no_root_squash`—将 `NFS` 客户端的 `root` 用户和组账户映射到本地的 `root` 用户和组账户。更多细节请见下一节“用户 ID 映射”。

## 用户 ID 映射

为了使从 `NFS` 服务器到 `NFS` 客户端共享资源的过程尽可能透明，请确保两个系统使用相同的 `UID`（用户 ID）和 `GID`（组 ID）。要理解这个概念，请先看图 27-1。

![](img/a76ac3bb017d749781a228f025853f37_564_0.png)

图 27-1 NFS ID 映射——相同的用户和组名

在图 27-1 中，`NFS` 服务器和 `NFS` 客户端都具有相同的用户和组账户。两个系统对这些账户使用 `UID` `500` 和 `GID` `500`。`NFS` 服务器将 `/share` 目录共享给 `NFS` 客户端，客户端将其挂载到 `/access` 目录。当学生尝试访问 `/access/example` 文件时，该用户将对该文件拥有 `rw` 权限。

现在考虑图 27-2 中描述的情况。

![](img/a76ac3bb017d749781a228f025853f37_564_1.png)

图 27-2 NFS ID 映射——不同的用户和组名

图 27-2 示例中的 `NFS` 客户端有一个名为 `bob` 的用户和组，被分配给 `/access/example` 文件。这意味着当 `NFS` 客户端访问 `/access/example` 文件时（实际上是 `/share/example`），`bob` 被授予了该文件的所有权访问。换句话说，`NFS` 客户端上的用户 `bob` 对由 `NFS` 服务器上的学生拥有的文件具有读取和写入权限！

这就是为什么你不在局域网（`LAN`）之外使用 `NFS` 的原因之一。还有其他原因（如安全问题），但理解这种 `UID` 和 `GID` 映射是理解 `NFS` 的一个重要方面。

注意：避免账户不匹配的一种方法是使用中央认证系统，例如 `NIS` 或 `LDAP` 服务器。`NIS` 不是考试目标，但 `LDAP` 包含在第 29 节“PAM 认证”和第 30 节“配置 LDAP 服务器”中。

回想 `/etc/exports` 文件的一个共享选项是 `root_squash`。这是因为你可能不希望 `NFS` 客户端上的 `root` 账户在 `NFS` 服务器上拥有 `root` 权限。`root_squash` 共享选项会导致一种罕见情况，即普通用户对文件系统上某些内容的拥有的权限比 `root` 用户还大。例如：

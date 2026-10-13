
for sites with large user communities.

```
# mkpasswd /etc/passwd    Create new passwd dbm database.
```

## 组

组提供了一种粗略的机制，用于在用户之间共享信息。与 /etc/passwd 文件类似，/etc/group 文件是一个表格，用于标识系统上的所有组名、关联的 GID 以及组成组成员资格的账户名称的逗号分隔列表（示例 2.11）。UNIX 假定有限的组集来实现默认访问权限。系统管理员可以将用户添加到这些默认组中或创建新组以促进额外的协作。如果用户基数较小，这可以相对容易地完成。对于大量用户，管理 GID 集可能是一项繁重的工作。

## 示例 2.11 /etc/group

```
system::!0:root,ops
daemon::!1:
bin::!2:root,bin
sys::!3:root,bin,sys
adm::!4:bin,adm,kenm,root
uucp::!5:uucp
mail::!6:
security::!7:root
cron::!8:root
staff::!10:root,ren,stimpy,daffy,huey,dwewy
user::!30:luge,acadmus,gwyneira,bungi
```

## 网络信息服务

网络信息服务（NIS）是一种管理工具，可用于在机器之间分发通用的系统配置信息。NIS 和 NIS+ 过去通常被称为“黄页（YP）”。对于负责维护实验室或分布式网络中大量机器的系统管理员来说，NIS 是一大福音。参与机器的集合称为 NIS 域。分发集中每个文件都被转换为 ndm 数据库格式并作为 NIS 映射文件存储在服务器上。NIS 映射的集合构成了 NIS 数据库，该数据库会定期分发到 NIS 域中的机器。

正如你可能猜到的那样，使用 NIS  commonly 分发的两个文件是 /etc/passwd 和 /etc/group 文件。NIS 提供了一种便捷的方法，可在多台机器之间同步账户信息。在仅需在机器之间保持部分账户和组共用的情况下，NIS 允许将账户和组划分为本地和分布式类别（表 2.10）。本地信息是每个机器独有的。分布式信息是在主 NIS 服务器上管理的配置信息，并推送到参与机器以实现统一。本地数据会覆盖冲突的分布式数据。

## 表 2.10 NIS 密码和组文件

| /etc/passwd | /etc/group |
|---|---|
| /etc/passwd.yp | /etc/group.yp |
| /etc/passwd.local | /etc/group.local |

## Kerberos

有许多适用于 UNIX 的身份验证系统可供使用，它们增强了基本密码和组架构的功能和安全性。其中一个系统是 *Kerberos* 身份验证，由 M.I.T. 开发，基于 *Trusted Third-Party* 身份验证模型。原始设计在 1988 年 USENIX 冬季会议上发表的一系列论文中进行了描述。Kerberos 是关于 UNIX 和 NT 共存的重要技术，因为它是 Windows 2000 中的网络身份验证系统。

Kerberos 假定网络中的所有内容都是不可信的，除了 Kerberos 身份验证服务器本身。Kerberos 身份验证服务器称为 *Key Distribution Center (KDC)*。KDC 在客户端和所需服务之间充当中介。客户端必须向 KDC 进行身份验证以获取票据，该票据授予访问分布式服务的权限（图 2.5）。该票据称为 *Ticket Granting Ticket (TGT)*。只需向 KDC 验证一次身份，而非每次访问的服务都需验证一次。各种 Kerberos 票据也仅在特定时间内有效。Kerberos 票据机制消除了通过网络以明文传输密码的需求。客户端和服务器密码由 KDC 知晓并存储。

![](img/7684008b1d7775727df27d44aed5b3f0_32_0.png)

1. 请求用户和服务的身份验证。
2. 返回 TS 会话密钥和标识符。
3. 使用密封的身份验证器请求票据。
4. 返回所请求服务的票据。
5. 使用身份验证器票据连接到服务。

图 2.5：Kerberos 票据交换

每当未经身份验证的客户端请求访问服务时，就会向 KDC 发送一条消息，其中包含客户端名称和 Kerberos 票据授予服务名称。KDC 查找名称并获取客户端和票据服务器的加密密钥。加密密钥仅为拥有方代理和 KDC 所知。然后 KDC 构造一条消息，其中包含客户端和票据服务器名称、地址以及随机会话密钥，并使用客户端的加密密钥对其进行加密。该消息称为票据并发送给客户端。客户端使用其加密密钥解密票据并在票据有效期内存储票据。会话密钥用于加密与 Kerberos 票据服务的票据通信以获取对其他服务和资源的访问权限。

当请求访问服务时，票据服务提供一个新的会话密钥以及使用 KDC 数据库中的服务加密密钥加密的票据。客户端使用新的会话密钥创建身份验证器票据以标识客户端，并将其与加密的服务票据一起发送给新服务。服务使用其加密密钥解密票据。服务票据包含会话密钥，然后用于解密身份验证器票据。现在客户端和服务彼此知晓，真正的任务可以开始了。

这看起来似乎是大量手势挥动以防止明文密码和身份验证信息在网络上传播。另一方面，在线路上窃听极其容易。所有这些协商都在幕后进行，因此对终端用户不可见。请记住，Kerberos 不会限制已经窃取了另一用户登录 ID 和密码的人的访问。

## 摘要

- UNIX 具有三层架构：内核、shell 和命令层。
- 执行任务和程序称为 *processes*，并由 *PID* 号码标识。
- 服务器进程称为 *daemons*。
- *Init*，PID 1，负责生成系统进程，这些进程在 `/etc/inittab` 文件中标识。
- TCP/IP 是一种具有四层的网络协议：*physical*、*internetwork*、*transport* 和 *application*。
- 网络上的每台计算机都由一个四字节的 IP 号码标识。
- 网络计算机组使用 *subnets* 进行划分，以隔离和管理流量并执行安全策略。
- 一种称为 *Domain Name Service (DNS)* 的分层动态网络名称服务将域名解析为 IP 号码。
- UNIX DNS 服务器称为 *named*。
- DNS 服务器地址在 `/etc/resolv.conf` 中标识。
- *inetd* 服务器在由 `/etc/inetd.conf` 定义的客户端请求时启动网络服务器。
- 众所周知的服务名称到端口映射记录在 `/etc/services` 中。
- UNIX 文件系统包含在称为 *partitions* 的磁盘块集合中。
- 分区内的文件系统结构表示为 *superblock*、*inode table* 和 *data blocks*。
- 文件系统包含 *files* 和 *directories* 的分层集合，每个都记录在 inode 中。
- 所有 UNIX 对象都被抽象为文件。
- 文件和目录访问控制记录在 inode 中，指示 *owner*、*group* 和 *world* 的 *read*、*write* 和 *execute* 权限。
- NFS 是一种无状态的网络文件系统，用于共享文件和目录。
- 本地和远程打印与排队由 `lpd` 守护进程管理。
- 打印机和队列配置信息记录在 `/etc/printcaps` 中。
- UNIX 用户由账户名、UID 和 GID 标识。
- 用户识别信息存储在 `/etc/passwd` 中。
- 通过使用 shadow 密码文件启用对加密密码数据库的受限访问。
- 通过使用 `dbm` 密码数据库、`/etc/passwd.dir` 和 `/etc/passwd.pag` 可以提高密码访问性能。
- 组授权在 `/etc/groups` 中定义。
- NIS 可用于向共享通用用户基的多台机器分发密码和组信息。
- Kerberos 是一种基于 *Trusted Third-Party* 模型的网络身份验证系统。
- Windows 2000 支持 Kerberos 身份验证。

## 第 3 章：Windows 概述

## 概述

在上一章中，我们研究了 UNIX 系统和网络框架的各个部分，以帮助开发使用 Samba 与 Windows 客户端共享 UNIX 资源的模型。在第 3 章中，我们继续这一讨论线索，通过检查相应的 Windows 系统和网络子系统。在 particular，我们将仔细查看 Windows 网络协议、域和工作组、文件系统和访问控制。Samba 是 Windows 文件和打印共享服务的实现，也提供了基本 NT 主域控制器（PDC）功能。因此，对 Windows 网络协议和域服务的透彻理解对于在企业中成功部署 Samba 至关重要。

## Windows NT 架构

Windows NT 操作系统与 UNIX 相似，因为进程通过执行系统服务层与 CPU、内存和硬件交互。NT 采用抢占式多任务来管理进程线程的执行方式，与 UNIX 调度程序的工作方式大致相同。这允许 NT 暂停某些任务以提供资源给更高优先级的任务。NT 也是多线程的，使其能够在对称多处理平台上运行。这看起来与 UNIX 非常相似。NT 开发团队花费了大量时间审查和借鉴 UNIX 和其他计算架构的想法，最终以卡内基梅隆大学的 Mach 微内核作为操作系统的基础。

Windows NT 被实现为分层子系统架构并支持


```bash
$ sudo down eth2s0 && ifup eth2s0
killed old client process
Internet Systems Consortium DHCP Client 4.3.3
Copyright 2004-2015 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/eth2s0/e4:11:5b:12:c2:77
Sending on LPF/eth2s0/e4:11:5b:12:c2:77
Sending on Socket/fallback
DHCPCOVER on eth2s0 to 192.168.0.1 port 67 (xit=0xd70caeea)
RTNELINK: No such process
RTNELINK: Assign requested address
Internet Systems Consortium DHCP Client 4.3.3
Copyright 2004-2015 Internet Systems Consortium.
All rights reserved.
For info, please visit https://www.isc.org/software/dhcp/
Listening on LPF/eth2s0/e4:11:5b:12:c2:77
Sending on LPF/eth2s0/e4:11:5b:12:c2:77
Sending on Socket/fallback
DHCPCOVER on eth2s0 to 255.255.255.255 port 67 interval 3
(xit=0xc0639266)
DHCPCOVER on eth2s0 to 255.255.255.255 port 67 interval 8
DHCPREQUEST of 192.168.0.6 on eth2s0 to 255.255.255.255 port 67
(xit=0xc0639266)

DHCPOFFER from 192.168.0.6 from 192.168.0.1

DHCPACK from 192.168.0.6 from 192.168.0.1

bound to 192.168.0.6 -- renewal in 288071 seconds.

$
```

# Linux 系统管理基础

## 练习 17.38

在此会话期间，你如何删除对 `enp2s0` 的地址 `192.168.0.100` 的分配？

## 练习 17.39

你如何确保删除操作在系统启动之间持续有效？

结论：我们在 Linux 系统的同一个网卡上分配了多个局域网 IP 地址。

# 17.9 系统安全

在提到计算机时，“安全”一词有两个含义。我们将只考虑其中一个。

第一个含义是指可靠性。换句话说，磁盘上的文件和数据可以信随着时间的推移而存在。这不仅是持久化介质的目标，也是备份操作系统本身、用户文件和数据的目标。例如，如果操作系统崩溃且无法恢复，而用户文件和数据已归档，则可以完全恢复。

第二个含义是指免受恶意入侵（如机器人黑客）或对象（如作为进程执行基础的进程）的侵害，这些对象没有访问系统特定部分或其任何组件、文件或数据的权限。对于单用户系统和多用户环境，从这种意义上实施安全性的理由应该是显而易见的。特别是考虑到当代的隐私问题，互联网上普遍的黑客攻击和系统渗透力量无处不在。

从根本上说，根据这种含义，安全在几个领域实施。我们将在后续章节描述其中一些：

- 1. 进程层面：涉及保护进程免受未经的访问。示例包括：
    - 设置文件和目录权限。
    - 使用访问控制列表 (ACL)。
    - 使用命名空间隔离。
- 2. 物理层面：涉及保护硬件本身。示例包括：
    - 基于密码的身份验证。
    - 在未使用时锁定机器。
- 3. 网络层面：涉及保护系统免受外部攻击。示例包括：
    - 入侵检测系统 (IDS)。
    - 入侵防御系统 (IPS)。
    - 使用防火墙。
- 4. 持久化层面：涉及保护存储在持久化介质上的数据。示例包括：
    - 数据加密。
    - 使用全盘加密、分区加密或文件级加密。

## 17.9.2 访问控制凭据：DAC、MAC 和 RBAC

如果你想理解不同的访问控制类型，本节使用的术语非常重要。当我们讨论通过安全检查进行访问控制时，以下是重要的术语：

**对象（Objects）：** 执行中的 Linux 内核的一个基本组件是它维护的程序和进程。对象是程序进程所针对或正在处理的实体。例如，进程本身可以是对象，也可以是由于执行程序实例而产生的进程。

**文件/索引节点（Files/inodes）：** 是对象的另一种形式，特别是对象的可执行文件，以及存储其信息的数据结构。这不应与文件系统对象混淆，我们通常将文件系统对象称为普通文件（`file`）或目录（`directory`）。

**对象所有权（Object Ownership）：** 指明所属的用户和组。

**对象上标文/上下文（Object Context）：** 当对某个对象进行操作时的安全检查。

**主体（Subjects）：** 被另一个对象所操作的对象。进程是活跃的主体，例如那些由某个源进程通过 `exec()` 或 `fork()` 系统调用创建的进程。

**主体上下文/上下文（Subject Context）：** 当一个活跃的主体执行其操作时的安全检查。

**动作（Action）：** 主体对对象执行的操作。这包括读取、写入、创建和删除文件；以及派生（`forking`）或发送信号（`signaling`）。

**权限（Permissions）：** 当主体作用于对象时进行的检查。结合主体上下文、对象上下文和动作，搜索一个或多个权限，以查看在给定这些上下文的情况下，主体是否被授予或被拒绝以预期方式对对象执行操作。简单来说，就是匹配主体和对象的权限，并允许主体执行或不执行。

权限有三种基本的“类”：

1. **DAC（自主访问控制）：** 有时对象包含一组规则作为其描述的一部分。这被称为“访问控制列表”（Access Control List，简称 `ACL`）。一个 Linux 文件可能提供多个 ACL。例如，传统的 Linux 文件包含一个掩码（`mask`），它是一个简化的 ACL，具有三个固定的主体类别（“用户 `user`”、“组 `group`”和“其他 `other`”），每种类别都可以被授予权限（“读”、“写”和“执行”），无论这些权限映射到相关的对象是什么。然而，Linux 文件不允许任意指定主体，并且受到限制。
   Linux 文件可能还支持 POSIX.1 ACL，或者在 ZFS 的情况下支持 NFS4 ACL。这是一份向任意主体授予各种权限的规则列表。

2. **MAC（强制访问控制）：** 系统整体可能有一组或多组权限，无论其安全性如何，这些权限适用于所有主体和对象。Extended Linux 就是这样一个例子。

3. **RBAC（基于角色的访问控制）：** RBAC 模型不是使用用户来识别其在系统中拥有的访问权限和组，而是根据用户所承担的角色或多个角色来授予访问权限。RBAC 的经典示例是使用 `sudo` 命令来授予未使用的 root 权限。另一个例子是在 ZFS 中，当你执行 `zfs` 命令时，你的操作会进行检查，以确认如果用户是 root，主体是否具有该角色权限。

这些控制策略类定义了在什么情况下（DAC、MAC 或 RBAC）、由什么主体允许在什么对象上执行什么动作。

例如，在传统的 UNIX/Linux 意义上的权限是指读、写、执行权限。主体、对象可以被认为是一个正在执行的进程。最重要的是，对象是一个 Linux 进程（在第 10 章详细介绍），因为在文件和数据上进行的一切操作都是通过系统上的活跃进程完成的。

## 练习 17.41

什么机制控制着 Linux 中进程的执行？

## 练习 17.42

给出 DAC、MAC 和 RBAC 的其他例子。

在命令行上，普通用户或系统管理员可以通过 `chmod` 命令控制作用于可执行镜像文件的进程凭据分配，从而实现资源使用限制和权限。在 Linux 上，可以通过 `su` 或 `sudo` 命令赋予无特权用户所需的特权角色。然后，以 `root` 身份，她可以执行特权的 `chmod`、`chown` 和 `chgrp` 来授予或修改文件和目录的访问权限，并使用 DAC、MAC 或 RBAC 方法。

## 凭证类型（Types of Credentials）

我们关注的是 Linux 内核支持的三种基本凭证类型。文中主要引用了：

传统的 UNIX 凭证——请参阅第 5 章获取更完整的阐述。

1. 真实 UID (`Real UID`)

2. 真实 GID (`Real GID`)

`UID` 和 `GID` 被分配给大多数 Linux 对象。这些在很大程度上定义了该对象的对象上下文，进程也包含在此分配中。

3. 有效 UID (`EUID`)、保存 UID (`SAID`) 和文件系统 UID (`FSID`)

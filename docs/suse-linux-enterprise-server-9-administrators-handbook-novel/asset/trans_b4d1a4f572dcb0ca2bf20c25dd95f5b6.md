
配置在 sudoers 文件中，eric 和 hart 必须知道 root 密码才能获得必要的权限。

与此相反，用户 belandja 可以直接访问 shutdown 命令，而无需知道 root 密码。这种功能在用户（如 Oracle DBA）在安装期间需要重启机器时通常很方便。因为此类用户在日常任务中不需要 root 密码，所以他们可以在无需额外支持人员的情况下自由重启服务器。

## 清单 5.10
示例 /etc/sudoers 文件

```text
# sudoers file.
#
# This file MUST be edited with the 'visudo' command as root.
#
# Defaults specification
Defaults targetpw # ask for the password of the target user
#%users ALL=(ALL) ALL # WARNING! Only use this together
#with "Defaults targetpw"
#
# User privilege specification
# You should not use sudo as root in an SELinux environment
# If you use SELinux, remove the following line
root ALL=(ALL) ALL

User_Alias    POWERUSER = eric, hart

Cmnd_Alias    MNT = /bin/mount, /bin/umount
Cmnd_Alias    KILL = /bin/kill
Cmnd_Alias    USERMGMT = /usr/sbin/useradd, /usr/sbin/groupadd
Cmnd_Alias    PRINTING = /usr/sbin/lpc, /usr/sbin/lprm
Cmnd_Alias    SHUTDOWN = /bin/shutdown
Cmnd_Alias    REBOOT = /sbin/reboot

POWERUSER     ALL = (root) MNT, USERMGMT, KILL, PRINTING,
              SHUTDOWN, REBOOT
belandja ALL= NOPASSWD: /sbin/shutdown
eric     ALL= (root) /usr/sbin/setquota
```

在此配置生效的情况下，POWERUSER 组的成员可以执行他们需要执行的所有任务，但不会超出这些任务。对于用户 hart 来说，即使他可以 sudo 到 root，他也可以管理组但不能影响系统服务。这可以在以下在线会话摘录中看到：

```text
hart@Athena:~>
hart@Athena:~> sudo /usr/sbin/groupadd websales
Password:
hart@Athena:~> grep -we websales /etc/group
websales:x:1000:
hart@Athena:~>
hart@Athena:~> sudo /etc/init.d/xinetd stop
Sorry, user hart is not allowed to execute
"/etc/init.d/xinetd stop" as root on Athena.
hart@Athena:~>
```

在所有规则理清并向需要的人授予访问权限后，su 实用程序就可以退役了。最简单的方法是更改 /bin/su 的权限，不允许 Other 对程序具有执行访问权限。用 sudo 替换 su 命令——结合使用 PAM 将敏感账户限制在已知工作站上——大大降低了服务器的风险敞口。将 root 锁定到控制台可进一步保护账户免受外部访问。

## 摘要

在本章中，您看到可以做许多事情来使服务器环境更安全。与仅运行必要服务的概念相一致，即使在新安装的服务器上，也必须审计和维护账户。

在用户环境方面，本章研究了可插拔认证模块（PAM），并讨论了如何使用它来控制系统访问。PAM 是一种强大的工具，可用于控制系统访问、资源消耗以及标准的认证方法。关于可消耗资源，本章涉及了磁盘配额系统，并研究了如何使用它来防止磁盘空间耗尽。

为了进一步保护环境，您看到可以减少具有提升权限访问权限的用户数量。同时，您看到对于确实需要强大命令的个人，您可以授予他们根据其需求量身定制的命令集。

## 文件系统安全

Linux 系统（这对 Unix 也同样适用）的一个简单描述是“在 Linux 系统中，一切皆文件；如果某物不是文件，那就是一个进程”。有些实体不仅仅是文件（例如命名管道和套接字）；Linux 操作系统和 Linux 命令将它们视为文件。因此，为了简化讨论，可以公平地说一切皆文件。Linux 系统与 Unix 一样，不区分文件和目录，因为目录只是一个包含其他文件名称的文件。程序、服务、文本、图像等等都是文件。输入和输出设备，以及通常所有设备，根据系统都被视为文件。

Linux 系统支持多用户，为了让用户共享或保护其文件，实现了一个权限系统。这种保护机制有一些奇怪的转折。例如，要重命名或删除一个文件，您需要该文件所在目录的写权限。对权限工作原理的透彻理解可以让您使系统更安全、轻松地与其他用户共享数据并保护文件免受意外更改。本章回顾了 Linux 文件系统权限的基础知识——并揭示了一些黑暗角落——以及一些高级主题，例如访问控制列表（除了权限设置之外）和文件系统加密。

## 文件和目录权限回顾

在 Linux/Unix 世界中，对文件或目录的访问权限取决于您是否是文件或目录的所有者、分配的特定组的成员，或以上都不是。（另称为“other”或“world”）。换句话说，每个文件和目录都有三种可能的受托人分配（使用“NewWare”术语）。

### 注意

目录只是一个包含文件和其他目录的特殊文件；因此，在下面的讨论中，除非另有说明，否则术语文件用于指代文件和目录。

命令 `ls -l` 显示了文件类型和文件权限设置等信息。图 6.1 显示了此类列表的示例并标识了权限适用性。如您所见，每个权限设置由三个字段（一个三元组）组成，并为三个受托人分别显示。每个字段可能的权限值列在表 6.1 中；权限始终按相同顺序排列：用户、组和其他（又名 world）的读、写和执行。

### 图 6.1
文件类型和权限。

![](img/ae8469257d2662b469f2360b3bbbe322_173_0.png)

### 表 6.1
符号权限值

| 权限 | 符号 | 描述 |
|---|---|---|
| 读取 | r | 在文件中，表示文件可读。在目录中，表示可以访问目录的内容。它位于三元组的第一位。 |
| 写入 | w | 在文件中，表示文件可被修改。在目录中，表示目录中的文件可以被创建、重命名或删除。它位于三元组的第二位。 |

### 表 6.3
符号权限值（续）

| 权限 | 符号 | 描述 |
|---|---|---|
| 执行 | x | 在文件中，表示文件可执行。在目录中，表示可以遍历目录并搜索文件（如直接使用 `ls`）。它位于三元组的第三位。 |
| 粘滞 | t | 在目录上，粘滞位意味着除所有者或 root 之外的用户不能删除或重命名（但可以修改）此目录中的文件，即使他们对文件和目录具有写权限。此权限仅适用于“others”，位于三元组的第三位。在文件上，符号显示为 T 且无效果。小写 t 表示粘滞位和执行位均已设置；大写 T 表示粘滞位已设置，但执行位未设置。 |
| 设置 UID (SUID) 或设置 GID (SGID) | s | 仅适用于所有者或组权限三元组。当在文件的所有者三元组中发现时，表示执行时，该文件将以文件所有者的 UID 执行，而不是执行程序的用户 UID；如果设置在目录的所有者三元组上，则无效。如果设置在文件的组三元组中，执行的文件将假定为组所有者的 GID，而不是执行程序的用户的首要 GID。当设置在目录的组三元组上时，所有新文件和子目录将继承与目录本身相同的 GID——目录也将继承 SGID 位——而不是创建它们的用户的 GID；现有文件和子目录保持不变。小写 s 表示 SUID 或 SGID 位已打开，且对应的用户或组执行位也已打开；大写 S 表示 SUID 位已设置，但对应的执行位未设置。此设置显示在三元组的第三位。 |
| 无权限 | - | 如果此符号出现在权限三元组的任何位置，表示该位置未分配权限。 |

**注意**

粘滞位和 SUID/SGID 权限位将在本章后面“特殊文件权限”部分进一步讨论。

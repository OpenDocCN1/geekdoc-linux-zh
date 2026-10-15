
```bash
$ whoami
Christine
$ ls -1d /etc
drwxr-xr-x. 143 root root 12288 Jan  4 09:22 /etc
$
$ ls /etc
abrt                 gshadow-             profile
adjtime              gss                  profile.d
[...]
$
```

下一个示例（列表 22.13）表明，父目录（`/home`）允许用户使用 `cd` 将当前工作目录更改为该目录。然而，子目录（`Samantha`）通过未授予执行（`x`）特权来阻止了这种操作。

**列表 22.13：** 理解目录权限中执行特权的影响

```bash
$ whoami
Christine
$ ls -ld /home/
drwxr-x-x. 5 root root 52 Nov 8 14:31 /home/
$ cd /home
$ pwd
/home
$ ls -ld /home/Samantha
drwx------. 5 Samantha Samantha 128 Nov 8 14:38 /home/Samantha
$ cd /home/Samantha
-bash: cd: /home/Samantha: Permission denied
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_698_0.png)

> 如果子目录授予了执行权限，但其父目录之一未授予执行权限，用户将无法使用 `cd` 到达该子目录。该路径中的所有目录都必须为该用户设置执行权限。

如果您有一个在用户之间共享的目录，且用户能够删除彼此的文件，但并非希望如此，请对该目录使用粘滞位（`sticky bit`）。此权限（在第 15 章中涵盖）将解决此问题。

## 处理高级权限

除了标准的 Linux 文件和目录权限外，您可能会遇到使用了 Linux 更高级权限特性的系统。

访问控制列表（`ACL`）允许您除了标准的属主、组和其他设置外，还为多个用户或组指定权限。如果您的 Linux 系统使用 `ACL`，请始终使用 `getfacl` 实用工具检查应用于文件或目录的额外 `ACL` 权限：

```bash
$ getfacl test.txt
# file: test.txt
# owner: rich
# group: rich
user::rw-
user:sales:r-x
mask::r-x
other::r--
```

在此示例中，属主使用 `ACL` 将 `sales` 组的读取权限分配给了该文件。要更改 `ACL` 设置，请使用 `setfacl` 实用工具。

除了 `ACL` 权限外，Linux 系统还可能使用基于上下文的权限，采用 `SELinux`（最常见于基于 Red Hat 的 Linux 发行版）或 `AppArmor`（最常见于基于 Debian 的 Linux 发行版）。

要确定 `SELinux` 在您的 Linux 系统上是否处于活动状态，请使用 `sestatus` 命令：

```bash
$ sudo sestatus
SELinux status:               enabled
SELinuxfs mount:             /sys/fs/selinux
SELinux root directory:      /etc/selinux
Loaded policy name:          targeted
Current mode:                enforcing
Mode from config file:       enforcing
Policy MLS status:           enabled
Policy deny_unknown status:  allowed
Memory protection checking  actual (secure)
Max kernel policy version:   331
$
```

如果 `SELinux` 已启用，请使用 `ls` 命令的 `-Z` 命令行选项来查看文件和目录的附加上下文权限：

```bash
$ ls -Z test1.txt
unconfined_u:object_r:user_home_t:s0 test1.txt
$
```

您可以使用 `chcon` 命令更改文件的安全上下文：

```bash
chcon -u newuser -r newrole -t newtype filename
```

`SELinux` 使用策略来控制对对象的访问。`getsebool` 命令允许您列出策略并确定它们是处于活动还是禁用状态，并使用 `setsebool` 命令来激活或停用它们。

要确定 `AppArmor` 在您的系统上是否处于活动状态，请使用 `aa-status` 实用工具：

```bash
$ sudo aa-status
apparmor module is loaded.
...
$
```

## 文件创建

用户尝试创建文件时权限被拒绝。首先检查目录权限。如果目录权限正常，请考虑以下事项：

- **该分区是否强制执行配额？** 用户可能已达到配额限制。检查分区的 `/etc/fstab` 记录中是否存在 `usrquota` 或 `grpquota`，以查看此文件系统上是否启用了配额（在第 10 章中介绍），或者使用 `repquota` 实用工具。如果启用了配额，使用 `quota` 命令检查用户（或组）的配额使用情况。如果用户超出了配额限制且宽限期已过，请使用 `quotaoff` 关闭配额，延长用户的配额，或让用户删除不必要的文件。

- **磁盘是否已用完空间？** `df` 命令（在第 20 章中介绍）可以帮助您快速确定用户尝试创建文件的分区是否已用完空间。如果空间不足，请采取适当措施（同样在第 20 章中介绍）。

- **分区是否已用完 inode？** *inode 耗尽* 是一种不常见的情况，但确实会发生。`inode` 号（在第 3 章“管理文件、目录和文本”中介绍）是与文件关联的索引号。如果文件系统的 `inode` 耗尽，则无法在其上创建任何额外文件。通过执行 `df -i` 命令来检查是否存在此问题，该命令显示每个文件系统的 `inode` 使用情况。

如果 `inode` 已耗尽，您在文件系统创建后无法扩展它们。相反，请查找包含大量小且不必要的文件的目录（例如临时目录），并删除可以删除的内容。良好的做法是将创建许多小文件的应用程序放在自己的大容量分区上，并将其格式化以提供更高数量的 `inode` 号。在创建文件系统时，通过使用 `mke2fs -i` 命令等实用选项来增加 `inode` 数量，使其高于默认值。

- **用户的 umask 设置是什么？** `umask` 设置（在第 15 章中介绍）会从默认文件和目录权限设置中减去权限。因此，当用户创建文件和/或目录时，其上的权限设置会受此影响。让用户在命令行输入 `umask`（或检查用户的环境文件）以确定其设置。如果设置过高（例如，移除了创建子目录所需的写权限），则找到了问题的原因。

与访问问题类似，在用户无法创建或删除文件的情况下，请检查您的 Linux 内核安全模块（`SELinux` 或 `AppArmor`）。使用适当的工具浏览相应的策略违规日志文件（`/var/log/messages` 或 `/var/log/audit/audit.log`）。

在找到关于相关文件或目录的策略违规后，确定是文件/目录标签错误、策略不正确，还是可能使用了错误的 `security context`。采取适当措施解决问题。

## 探索环境和 Shell 问题

在处理用户问题时，潜在问题是用户账户的默认 shell。使用 `getent` 命令进行检查，如图 22.14 所示在 Ubuntu 发行版中的显示。

**图 22.14：** 使用 `getent` 命令确定账户的默认 shell

```bash
$ getent passwd BSisko
BSisko:x:1007:1007::/home/BSisko:/bin/sh
$
$ readlink -f /bin/sh
/bin/dash
$ 
```

请注意，默认 shell 没有使用 `/bin/bash`，而是使用了 `/bin/sh` shell。在此系统上，`/bin/sh` 文件链接到 `/bin/dash` shell。如果这不是您想要的，您可以通过 `usermod` 命令更改用户的默认 shell（参见第 10 章）。

设置不正确或错误的环境变量会导致各种用户困难。查看用户的环境文件（在第 10 章中介绍），如 `~/.profile` 文件。与此同时，使用 `set`、`env` 或 `printenv` 命令检查系统的全局环境变量设置。

确保环境变量被导出，以便它们在子 shell 中可用（当执行 shell 脚本时可能会发生子 shell）。此问题的示例如图 22.15 所示。

**图 22.15：** 演示当变量未被导出时会发生什么

```bash
$ EDITOR='nano'
$ echo $EDITOR
nano
$
$ bash
$
$ echo $EDITOR
$
$ exit
exit
$
```

用户设置环境变量 `EDITOR`，使其默认文本编辑器变为 `nano`。但是，当通过 `bash` 命令创建新的子 shell 时，设置会丢失。为了保持设置的持久性，需要将其导出并存储在用户的环境文件中。导出变量的示例如图 22.16 所示。

**图 22.16：** 演示 `export` 命令

```bash
$ export EDITOR='nano'
$
$ echo $EDITOR
nano
$
$ bash
$
$ echo $EDITOR
nano
$
```

同样重要的是，确保环境变量位于正确的文件中，无论是全局文件还是用户文件。此外，您必须了解用户进行的登录类型，以便将这些变量设置在正确的文件中（参见第 10 章）。

## 总结

用户问题故障排除很棘手。访问、身份验证、文件管理以及用户的 shell 和环境涉及许多组件。理解常见问题将有助于解决问题。

## 考试要点

- **总结用户访问问题/解决方案。** 对于受阻的本地访问，研究损坏的终端文件、配置错误的 GUI 组件以及过期的密码/账户。远程访问问题通常是由配置错误的 `OpenSSH` 组件或远程桌面应用程序引起的。其他问题可能涉及分层身份验证软件，如 `PAM` 或系统的内核安全模块，如 `SELinux` 或 `AppArmor`。

- **描述各种文件问题/解决方案。** 文件访问和管理需要理解基本的文件和目录权限以及所有权和组成员资格。需要审查的其他系统项目包括文件系统配额、磁盘空间、`inode` 使用情况和 `umask` 设置。还要检查内核安全模块日志文件中的策略违规。如果用户无法删除文件，请查找文件上设置的不可变位。

- **解释用户环境和 shell 问题。** 配置不当或未导出的环境变量会导致用户问题。检查各种环境文件，包括全局文件和用户文件，查找问题。用户账户的默认 shell 设置也可能导致困难。

## 复习题

1. 承包商 Lamar 声称他无法本地登录他的账户。昨天他还能登录。其他人似乎没有遇到访问系统的问题。你应该首先检查什么？

    A. 使用 `systemctl` 命令检查 GUI 服务是否正在运行。

    B. 查看 `OpenSSH` 服务器配置文件。

    C. 使用 `chage` 命令确定他的账户是否已过期。

    D. 使用 `faillock` 实用工具查看账户是否被锁定。

    E. 检查 `SELinux` 日志文件中的策略违规。

2. Irene 通常通过 `tty4` 终端本地登录系统，但今天无法登录。她在 `tty3` 终端尝试身份验证并成功登录。你应该首先检查什么？

    A. 使用 `systemctl` 命令确定 `getty` 服务是否正在运行。

    B. 查看 `/etc/security/access.conf` 文件中的访问规则。

    C. 使用 `passwd -S` 命令查看账户是否被锁定。

    D. 使用 `last` 命令查看她最后登录的时间。

    E. 使用 `ls -l` 命令检查 `tty4` 设备文件是否损坏。

3. Vincent 尝试使用 `OpenSSH` 远程登录系统但未成功。他问你可以做什么来帮助排除此问题。你首先应该建议什么？

    A. 检查 `/etc/ssh/sshd_config` 配置文件。

    B. 在 Vincent 的 `ssh` 命令中添加 `-vvv` 选项。

    C. 在 Vincent 的 `ssh` 命令中添加 `-X` 选项。

    D. 确认 Vincent 的公钥存储在 `~/.ssh/authorized_keys` 文件中。

    E. 检查 `~/.ssh/config` 配置文件。

4. Anton 难以确定为什么特定用户无法登录 Rocky Linux 系统，其中 `SELinux` 已禁用且未使用 `auditd`。以下哪些是最佳日志文件？（选择两项。）

    A. `/var/log/audit/audit.log`

    B. `/var/log/messages`

    C. `/var/log/auth`

    D. `/var/log/secure`

    E. `/var/log/lastlog`

5. Tarissa 需要运行一个 shell 脚本，该脚本的权限为 `rwxr--r--`，所有者为 `root`，所属组为 `wheel`。Tarissa 的用户账号是 `T2T1080`，她是 `admin` 组的成员。为了让她能够运行此脚本，可以执行以下哪些操作？（选择所有适用项。）

- **A.** 将 Tarissa 添加到 `wheel` 组中。

- **B.** 为 Tarissa 创建一个名为 `wheel` 的新账号。

- **C.** 在脚本文件的组权限中添加 `w`。

- **D.** 在脚本文件的组权限中添加 `x`。

- **E.** 无需任何操作。Tarissa 现在就可以运行该脚本。

6. Miles 需要将当前工作目录更改为 `/home/miles` 目录。他既不是该目录的所有者，也不属于该目录的组。假设所需的父目录权限已设置，要实现此操作成功发生，需要满足什么条件？

- **A.** 无需任何操作。`/home/miles` 目录是 Miles 的主目录，因此他可以默认访问。

- **B.** 需要添加执行 (`x`) 权限。

- **C.** 需要添加写入 (`w`) 权限。

- **D.** 需要添加读取 (`r`) 权限。

- **E.** 需要添加破折号 (`–`) 权限。

7. Sarah 是一名系统管理员，她尝试创建一个文件，但收到一条错误消息，表明无法创建该文件。以下哪几项可能是问题所在？（选择所有适用项。）

- **A.** 她尝试创建文件的文件系统设置了配额，且她已超出配额和宽限期。

- **B.** 她尝试创建文件的文件系统空间已耗尽。

- **C.** 她尝试创建的文件设置了不可变位（immutable bit），因此无法创建。

- **D.** 该操作触发了 `SELinux` 或 `AppArmor` 策略违规。

- **E.** 文件系统正在经历 `inode` 耗尽，因此无法容纳任何新文件。

8. 一名用户无法删除自己的某个文件，但能够删除其目录中的其他文件。John 是一名系统管理员，正在尝试排查此问题。他首先应该对该文件使用哪个命令？

- **A.** `chown`

- **B.** `chattr`

- **C.** `chmod`

- **D.** `umask`

- **E.** `lsattr`

9. Melissa 希望将她的默认编辑器设置为 `vim` 编辑器，并希望当她进入子 shell 时此设置保持不变。她应该怎么做？

- **A.** 在 `/etc/profile` 文件中放入 `EDITOR='vim'`。

- **B.** 在 `/etc/profile` 文件中放入 `export EDITOR='vim'`。

- **C.** 在她的 `~/.profile` 文件中放入 `EDITOR='vim'`。

- **D.** 在她的 `~/.profile` 文件中放入 `export EDITOR='vim'`。

- **E.** 在她的 `~/.bashrc` 文件中放入 `export EDITOR='vim'`。

10. Mark Watney 是一名系统管理员，他的账号 `MW2015` 被一名新的系统管理员实习生修改了。当 Mark 登录系统并尝试使用花括号对一组命令进行分组时，它不再起作用。其他人没有遇到这个问题。他怀疑他的账号默认 shell 已从 `/bin/bash` 更改为 `/bin/tcsh`。以下哪几项有助于确定他的怀疑是否正确？（选择所有适用项。）

- **A.** `cat /etc/profile`

- **B.** `echo $SHELL`

- **C.** `sudo grep tcsh /etc/passwd`

- **D.** `sudo getent shadow MW2015`

- **E.** `sudo getent passwd MW2015`

# 第 23 章

![](img/c0a399aca0d18f8822d714ad0a173123_708_0.png)

# 处理 Linux 设备

✓ 目标 1.1：总结 Linux 基础知识

![](img/c0a399aca0d18f8822d714ad0a173123_709_0.png)

典型的 Linux 系统连接着许多不同的硬件设备。列表可能包括硬盘、监视器、键盘、打印机、声卡和网络卡。作为 Linux 管理员，你的工作之一就是确保所有这些设备都能正常工作。本章将指导你如何安装和排查连接到你的 Linux 系统的不同类型硬件设备的问题。首先，本章讨论了你在 Linux 系统上可能需要处理的不同类型设备接口，以及它们如何与操作系统通信。随后，本章讨论了可用于监视和排查系统上这些设备工作问题的 Linux 实用工具。最后，本章深入探讨了热插拔设备的话题，随着 `USB` 设备的普及，这一话题变得极其重要。

## 与 Linux 设备通信

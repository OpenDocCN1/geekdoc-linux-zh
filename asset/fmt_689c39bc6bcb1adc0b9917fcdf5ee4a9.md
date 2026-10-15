
对于 SUID、SGID 和粘性位，有一些特殊的选项。如果你选择使用数值位，这些特殊位也被分配了数值值，其中 `SUID=4`，`SGID=2`，设置位=`1`。然而，要定义特殊位你还需要一个数字。例如，以下命令配置 SUID 位（带有 4）、组的读写权限（带有 6）以及其他用户的权限（带有 4）：

```
chmod 464 testfile
```

如果你更倾向于使用 `ugo/rwx` 格式，以下命令激活文件的 SGID 位：

```
chmod g+s testfile
```

以及以下命令为目录开启粘性位：

```
chmod o+t /tmp
```

对于 `chmod` 命令，更改不需要由 root 用户执行。文件的所有者允许更改相关权限。

https://t.me/CCNA_SECURITY

https://t.me/CCNPSECURITY

## chown 命令

`chown` 命令用于修改文件的所有者。例如，查看我们在本章创建的第一个图形的所有权，基于 `ls -l` 命令：

```
-rw-r--r-- 1 michael 85502 Oct 25 14:07 F02-01.tif
```

该文件的所有者是 `michael`；组是 `exam`。以下 `chown` 命令将所有者改为 `elizabeth`，但必须以 root 身份执行：

```
# chown elizabeth F02-01.tif
```

你可以使用 `chown` 执行更多操作：例如，以下命令将文件的用户和组都改为 `donna` 和 `supervisors`，假设这些用户已存在：

```
# chown donna.supervisors F02-01.tif
```

只有 root 用户可以更改文件的所有者，而所有权可以由 root 以及文件的所有者修改。

## chgrp 命令

你可以使用 `chgrp` 命令更改文件的组所有者。例如，以下命令将名为 `F02-01.tif` 的文件的组更改为 `project` 组（假设它存在）：

```
# chgrp project F02-01.tif
```

## 特殊文件属性

除了 `rw/ugo` 权限外，文件还有属性。这些属性可以帮助你控制对不同文件的操作。虽然 `lsattr` 命令列出文件属性，`chattr` 命令可以帮你更改这些属性。例如，以下命令保护 `/etc/fstab` 不被意外删除，即使是 root 管理员也是：

```
## chattr +i /etc/fstab
```

这时，如果你以 root 管理员身份删除该文件，将得到如下响应：

```
# rm /etc/fstab
rm: remove regular file '/etc/fstab'? y
rm: cannot remove '/etc/fstab': Operation not permitted
```

# 第66 章 第2 章 基础命令行技能

| 表格 2-6 | 文件属性 |
| :--- | :--- |
| 属性 | 描述 |
| 仅追加 (`a`) | 防止删除，但允许向文件追加内容——例如，如果你运行了 `chatter +a tester`，`cat /etc/fstab > tester` 会将 `/etc/fstab` 的内容添加到 `tester` 文件的末。然而，命令 `cat /etc/fstab > tester` 将执行失败 |
| 不备份 (`d`) | 不允许使用 `dump` 命令对已配置的文件进行备份 |
| 不可变 (`i`) | 防止删除或对文件进行任何形式的更改 |

`lsattr` 命令显示 `/etc/fstab` 上有一个激活的“不可变”属性：

```bash
## lsattr /etc/fstab
--i ---------/etc/fstab
```

当然，root 管理员用户可以使用以下命令取消该属性。在进行更改之前，最初对删除文件的拒绝至少应该让管理员停一下。

```bash
# chattr -i /etc/fstab
```

表 2-6 中描述了几个关键属性。其他属性，如 `c`（压缩）、`s`（安全删除）和 `u`（不可删除），对于存储在 `ext4` 和 `XFS` 文件系统中的文件不起。

# 用户和组概念的基本介绍

Linux 与 Unix 不同，它通过用户和组进行配置。每个使用 Linux 的人都有一个用户名，即使只是“guest”。系统中没有名为“nobody”的标准用户。请看图 2-4 所示的 `/etc/passwd` 文件。

所示，所有的用户名都列在 `/etc/passwd` 文件中。邮件、新闻、ftp 和 apache 等许多服务都有它们自己的用户名。在任何情况下，`/etc/passwd` 文件都遵循特定的格式，在第 6 章中会有更详细的描述。为了讨论起，请注意此文件中显示的普通用户是 `alex` 和 `mich`；它们的 UID 和组 ID (`GID`) 分别为 1000 和 1001；它们主目录与其用户名匹配。下一个用户使用的 UID 和 GID 为 1002，依此类推。

这种 UID 和 GID 的匹配是基于红帽组方案的。输出类似于以下：

```bash
drwx------ 4 alex alex 4096 Dec 15 16:12 alex
drwx------ 4 michael michael 4096 Dec 16 14:00 michael
```

https://t.me/CCNA_SECURITY

https://t.me/CCNPSECURITY

# 图 2-4

# /etc/passwd 文件

```
dbus:x:81:81:System message bus:/sbin/nologinpolkit:x:998:996:User for polkitd:/sbin/nologin
avahi:x:700:Avahi mDNS/NSD Stack:/var/run/avahi-daemon:/sbin/nologin
tss:x:59:59:Account for TPM access:/dev/null:/sbin/nologin
colorid:x:997:997:User for colorid:/sbin/nologin
clevis:x:996:992:Clevis Encryption Framework:/var/cache/clevis:/usr/sbin/*
rtkit:x:172:172:MediaKit:/proc/sbin/nologin
sssd:x:999:999:User for systemd:/sbin/nologin
geoclue:x:994:994:User for geoclue:/sbin/nologin
libmanagement:x:484:484:User for libmanagement:/var/run
strbleshoot:x:992:958:SELINUX troubleshooter:/var/lib/troubleshoot:/sbin/nologin
pipewire:x:998:986:PipeWire Daemon:/var/run/pipewire:/sbin/nologin
flatpak:x:1000:1000:User for flatpak:/sbin/nologin
gdm:x:422:422:User for GDM manager:/sbin/nologin
cockpit:x:998:998:User for network service:/sbin/nologin
cockpit-windows:x:998:993:User for cockpit-ws instances:/sbin/nologin
gnome-initial-setup:x:987:982:run for gnome-initial-setup:/sbin/nologin
sys:x:500:500:System for systemd-cored:/sbin/nologin
chrony:x:998:981:User for chrony:/sbin/nologin
dnsmasq:x:998:996:DNS and DHCP server:/var/lib/dnsmasq:/sbin/nologin
tctpdm:x:722:722:/sbin/nologin
system-ood:x:978:978:System users OOM Killer:/usr/sbin/nologin
alex:x:1000:1000:Alessandro Orlando:/home/alex/bash
michael:x:1001:1001:Michael Lang:/home/michael/bash
[root]root-#
```

注意权限。根据 `r`、`w`、`x` 权限。

# 文件权限 67

# /etc/passwd 文件

# 70 第2章 基础命令行技能

图 2-5 less 和 `/var/log/messages`

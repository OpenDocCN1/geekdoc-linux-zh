
```
student@debian:-$ lsblk
NAME  MA:MIN SIZE RO TYPE MOUNTPOINT
db0     2:0    14K 0 disk
sda     8:0     5G 0 disk
-sda1 8:1    4.7G 0 part /
-sda2 8:2      0 part
-sda5 8:5    334M 0 part [SWAP]
```

列表 543 - 所有驱动包含三个分区，并已进行编号。在某些情况下，显示系统上所有磁盘的信息可能会揭示未挂载的分区。取决于系统的配置（或配置错误），那么我们可能

# 使用 Kali Linux 2.0 进行渗透测试

挂载分区并搜索感兴趣的文档、凭据或其他信息，这些信息可能允许我们提升权限或在网络中获得更优立足点。

## 18.1.1.11 枚举设备驱动程序和内核模块

另一种常见的权限提升涉及对设备驱动程序和内核模块的利用。我们将在本模块的后续部分查看实际的执行技术，但让我们先来看看重要的枚举技术。由于这种技术依赖于将漏洞与相应的利用程序进行匹配，我们需要编译一个加载在系统上的驱动程序和内核模块列表。

在 Windows 上，我们可以从 `driverquery` 命令开始搜索。我们将提供 `/v` 参数来获取详细输出，或者使用 `/f csv` 来以 CSV 格式请求输出。

为了过滤输出，我们将在 `powershell` 会话中运行此命令。我们将输出通过到 `Convert-Csv` 句法（类似于 `Select-Object`），这允许我们选择特定的对象属性或对象组，如 `DisplayName`（显示名称）、`Start Mode`（启动模式）和 `Path`（路径）。

```
c:\Users\student>powershell
PS C:\Users\student>driverquery.exe /f csv | Convert-CSV | Select-Object -DisplayName Name, 'Start Mode', Path
```

| Display Name | Start Mode | Path |
| --- | --- | --- |
| 1394 OHCI Host Controller | Manual | C:\Windows\system32\drivers\1394hci.sys |
| Beware Microsoft ACPI Driver | Manual | C:\Windows\system32\drivers\3ware.sys |
| ACPI Devices Driver | Manual | C:\Windows\system32\drivers\acpi.sys |
| Microsoft ACPIEx Driver | Boot | C:\Windows\system32\drivers\aciex.sys |
| ACPI Processor Aggregator Driver | Manual | C:\Windows\system32\drivers\acipagr.sys |
| ACPI Meter Driver | Manual | C:\Windows\system32\drivers\acpim.sys |
| ACPI Wake Alarm Driver | Manual | C:\Windows\system32\drivers\aciptime.sys |
| ADP80XX | Manual | C:\Windows\system32\drivers\adp80xx.sys |

在生成已加载驱动程序列表的同时，我们必须采取下一步来请求每个已加载驱动程序的版本。我们将使用 `Get-WmiObject` 句法获取 `Win32_PnPESignedDriver` WMI 实例，它提供了关于驱动程序的重要信息。通过将输出通过到 `Select-Object`，我们可以枚举特定的属性，包括：

此外，我们可以根据如何将输出通过到 `Where-Object` 来针对性地目标驱动程序。

```
PS C:\Users\student> Get-WmiObject Win32_PnPESignedDriver | Select-Object DeviceName, DriverVersion, Manufacturer | Where-Object {$_.DeviceName -like "*VMware*"}
```

| DeviceName | DriverVersion | Manufacturer |
|---|---|---|
| VMware HCI Host Device | 9.8.6.0 | VMware, Inc. |
| VMware PVSCCI Controller | 1.3.10.10 | VMware, Inc. |
| VMware SVGA 3D | 8.16.1.24 | VMware, Inc. |
| VMware VMCI Bus Device | 9.8.6.0 | VMware, Inc. |
| VMware Pointing Device | 12.5.7.0 | VMware, Inc. |

现在我们已经有了所有加载的 VMware 设备驱动程序列表及其相应的版本号，我们可以搜索这些特定的驱动程序。

在 Linux 上，我们可以使用 `lsmod` 在不带任何参数的情况下搜索已加载的内核模块。

```
student@debian:~# lsmod
Module Size Used by
fuse 90112 3
apptalk 32768 0
ax25 49512 0
ips 28672 0
p8023 16384 1 ipx
p8022 16384 1 ipx
spnap 16384 2 apptalk,ipx
lllc 16384 2 p8022,psnap
evdev 20480 5
mmw_balloon 20480 0
crc32_pcmul 16384 0
...
i2c_piix4 20480 0
libata 189212 2 ata_piix,ata_generic
scsi_mod 57324 4 sd_mod,libata,vmw
floppy 57344 0
```

一旦我们有了已加载模块的列表并识别出我们想要信息的模块（例如示例中的 `libata`），就可以使用 `modinfo` 来查找特定模块。注意，这需要 root 权限运行。

```
student@debian:~# /sbin/modinfo libata
filename: /lib/modules/4.9.0-kernel/drivers/ata/libata.ko
version: 3.0
license: GPL
description: Library for ATA devices
author: Jeff Garrick
srcversion: 7D0
depends: scsi_mod
vermagic: Y
magic: 4.9.0-SMP
unload_delay: seconds (int)
par: ...
```

与 Windows 的情况类似，在获取驱动程序列表及其版本后，我们更有可能找到可能存在的相关“捷径”。

## 18.1.1.12 枚举自动提升权限的二进制文件

在本模块的稍后部分，我们将探索能够自动提升权限的二进制文件。在 Windows 系统上，我们可以根据如何将输出通过到 `Where-Object` 来针对性地目标这些设置。我们可以使用 `reg query` 来检查这些设置：

```
c:\Users\student>reg query HKEY_CURRENT_USER\Software\Policies
HKEY_CURRENT_USER\Policies\Microsoft\Installer
AlwaysElevate REG_DWORD 1
```

```
c:\Users\student>reg query HKEY_LOCAL_MACHINE\Software\Policies
HKEY_LOCAL_MACHINE\Policies\Microsoft\Installer
AlwaysElevate REG_DWORD 1
```

同样，在 Linux 系统上我们可以检查 SUID。通常情况下，运行一个可执行文件时，它会继承文件所有者的权限。如果所有者是 root，任何本地用户都将以 root 权限执行该二进制。

我们可以使用 `find` 命令查找 SUID 标记的文件。在这种情况下，我们从根目录开始搜索（`-type f`），查找带有 SUID 权限的文件（`-perm -u=s`），并丢弃所有错误（`2>/dev/null`）：

```
student@debian~$ find / -perm -u=s -type f 2>/dev/null
usr/lib/encrypt/crypt-device
usr/lib/openssh/ssh-keys
usr/lib/policykit-1/polkit-agent-helper
usr/lib/dbus-1.0/daemon-launch-helper
usr/lib/xorg/Xorg.wrap
usr/bin/user
usr/bin/passwd
usr/bin/sudo
usr/bin/chfn
usr/bin/newgrp
usr/bin/exec
usr/bin/chsh
bin/mount
bin/su
bin/fuser
bin/umount
bin/ntfs-3g
bin/ping
```

在这种情况下，命令发现了几个 SUID 二进制文件。利用 SUID 二进制文件的方法取决于多个因素。例如，如果 `/bin/cp`（复制命令）是 SUID，我们可以复制并覆盖敏感文件如 `/etc/passwd`。

## 18.1.1.13 练习

- 1. 在你的专用 Windows 和 Linux 客户端上执行本节涵盖的手动枚举方法。尝试实验本节使用的工具和命令的各种选项。

## 18.1.2 自动化枚举

显然，每个操作系统都包含可以进一步攻击的丰富信息。无论目标操作系统是什么，手动收集这些信息都是非常耗时。幸运的是，我们可以使用各种脚本来自动化此过程。

在 Windows 上，每个脚本是 `windows-privesc-check`，可以在 windows-privesc-check GitHub 仓库中找到。该仓库已经包含一个由 Installer 生成 Windows 可执行文件，也可以根据需要重新构建。

```
带有 -h 标志运行检查会显示以下菜单：
c:\Tools\privilege_escalation\windows-privesc-check-master>windows-privesc-check.exe -h
```

# windows-privresc-check v2.0 (http://pentestmonkey.net/windows-privresc-check)

用法: windows_privresc_check.exe [--dump [ dump opts]] | --dumptab | --audit] examine opts [host opts] -o report-file-system

选项:

- - --version 显示程序版本号并退出

- -h,--help 显示此消息并退出

- --dump 导出信息供你手动分析

- --dumptab 以制表符分隔的格式导出

- --audit 识别并报告安全漏洞

- --pshell 启动交互式 python shell

examine opts:

至少包含以下一个项之一，以指示要检查的内容（* 表示未实现）

- -a,--all 所有简单检查（非慢速）

- -A,--allfiles 所有文件和目录（慢速）

- -D,--drivers 驱动器

- -e,--reg_keys 杂项安全相关的注册表项

- -E,--events 事件日志

- -INTERESTING_FILE_LIST,--INTERESTING_FILE=INTERESTING_FILE_LIST 更改行为。请查看此处

- -INTERESTING_FILE,--INTERESTING_FILE 更改行为。请查看此处。每行一个

- -G,--groups 组

- -H,--shares 共享文件夹

- -I,--installed_software 安装的软件

- -j,--tasks 计划任务

- -k,--drivers 内内核驱动程序

列表 550 - 由 PyInstaller 生成的可执行文件输出

此工具接受许多选项，但我们将通过一些示例。首先，我们将列出系统中关于组的信息。我们将解释自而其明的 --dump 以查看输出，并使用 -G 来列出组。

```
c:\Tools\privilege_escalation\windows-privresc-check-master>windows-privresc-check2.exe
--dump -G
windows-privresc-check v2.0 (http://pentestmonkey.net/windows-privresc-check)
```

[i] UserEnabled 注册表值为 0。排除终端服务器 (TERMINAL SERVER)

将这些用户视为可信的：

* BUILTIN\Power Users

* BUILTIN\Administrators

* NT SERVICE\InstalledInstaller

* NT AUTHORITY\SYSTEM

[i] 以当前用户身份运行。未提供登录凭据 (-u, -D, -p)。

```
========== Starting Audit at 2019-09-22 12:45:56 ==========
```

# 运行: dump_misc_checks

- - [+] 正在运行: dump_groups

[+] 主机不在域

[+] 检查完成

导出组列表：

BUILTIN\Administrators 成员：CLIENT251\Administrator

BUILTIN\Administrators 成员：CLIENT251\admin

BUILTIN\Administrators 成员：[unknown]\S-5-S-21-271534670-1758985447-1278008508

BUILTIN\Users 成员：[unknown]\S-5-S-21-271534670-1758985447-1278008508

BUILTIN\Guests 成员：CLIENT251\Guest

BUILTIN\IIS_USERS 成员：NT AUTHORITY\IUSRS

BUILTIN\Remote Desktop Users 成员：CLIENT251\student

BUILTIN\Users 成员：NT AUTHORITY\Authenticated Users

BUILTIN\Users 成员：CLIENT251\student

BUILTIN\Users 成员：[unknown]\S-5-S-21-271534670-1758985447-1278008508-513

[+] 检查完成

列表 551 - windows-privesc-check

脚本成功执行，向我们展示了系统中安全组的信息。

由于 Windows 上有 windows-privesc-check，我们也可以在 Linux 等 Unix 派生系统在使用 unix_privesc_check492。我们可以通过不带任何参数运行脚本来查看帮助信息。

```
student@debian:~$ /unix-privesc-check
unix-privesc-check v1.4 ( http://pentestmonkey.net/tools/unix-privesc-check )
用法: unix-privesc-check { standard | detailed }

"standard" 模式：对大量安全设置进行速度优化的检查。

"detailed" 模式：与标准模式相同，还会检查打开的文件句柄和调用的文件（例如从 shell 脚本解析出的、.so 文件）。此模式较慢且容易产生误报，但可能帮助你发现第三方程序中细微的缺陷。
```

此脚本检查了可能允许本地用户提升权限的权限和其他设置。

列表 552 - 运行 unix_privesc_check

如上面的列表所示，脚本支持 "standard"（标准）模式和 "detailed"（详细）模式。根据所提供的信息，标准模式似乎执行了速度优化的过程，应该提供更少的误报。因此，在接下来的示例中，我们将使用标准模式并将整个输出重定向到名为 output.txt 的文件中。

```
student@debian:~$ /unix-privesc-check > output.txt
```

# 使用 Kali Linux 2.0 进行渗透测试

# 攻击性安全 (OFFENSIVE SECURITY)

www.offensive-security.com

脚本对常用文件的权限进行了大量检查。例如，以下异常揭示了非 root 用户可写入的配置文件：

```
正在检查可写文件
正在检查 root 是否可以更改 /etc/passwd
警告：/etc/passwd 是一个关键文件。检查 root 是否可以更改 /etc/passwd
检查 root 是否可以更改 /etc/group
检查 root 是否可以更改 /etc/fstab
检查 root 是否可以更改 /etc/profile
检查 root 是否可以更改 /etc/sudoers
检查 root 是否可以更改 /etc/shadow
```

列表 554 - 可写文件可写检查

此输出揭示了任何人都可以编辑 `/etc/passwd` 文件！这很重要，因为它允许攻击者轻松地提升权限或创建账户。尽管这些工具执行了自动化检查，但请注意每个系统都是不同的，且更改会被这些工具捕获。

## 18.2.1 练习

1. 使用本节介绍的工具和命令检查 Windows 和 Linux，以熟悉技术。

2. 不同的 windows-privesc-check 选项。

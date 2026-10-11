

srcversion:		7D0876C4A3FEBAB6219DD851

depends:		scsi_mod

retpoline:		Y

intree:		Y

vermagic:		4.9.0-6-686 SMP mod_unload modversions 686

parm:		zpodd_poweroff_delay:ZPODD 的断电延迟时间（以秒为单位）(int)

> 列表 547 - 列出 Linux 下关于模块的附加信息

与上文演示的 Windows 情况类似，在获取驱动列表及其版本后，如果存在相关漏洞，我们将处于更有利的位置去发现它们。

### 18.1.1.12 枚举自动提升权限的二进制文件

在本模块的后续部分，我们将探讨各种权限提升方法。然而，在本节中，我们应该涵盖一些特定的枚举操作，这些操作可能揭示某些操作系统特定的权限提升“捷径”。

首先，在 Windows 系统上，我们应该检查 *AlwaysInstallElevated*⁴⁸⁸ 注册表设置的状态。如果此键在 *HKEY_CURRENT_USER* 或 *HKEY_LOCAL_MACHINE* 中处于启用状态（设置为 1），任何用户都可以以提升的权限运行 Windows Installer 包。

我们可以使用 **reg query** 来检查这些设置：

```
c:\Users\student>reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer

HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer
  AlwaysInstallElevated REG_DWORD 0x1

c:\Users\student>reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer

HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
  AlwaysInstallElevated REG_DWORD 0x1
```

> 列表 548 - 在 Windows 上查询 AlwaysInstallElevated 注册表值

如果此设置已启用，我们可以制作一个 MSI 文件并运行它以提升我们的权限。

类似地，在基于 Linux 的系统上，我们可以搜索 *SUID*⁴⁸⁹ 文件。

通常，运行可执行文件时，它会继承运行该文件的用户的权限。但是，如果设置了 SUID 权限，该二进制文件将以文件所有者的权限运行。这意味着，如果一个二进制文件设置了 SUID 位且该文件由 root 所有，那么任何本地用户都能以提升的权限执行该二进制文件。

⁴⁸⁸ (Microsoft, 2018). https://docs.microsoft.com/en-us/windows/win32/msi/alwaysinstallelevated

⁴⁸⁹ (Microsoft, 2018). https://www.linux.com/tutorials/what-suid-and-how-set-suid-linuxunix/

我们可以使用 **find** 命令搜索标记为 SUID 的二进制文件。在这种情况下，我们从根目录（`/`）开始搜索，查找设置了 SUID 位的文件（`-type f`），（`-perm -u=s`），并丢弃所有错误消息（`2>/dev/null`）。

```
student@debian:~$ find / -perm -u=s -type f 2>/dev/null
/usr/lib/eject/dmcrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/polkit-1/polkit-agent-helper-1
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/Xorg/Xorg.wrap
/usr/sbin/userhelper
/usr/bin/passwd
/usr/bin/sudo
/usr/bin/chfn
/usr/bin/newgrp
/usr/bin/pkexec
/usr/bin/gpasswd
/usr/bin/chsh
/bin/mount
/bin/su
/bin/fusermount
/bin/umount
/bin/ntfs-3g
/bin/ping
```

*列表 549 - 在 Linux 上搜索 SUID 文件*

在这种情况下，该命令发现了多个 SUID 二进制文件。SUID 二进制文件的利用方式会因多种因素而异。例如，如果 /bin/cp（复制命令）是 SUID 的，我们可以复制并覆盖敏感文件，如 /etc/passwd。

### 18.1.1.13 练习

- 1. 在你的专用 Windows 和 Linux 客户端上执行本节中涵盖的各种手动枚举方法。尝试对本节中使用的工具和命令的各种选项进行实验。

### 18.1.2 自动化枚举

显然，每个操作系统都包含大量可用于进一步攻击的信息。无论目标操作系统如何，手动收集这些详细信息可能相当耗时。幸运的是，我们可以使用各种脚本来自动化此过程。

在 Windows 上，其中一个这样的脚本是 *windows-privesc-check*，⁴⁰⁰ 它可以在 windows-privesc-check Github 仓库中找到。⁴⁰¹ 该仓库已经包含由 PyInstaller 生成的 Windows 可执行文件，但也可以根据需要重新构建。

使用 **-h** 标志运行可执行文件会向我们展示以下帮助菜单：

```
C:\Tools\privilege_escalation\windows-privsc-check-master>windows-privsc-check2.exe -h
```

![](img/ec25e59d75726b7041242a56d3376832_529_0.png)

windows-privesc-check v2.0 ([http://pentestmonkey.net/windows-privesc-check](http://pentestmonkey.net/windows-privesc-check))

Usage: windows_privesc_check.exe (--dump [ dump opts] | --dumptab | --audit) [examine opts] [host opts] -o report-file-stem

Options:
- --version show program's version number and exit
- -h, --help show this help message and exit
- --dump Dumps info for you to analyse manually
- --dumptab Dumps info in tab-delimited format
- --audit Identify and report security weaknesses
- --pyshe ll Start interactive python shell

examine opts:
At least one of these to indicate what to examine (*=not implemented)
- -a, --all All Simple Checks (non-slow)
- -A, --allfiles All Files and Directories (slow)
- -D, --drives Drives
- -e, --reg_keys Misc security-related reg keys
- -E, --eventlogs Event Log*
- -F INTERESTING_FILE_LIST, --interestingfiledir=INTERESTING_FILE_LIST
- Changes -A behaviour. Look here INSTEAD
- -F INTERESTING_FILE_FILE, --interestingfilefile=INTERESTING_FILE_FILE
- Changes -A behaviour. Look here INSTEAD. On dir per line
- -G, --groups Groups
- -H, --shares Shares
- -I, --installed_software Installed Software
- -j, --tasks Scheduled Tasks
- -K, --drivers Kernel Drivers
- ...

*列表 550 - 由 PyInstaller 输出的可执行文件*

该工具接受许多选项，但我们将通过一些快速示例进行说明。首先，我们将列出有关系统中用户组的信息。我们将指定不言自明的 `--dump` 以查看输出，并使用 `-G` 列出组。

```
c:\\Tools\\privelege_escalation\\windows-privesc-check-master> windows-privesc-check2.exe --dump -G

windows-privesc-check v2.0 (http://pentestmonkey.net/windows-privesc-check)

[i] TSUserEnabled registry value is 0. Excluding TERMINAL SERVER USER

Considering these users to be trusted:
* BUILTIN\Power Users
* BUILTIN\Administrators
* NT SERVICE\TrustedInstaller
* NT AUTHORITY\SYSTEM

[i] Running as current user. No logon creds supplied (-u, -D, -p).
...
========== Starting Audit at 2019-09-22 12:45:56 ==========
```

```
[+] Running: dump_misc_checks
[+] Host is not in domain
[+] Checks completed

[+] Running: dump_groups
[+] Dumping group list:
BUILTIN\Administrators has member: CLIENT251\Administrator
BUILTIN\Administrators has member: CLIENT251\admin
BUILTIN\Administrators has member: [unknown]\$-1-5-21-2175734670-1758985447-1278008508
BUILTIN\Administrators has member: [unknown]\$-1-5-21-2175734670-1758985447-1278008508
BUILTIN\Guests has member: CLIENT251\Guest
BUILTIN\IIS_IUSRS has member: NT AUTHORITY\IUSR
BUILTIN\Remote Desktop Users has member: CLIENT251\student
BUILTIN\Users has member: NT AUTHORITY\INTERACTIVE
BUILTIN\Users has member: NT AUTHORITY\Authenticated Users
BUILTIN\Users has member: CLIENT251\student
BUILTIN\Users has member: [unknown]\$-1-5-21-2175734670-1758985447-1278008508-513
[+] Checks completed
```

*列表 551 - windows-privesc-check 输出*

脚本成功执行，我们得到了有关系统安全组的信息。

类似 Windows 目标上的 *windows-privesc-check*，我们也可以在 Linux 等 UNIX 衍生系统中使用 *unix-privesc-check*⁴⁰²。我们可以通过不带任何参数运行脚本来查看该工具的提供帮助。

```
student@debian:~$ ./unix-privesc-check
unix-privesc-check v1.4 ( http://pentestmonkey.net/tools/unix-privesc-check )

Usage: unix-privesc-check { standard | detailed }

"standard" mode: Speed-optimised check of lots of security settings.

"detailed" mode: Same as standard mode, but also checks perms of open file handles and called files (e.g. parsed from shell scripts, linked .so files). This mode is slow and prone to false positives but might help you find more subtle flaws in 3rd party programs.

This script checks file permissions and other settings that could allow local users to escalate privileges.
...
```

*列表 552 - 运行 unix-privesc-check*

如上述列表所示，该脚本支持"standard"和"detailed"模式。根据提供的信息，standard 模式似乎执行了一个速度优化的过程，并应提供较少的误报。因此，在接下来的示例中，我们将使用 standard 模式，并将整个输出重定向到一个名为 *output.txt* 的文件。

```
student@debian:~$ ./unix-privesc-check standard > output.txt
```

⁴⁰² (Pentest Monkey, 2019), http://pentestmonkey.net/tools/audit/unix-privesc-check


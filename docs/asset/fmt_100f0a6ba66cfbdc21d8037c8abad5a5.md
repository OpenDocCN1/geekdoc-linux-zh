
`c:\Users\student>reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`

`HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer`

  `AlwaysInstallElevated` `REG_DWORD` `0x1`

`c:\Users\student>reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer`

`HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer`

  `AlwaysInstallElevated` `REG_DWORD` `0x1`

> 列表 548 - 在 Windows 上查询 `AlwaysInstallElevated` 注册表值

如果此设置已启用，我们可以制作一个 MSI 文件并运行它以提升我们的权限。

类似地，在基于 Linux 的系统上，我们可以搜索 `SUID` 文件。

通常，运行可执行文件时，它会继承运行该文件的用户的权限。但是，如果设置了 SUID 权限，该二进制文件将以文件所有者的权限运行。这意味着，如果一个二进制文件设置了 SUID 位且该文件由 root 所有，那么任何本地用户都能以提升的权限执行该二进制文件。

⁴⁸⁸ (Microsoft, 2018). https://docs.microsoft.com/en-us/windows/win32/msi/alwaysinstallelevated

⁴⁸⁹ (Microsoft, 2018). https://www.linux.com/tutorials/what-suid-and-how-set-suid-linuxunix/

我们可以使用 `find` 命令搜索标记为 SUID 的二进制文件。在这种情况下，我们从根目录（`/`）开始搜索，查找设置了 SUID 位的文件（`-type f`），（`-perm -u=s`），并丢弃所有错误消息（`2>/dev/null`）。

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

在这种情况下，该命令发现了多个 SUID 二进制文件。SUID 二进制文件的利用方式会因多种因素而异。例如，如果 `/bin/cp`（复制命令）是 SUID 的，我们可以复制并覆盖敏感文件，如 `/etc/passwd`。

### 18.1.1.13 练习

- 1. 在你的专用 Windows 和 Linux 客户端上执行本节中涵盖的各种手动枚举方法。尝试对本节中使用的工具和命令的各种选项进行实验。

#### 18.1.2 自动化枚举

显然，每个操作系统都包含大量可用于进一步攻击的信息。无论目标操作系统如何，手动收集这些详细信息可能相当耗时。幸运的是，我们可以使用各种脚本来自动化此过程。

在 Windows 上，其中一个这样的脚本是 `windows-privesc-check`，⁴⁰⁰ 它可以在 `windows-privesc-check` Github 仓库中找到。⁴⁰¹ 该仓库已经包含由 PyInstaller 生成的 Windows 可执行文件，但也可以根据需要重新构建。

使用 `-h` 标志运行可执行文件会向我们展示以下帮助菜单：

```
C:\Tools\privilege_escalation\windows-privsc-check-master>windows-privsc-check2.exe -h
```

![](img/ec25e59d75726b7041242a56d3376832_529_0.png)

`windows-privesc-check` v2.0 ([http://pentestmonkey.net/windows-privesc-check](http://pentestmonkey.net/windows-privesc-check))

Usage: `windows_privesc_check.exe` (--dump [ dump opts] | --dumptab | --audit) [examine opts] [host opts] -o report-file-stem

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

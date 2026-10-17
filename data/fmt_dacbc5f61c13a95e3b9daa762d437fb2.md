
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

### 18.1.1.13 练习

- 1. 在你的专用 Windows 和 Linux 客户端上执行本节涵盖的手动枚举方法。尝试实验本节使用的工具和命令的各种选项。

### 18.1.2 自动化枚举

显然，每个操作系统都包含可以进一步攻击的丰富信息。无论目标操作系统是什么，手动收集这些信息都是非常耗时。幸运的是，我们可以使用各种脚本来自动化此过程。

在 Windows 上，每个脚本是 `windows-privesc-check`，可以在 `windows-privesc-check` GitHub 仓库中找到。该仓库已经包含一个由 Installer 生成 Windows 可执行文件，也可以根据需要重新构建。

```
带有 -h 标志运行检查会显示以下菜单：
c:\Tools\privilege_escalation\windows-privesc-check-master>windows-privesc-check.exe -h
```

# windows-privresc-check v2.0 (http://pentestmonkey.net/windows-privresc-check)

用法: `windows_privresc_check.exe [--dump [ dump opts]] | --dumptab | --audit] examine opts [host opts] -o report-file-system`

选项:

- - `--version` 显示程序版本号并退出

- -h,--help 显示此消息并退出

- `--dump` 导出信息供你手动分析

- `--dumptab` 以制表符分隔的格式导出

- `--audit` 识别并报告安全漏洞

- `--pshell` 启动交互式 python shell

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

此工具接受许多选项，但我们将通过一些示例。首先，我们将列出系统中关于组的信息。我们将解释自而其明的 `--dump` 以查看输出，并使用 `-G` 来列出组。

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

由于 Windows 上有 `windows-privesc-check`，我们也可以在 Linux 等 Unix 派生系统在使用 `unix_privesc_check492`。我们可以通过不带任何参数运行脚本来查看帮助信息。

```
student@debian:~$ /unix-privesc-check
unix-privesc-check v1.4 ( http://pentestmonkey.net/tools/unix-privesc-check )
用法: unix-privesc-check { standard | detailed }

"standard" 模式：对大量安全设置进行速度优化的检查。

"detailed" 模式：与标准模式相同，还会检查打开的文件句柄和调用的文件（例如从 shell 脚本解析出的、.so 文件）。此模式较慢且容易产生误报，但可能帮助你发现第三方程序中细微的缺陷。
```

此脚本检查了可能允许本地用户提升权限的权限和其他设置。

列表 552 - 运行 unix_privesc_check

如上面的列表所示，脚本支持 `"standard"`（标准）模式和 `"detailed"`（详细）模式。根据所提供的信息，标准模式似乎执行了速度优化的过程，应该提供更少的误报。因此，在接下来的示例中，我们将使用标准模式并将整个输出重定向到名为 `output.txt` 的文件中。

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

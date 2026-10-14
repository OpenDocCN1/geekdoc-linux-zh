

![](img/43f64015de86d989e30eff5bb284fb96_535_0.png)

## 图 11-9 authconfig 程序

使用 NIS 时会配置的一个重要文件是 /etc/nsswitch.conf 文件。该文件指示 Linux 中的各种系统程序在何处查找所需的配置信息。例如，/etc/nsswitch.conf 文件中的一行看起来像这样：

```
passwd: files
```

此行指示需要读取密码信息的程序参考本地系统上的 /etc/passwd。/etc/nsswitch.conf 中 passwd 行上可以列出的其他选项包括 NIS 服务器的 yp 或 nis，NIS+ 服务器的 nis+ 或 nisplus，数据库文件的 db，或 DNS 服务器的 dns。这些并非全部都用于密码信息，但 /etc/nsswitch.conf 文件包含查找多种类型信息的说明。就目前的讨论而言，你应该知道用户账户信息可以位于 NIS 服务器或其他位置，而不仅仅是 /etc/passwd。

/etc/nsswitch.conf 中的配置行通常包含多个选项。例如，passwd 行可能看起来像这样：

```
passwd: nis+, nis, files
```

这意味着程序应尝试通过联系 NIS+ 系统来查找用户的密码信息；如果找不到，则尝试使用 NIS 系统；如果仍找不到，则检查本地文件 /etc/passwd。这样，你就可以集中管理众多用户账户，同时为特殊情况提供灵活性。

## 章节摘要

- 用户账户可以使用 system-config-users、Webmin、YAST 或各种 Linux 发行版中的类似工具进行图形化管理。用户账户也可以从命令行非常有效地进行管理。
- 在更改 UID 或 GID 时，必须小心不要留下分配了旧 UID 或 GID 的文件。在删除用户或组账户时，必须小心不要无意中重用用户或组名。
- `useradd` 命令用于在命令行上创建用户账户。它依赖于可通过 `-D` 选项查看的默认设置。`groupadd` 命令用于创建新组。
- `usermod` 命令用于修改现有用户账户。`groupmod` 命令用于修改现有组账户。
- 密码过期详细信息可以使用 `chage` 命令配置，也可以使用大多数图形用户配置工具进行配置。
- 当创建新的用户账户时，`/etc/skel` 目录的内容会被复制到用户的新主目录中。`/etc/login.defs` 文件还为新用户账户定义了一些默认信息。
- 用户账户可以使用 `passwd` 命令禁用，或使用 `userdel` 命令删除。一些系统管理员更喜欢永远不删除用户账户，而只是禁用它们并删除用户的文件。
- SUID 和 SGID 权限会导致用户在执行该程序时假设可执行文件所有者的权限。这些特殊权限很有用，但在不受信任的程序文件上使用时可能非常危险。
- 粘滞位和几种其他特殊文件权限安排允许系统管理员仔细控制多个用户如何在共享目录中处理文件。
- 要设置粘滞位、SUID 或 SGID，可以使用 `chmod`，在数字模式下使用额外的一位数字，或在字母模式下使用 `s` 或 `t`。
- 系统管理员可以使用 `wall`、使用 `/etc/motd` 文件或通过电子邮件与用户通信，选择最适合传递消息的方法。
- `sudo` 程序允许普通用户执行需要 root 权限的任务。该程序使用 `/etc/sudoers` 文件进行配置，必须使用 `visudo` 命令进行编辑。
- `/etc/sudoers` 中的每一行都为用户或组配置了在特定计算机系统上使用某些命令的权限。示例配置使基本设置易于配置，但 `sudo` 配置错误可能导致严重的 安全漏洞。

- 可插拔认证模块（PAMs）为系统管理员提供了一种灵活而强大的方式，通过依赖各个模块执行不同的安全任务来精确配置用户安全性的处理方式。

- 多个系统可以通过使用 NIS 或 NIS+ 服务器来共享用户文件，例如 /etc/passwd 和 /etc/shadow。如果网络上存在此类服务器，可以通过使用 authconfig 程序配置系统来使用它。

## 命令摘要

| 命令 | 描述 | 示例 |
|---|---|---|
| authconfig | 在 Red Hat Linux 和 Fedora 中以文本模式菜单驱动程序配置 shadow 密码、NIS 和其他身份验证和安全功能。 | authconfig |
| chage | 查看或更改密码老化信息。 | chage -l nwells |
| fuser | 显示哪些用户正在使用文件系统上的任何文件、其他设备或网络连接。 | fuser /home |
| gpasswd | 分配或更改组的密码，允许知道该密码的人使用 newgrp 命令临时成为该组的成员。 | gpasswd journalists |
| groupadd | 创建新组。 | groupadd journalists |
| groupdel | 删除现有组。 | groupdel journalists |
| groupmod | 更改现有组的名称或 GID。 | groupmod -n press journalists |
| grpck | 检查 /etc/group 和 /etc/gshadow 文件的完整性。 | grpck |
| grpconv | 将包含组密码的现有 /etc/group 文件转换为更新的格式（大多数 Linux 系统的默认格式），其中组密码信息存储在 /etc/gshadow 中。 | grpconv |
| grpunconv | 将现有 /etc/group 和 /etc/gshadow 密码信息转换为旧格式，其中组密码信息仅存储在 /etc/group 中。 | grpunconv |
| newgrp | 临时更改用户的主要组。如果为用户想要更改的组配置了组密码，则可能需要输入组密码。 | newgrp journalists |
| pwck | 验证 /etc/passwd 和 /etc/shadow 文件的完整性。 | pwck |
| pwconv | 将包含加密密码的现有 /etc/passwd 文件转换为更新的格式（大多数 Linux 系统的默认格式），其中所有加密密码都存储在 /etc/shadow 中。 | pwconv |
| pwunconv | 将现有 /etc/passwd 和 /etc/shadow 密码信息转换为旧格式，其中所有加密密码都存储在 /etc/passwd 中。 | pwunconv |
| sg | 临时更改为不同的组；与 newgrp 命令相同。 | sg journalists |
| sudo | 根据 /etc/sudoers 中的配置信息允许访问通常保留给 root 的命令。 | sudo mount /mnt/cdrom |
| system-config-users | 使用此 Red Hat Linux 和 Fedora 提供的图形实用程序查看和编辑用户账户和组信息。 | system-config-users |
| useradd | 创建新用户账户。 | useradd cmoffett |
| userdel | 删除现有用户账户。 | userdel cmoffett |
| usermod | 修改存储在 /etc/passwd 中的现有用户账户的各个部分。 | usermod -c "Liz Osowski" lizw |
| visudo | 编辑 /etc/sudoers 文件以配置 sudo 命令。 | visudo |
| wall | 写给所有人——向系统中所有已登录的用户发送广播消息。 | wall Meet outside for lunch in 10 minutes |

## 关键术语

/etc/login.defs — 存储用于创建新用户账户的默认信息的 文件。

/etc/motd — 可存储每日消息的文件。大多数 Linux 系统默认为空，登录到基于文本的控制台或在终端窗口中启动 shell 时会显示此文件的内容。

/etc/nsswitch.conf — 定义在何处搜索各种系统信息的文件，例如密码和网络配置详细信息。支持将程序定向到本地文件、NIS 或 NIS+ 服务器或其他集中信息存储库。

/etc/skel — 一个目录，其中包含在创建新用户账户时复制到新用户主目录的文件。

/etc/sudoers — 确定普通用户使用 sudo 命令被允许执行哪些操作的配置文件。必须使用 visudo 命令进行编辑。

Network Information Service (NIS) — 一种网络服务，可在多个 Linux 或 UNIX 系统之间提供（其中包括）集中化的用户和密码管理。

NIS+ — Network Information Service 的更新版本。参见 NIS。



更重要的是，你应该对创建日期晚于你安装 Fedora Core 4 日期的 SUID 或 SGID 文件保持怀疑。你还应该警惕不在 `/sbin`、`/usr/bin` 或 `/usr/sbin` 等二进制目录的 SUID 或 SGID 文件。

可以使用以下两个命令获取所有 SUID 和 SGID 二进制文件的列表：

```
find / -perm +2000
find / -perm +4000
```

你应该在安装系统后尽快运行这些命令并保存输出；之后，你应该定期运行它们以检查是否出现了 SUID 或 SGID 文件。如果出现此类文件，请立即使用 `chmod` 移除其执行权限，并参考第 35 章“备份、故障排除和救援”。

## 保护 root 账户

`root` 账户是 Linux 和 Unix 操作系统最大的漏洞之一，因为 `root` 账户是全能的：`root` 账户可以创建、读取、修改和删除系统中的任何文件，或启用或禁用任何资源或服务。由于 `root` 账户非常强大，在大多数情况下，该账户的默认保护——简单的密码——认为是不够的。

幸运的是，对 `root` 账户的安全进行相对简单的更改就可以极大提高你 Linux 系统的整体安全性。涉及的更改是使用 `wheel` 组来保护 `su` 命令。`wheel` 组是一个特殊组，按照惯，其成员是 Unix 系统上唯一被允许访问 `su` 命令的用户。

## 启用 wheel 组

你已经学习过普通用户可以通过命令行调用 `su` 命令，允许用户承担 `root` 身份以执行系统管理任务。这种能力虽然方便，但也是危险的：如果恶意用户可以反复调用 `su`，他们最终可能猜出 `root` 密码，从而获得对整个系统的无限制访问。

## SUID 和 SGID 示例

`su` 命令为 SUID 和 SGID 权限的力量和危险提供了极佳的示例。

`su` 命令之所以能工作，是因为默认情况下它由 `root` 用户拥有并且是一个 SUID 可执行文件。这意味着当它被调用时，它的行为就像是由 `root` 用户调用的一样——赋予程序访问受保护资源的权限，例如更改身份所需的资源。为了说明，查看 `su` 程序的目录列表：

```
root@workstation20 you]# ls -1 /bin/su
-rwsr-xr-x 1 root 19902 Jul 31 07:34 /bin/su
[root@workstation20 you]#
```

按照惯和传统，安全的 Unix 系统使用一个特殊的系统管理员组拥有访问 `su` 命令的权限。所有其他用户都被禁止调用它。要让 `wheel` 组发挥作用，你必须做两件事：

- 向 `wheel` 组添加至少一个具有管理权限的用户，因为他可以调用 `su`。
- 更改 `su` 程序的组所有和权限，将访问限制为 `wheel` 组成员。

## 将用户添加到 wheel

要在命令行中将用户添加到 `wheel` 组，使用带有 `-a` 选项的 `passwd` 命令并将要添加的用户名和组名（在此例中为 `wheel`）作为参数：

```
root@workstation20 you]# passwd -a you wheel
[root@workstation20 you]#
```

## 将用户添加到 wheel

如果你不习惯命令行工具，可以使用第 29 章“桌面系统管理”中讨论的 Fedora Core 4 用户管理器工具将用户添加到 `wheel` 组。

如果你想给其他用户管理权限，现在也将他们添加到 `wheel` 组。在你完成接下来的章节后，只有 `wheel` 组的成员才能调用 `su`。

## 更改 su 的所有权权限

按照需要向 `wheel` 组添加成员后，使用 `chmod` 命令将 `su` 命令的所有者从 `root.root`（用户 `root`，组 `root`）更改为 `root.wheel`（用户 `root`，组 `wheel`）。使用此命令，你可以将执行权限限制为 `wheel` 组成员，完全移除公共执行权限：

```
[root@workstation20]# chown root.wheel /bin/su
[root@workstation20]#
```

现在你已经按照需要将管理员添加到 `wheel` 组并将 `su` 的所有权更改为 `root.wheel`，为 `su` 分配以下权限：

- 所有者 `root`：读取、写入和 SUID 执行
- 组 `wheel`：读取执行
- 非所有者、非组成员无权限

使用 `chmod` 命令的数字模式，你可以通过提供数字代码 `4750` 作为 `chmod` 的参数，随后是你想要更改的文件 `/bin/su` 来分配这些权限：

```
[root@workstation20]# chmod 4750 /bin/su
[root@workstation20]# ls -l /bin/su
-rw-xr-x-- 1 root wheel 19092 Jul 31 07:34 /bin/su
[root@workstation20]#
```

`su` 命令受所有普通用户的保护。不是特殊管理组 `wheel` 成员的用户尝试访问 `su` 命令时，权限被拒绝：

```
jane@workstation20]$ su
bash: /bin/su: Permission denied
```

## 自动注销

不幸的是，非活动会话可能代表严重的安全风险，特别是在允许远程登录的系统上。以这种方式开启的网络连接最终可能被恶意用户劫持，他们随后将获得你系统的访问。

除了在 `telnet` 或远程命令中使用 `ssh` 之外，这种风险最简单的解决方法是设置登录超时——即在用户没有按键后自动注销的延迟。可以使用 `TEOUT` 变量来更改默认 shell，在一段时间闲置后自动注销用户，时间单位为秒。例如，将 `TEOUT` 的值设置为 `1800` 将在 30 分钟后注销用户。

为了在每当用户登录时自动设置 `TEOUT` 变量的值，你必须在 `/etc/profile.d` 目录下创建一个文件，该文件包含一组每次用户登录时自动运行的脚本片段。该文件应以 `.sh` 结尾，表示它是用于标准 shell 的，并设置 `TEOUT` 变量的值。使用文本编辑器创建文件 `/etc/profile.d/secure.sh`，其内容只有一行：

```
TEOUT=1800
```

保存文件并退出编辑器后，不要忘记为所有人标记可执行：

```
[root@workstation20]# chmod ugox /etc/profile.d/secure.sh
[root@workstation20]#
```

Linux 除了标准 shell 外，还包含许多替代 shell；高级 Linux 或 Unix 用户可以使用 `csh` 命令在日常命令行工作环境中选择它们。两个替代 shell 提供了登录超时功能；它们是 `csh` 和 `tsh`。为了适应这些替代 shell，你必须创建另一个脚本片段。在这些中，超时是 `autologout`，计时值单位为分钟。使用文本编辑器为这些 shell 创建一个文件 `/etc/profile.d/secure.csh`，其包含以下行：

```
set autologout=30
```

再次，不要忘记将文件标记为可执行：

```
[root@workstation20 you]# chmod ugox /etc/profile.d/secure.csh own[root@workstation20 you]#
```

## 第 30 章：安全基础

使用任何主要 shell 登录的账户持有者在无活动 30 分钟后将被注销。

# 移除次要 Shell

`chsh` 命令的用户可以选择的 shell 列表包含了几个完全不支持登录超时的 shell。因此，应该将这些 shell 从用户可用的 shell 列表中删除，该列表存储在 `/etc/shells` 中。

默认的 `/etc/shells` 文件如列表 30.2 所示。`ash` 和 `sh` shell 的项不支持登录超时，可以使用文本编辑器删除它们，以生成如列表 30.3 所示的简化版 `/etc/shells` 文件。

列表 30.2 原始的 /etc/shells 文件

| /bin/sh |

| /bin/bash |

| /bin/nlogin |

| /bin/bash2 |

| /bin/ash |

| /bin/bsh |

| /bin/tcsh |

| /bin/csh |

列表 30.3 编辑后的 /etc/shells 文件

| /bin/sh |

| /bin/bash |

| /bin/nlogin |

| /bin/bash2 |

| /bin/tcsh |

| /bin/csh |

在编辑 `/etc/shells` 文件后，用户只能从那些在无活动一段时间后将其注销的 shell 中选择。

# 总结

在本章中，你学习了一些简单但基础的技术，帮助保护你的 Linux 计算机系统免受网络攻击、入侵和意外的安全漏洞。

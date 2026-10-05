

# 48 · 第 4 章

```
# 在标准运行级别运行 getty
1:2345:respawn:/sbin/getty tty1
2:2345:respawn:/sbin/getty tty2
3:2345:respawn:/sbin/getty tty3
4:2345:respawn:/sbin/getty tty4
5:2345:respawn:/sbin/getty tty5
6:2345:respawn:/sbin/getty tty6

# 在运行级别 5 运行 xdm
# xdm 现在是一个独立的服务
x5:2345:respawn:/etc/x11/getdm -F
pppt:2345:respawn:/usr/sbin/ppptd
```

图 4.2：initab 文件控制 Red Linux 的初始化序列（第2部分）。

initab 文件的格式最初非常难以理解。每行都符合以下格式：

```
code:runlevel:action:command
```

code 是一个唯一的单或双字符序列，用于标识 initab 文件中的特定条目。runlevel 表示运行级别 0 执行硬关机所需的进程，运行级别 3 执行启用 Linux 多用户模式所需的进程，而运行级别 6 则允许重启动进程运行。initab 文件有一行用于标识默认的运行级别。在图 4.2 中，除非在启动过程中通过执行 init 程序另有指定，否则将使用运行级别 3。

你可以通过带上运行级别作为参数调用 init 程序来手动运行它。例如，要关闭系统，你可以以 root 用户身份使用以下命令：

```
init 6
```

紧随默认运行级别之后的 si:sysinit/etc/rc.sysinit 条目将进入一个名为 rc.sysinit 的脚本并执行。该脚本会执行诸许多操作，如检查和监控文件系统、为磁盘交换启用内存，并将 Linux 系统时与平台的硬件时钟同步。执行完 rc.sysinit 脚本后，将执行一个带有指定运行级别参数的 rc 脚本。

在 Red Hat 上，rc 执行存在于由运行级别指定的目录中的脚本。当 init 程序以运行级别 3 运行时，initab 文件调用 rc 脚本进行切换，并运行位于 /etc/rc.d/rc3.d 目录下的脚本。Red Hat 的 rc.3 脚本会执行所有以 K 为缀的脚本，然后再执行以 S 为缀的脚本。K 脚本停止可能已经在执行的进程，而 S 脚本启动进程。K 或 S 后的两个数字控制脚本的执行顺序。

在 Red Hat 上，各种运行级别启动或停止相同的进程，通用脚本位于 /etc/rc.d/init.d 目录中，而指向这些脚本的符号链接位于各个 rc.X 目录中。为了向你说明其工作原理，考虑一个 Red Hat 7.1 系统，其中 PostgreSQL 应该在系统启动时启动。虽然 rc3.d 目录包含一个指向 /etc/rc.d/init.d/postgresql 脚本的链接名为 K12postgresql，但它并不包含一个以 S 开头的 /etc/rc.d/init.d/postgresql 链接。在安装 Red Hat 时，它在 rc.3 中放置了关闭 PostgreSQL 的链接，以防用户想手动启动 PostgreSQL 但在 Linux 关机时忘记了。

要让 rc.3 自动启动 PostgreSQL，你只需使用以下命令创建一个指向 /etc/rc.d/init.d/postgresql 的名为 S12postgresql 的链接（其中 12 可以是任何两位数）：

```
ln /etc/rc.d/init.d/postgresql S12postgresql
```

尽管 rc 脚本作为独立进程运行，但 init 程序会显式地等待执行完 initab 文件中的 rc 条目后才会继续。在 rc 脚本完成后，init 程序将执行 initab 文件中的其余条目。我们将跳过大部分，因为它们是自解释其明的。不过，请查看 /etc/getty 脚本。这些脚本启动六个虚拟控制台，这意味着可以在单个系统控制台上以六个不同身份登录六次。要在虚拟控制台之间切换，按下 Ctrl-Alt 然后按你想要查看的控制台数字。

另一个提到此内容的 initab 条目是：

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

该条目允许 Linux 捕获 Ctrl-Alt-Delete 键组合并温和地关闭系统。

# 自定义启动

配置 PostgreSQL 启动的更好方法不是在 rc.3 目录中添加链接，而是修改名为 /etc/rc.d.local 的脚本。每个 rc.N 目录都包含一个名为 S99local 的链接，指向文件 /etc/rc.d.local。因为 99 是最大的可能数字，名为 rc.local 的脚本将始终最后执行。因此，与其创建一个名为 S12postgresql 的链接，你可以将该条目放在 rc.local 脚本中：

```
/etc/rc.d/init.d/postgresql start
```

这种方法有两个优点：

- 它将你所有的启动修改都放在于一个脚本文件中。
- 你可以确保你的自定义进程在所有默认进程初始化之后启动。

# 登录

root 用户是 Linux 中全能的配置，也称为超级用户（super user）。在安装 Linux 时，系统会提示你输入 root 用户的密码。Linux 安装的一部分是创建一个权限较低的用户。正如第 3 章讨论的，Linux 的安全设置使得系统上的所有文件都有三个级别的授权：用户（或所有者）、用户组，以及既不是所有者也不属于授权用户组的用户。root 用户无所不能，拥有访问所有文件的权限。出于安全考虑，你应该仅在需要时才登录。

为了方便使用 root 登录，Linux 提供了 su 命令（代表 "super user"）。如果你以 root以外的用户登录，但需要 root 权限，可以使用 su 命令，它会提示输入 root 密码。然后你可以执行需要 root 权限的命令。但是，请务必使用 exit 命令返回你具有超级（且可能危险）权限的普通用户化身。当你以 root 登录时，也可以使用 su 命令临时切换到普通用户角色。在这种情况下，命令需要用户名。例如，在 root 登录时临时以用户 bill 的身份运行，你将使用：

```
su bill
```

# 运行 Linux 命令

Linux 登录界面被称为 bash shell。一旦登录 Linux，你就可以通过 调用成千上万个命令。第 12 章将详细介绍 bash，而本节将引导你掌握 bash 和通用 Linux 命令的知识。bash 提示符默认显示你的用户名、主机名、当前目录，如果以普通用户登录则显示美元符号 ($)，如果以 root 登录则显示井号 (#)。

从 bash 提示符开始，你已经准备好掌握 Linux。许多 Linux 命令遵循通用结构：

```
command option(s) argument(s)
```

然而，许多命令不需要选项或参数。表 4.1 显示了一些基础 Linux 命令。cd 命令用于在文件系统的各个目录间移动。当你使用 cd 时，可以使用相对路径或绝对路径。绝对路径意味着指定完整的路径（/）。例如，要切换目录到 /usr/local 将使用以下命令：

```
cd /usr/local
```

相对路径用于相对于当前目录切换目录。例如，如果你在 /usr/local 想要返回上一级目录，将使用：

```
cd ..
```

单个点 (.) 表示当前目录。

# Linux 配置与启动

表 4.1：一组基础 Linux 命令
| 命令 | 描述 |
|---|---|
| cd | 切换目录。 |
| pwd | 打印工作目录。 |
| ls | 列出目录下所有的文件、目录和链接。 |
| cp | 复制文件。 |
| mv | 移动或重命名文件。 |
| less | 分页查看显示文件内容。 |
| man | 显示命令文档。 |
| apropos | 列出所有帮助页中包含参数字符串的命令。 |


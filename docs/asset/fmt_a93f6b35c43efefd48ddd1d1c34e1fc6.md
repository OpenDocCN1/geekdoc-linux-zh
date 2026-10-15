
| `head filename` `tail -f logfilename` | Head 显示文件的前几行。Tail -f 用于跟踪增长中的文本文件或日志。 |

| `history` | 显示你之前执行过的命令。 |

# 第 2 章 • 理解 Unix

| Linux 命令 | 对应的命令（如果有） | 作用 |
|---|---|---|

| `script scriptfile name` | | 在指定的文件中创建你的命令行活动日志。对于记录你的活动以取证据非常有用！在输入你想要记录的最后一个命令后，输入 `"exit"`。 |

| `strings script name / less` | | 剥离所有控制字符，只显示可打印的字符串字符，用于查看命令脚本，或确切地说，查看任何二进制文件。 |

| `date` | | 显示当前日期，在 `script` 捕获的命令会话内部非常有用，可以提供粗略的时间戳。 |

| `export PS1=$(USER)@${HOSTNAME}:\d:\t\w\$` | 提示符 | 通过特殊的 BASH 环境变量 `PS1` 将你的 BASH 命令提示符设置为包含你的用户名、主机名、当前日期、时间以及工作目录。详情请查看 `man bash`。 |

| `man command name` | `help commandname` `commandname?` | 手册（Manual pages）。RTFM（去读那本手册）。阅读那本（精良）手册。非常重要，Man 是在线命令参考手册的接口。与有用但可用性不稳定的 Windows 帮助不同，*nix 作者为几乎每个可用的命令行程序都详细编写了 man 页面。 |

| `man -k keyword /less` | | `-k` 选项允许你通过关键字搜索 man 页面，以便找到与你想操作相关的命令。这在 Web 和搜索引擎出现之前更为重要，但现在仍然有用。 |

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_30_0.png)

# 理解 Unix • 第 23 章

| Linux 命令 | 最接近的 Windows 命令行（如果有） | 作用 |
|---|---|---|

| `find` | 资源管理器中的搜索功能，可能还有那只奇怪的动画狗？ | 令人不可或缺的文件查找/搜索命令。在 *nix 中你可能做的几乎任何操作可能都可以通过一个合适的长命令来实现。作为取证分析师，你会爱上这个命令的。 |

| `grep pattern` | | 显示文件中与给定搜索字符串模式匹配的行。另一个巨大且不可缺的工具。 |

| `df . df` | | 列出当前目录（`.` 代表当前目录）的磁盘空间。如果没有 `. df`，则列出所有挂载文件系统的磁盘使用情况。单位以块为单位，取决于磁盘如何格式化，大小可能为 1kB。 |

| `du -sk du -k` | | 显示当前目录及其所有子目录以 KB 为单位磁盘使用摘要。 |

| `mount` | | 列出已挂载的文件系统。稍后将详细介绍该概念。不急的人看 `man`。 |

| `dd` | | 磁盘转储器（Disk dumper）。正如你预期的，这对于取证社区非常重要！这是一个原生的 *nix 命令，可以导出原始磁盘设备，包括所有空闲区域（slack space）。 |

| `sudo` | `runas` | Sudo 是任何需要 root（管理员）超级用户权限的命令前的前缀。 |

| `mkdir directory` | `md` | 创建目录。 |

# 第 2 章 • 理解 Unix

`sudo mount -t auto /dev/device /media/mountpoint`

Windows 在启动时插入 USB 设备时会自动尝试此操作。

要挂载文件系统，你需要 root 权限，因此在命令前加上了 `sudo`。这个示例显示将磁盘挂载到一个空目录，并自动检测其文件系统类型。

`sudo umount /media/mountpoint`

右键点击 Ej 或 安全地删除硬件图标

卸载文件系统。例如，从系统中移除 USB 闪盘或外部硬盘。

`chmod file chown file chgrp file`

`attrib`

更改文件的权限、文件所有权和组所有权。

你应该加入 *nix 词汇表的其他需要查阅的命令包括：`top`（显示按 CPU 利用率排序的运行程序）、`ps -ef`（显示所有运行进程）、`netstat -an`（显示所有网络连接）、`last`（显示登录用户）、`who`（显示当前登录用户）、`uname -a`, `cp`, `rmdir`, `touch`, `wc -l`, `passwd`, `su -`, `gunzip`, `gzip`, `tar`, `zcat`, `env`, `ps`, `cut`, `uniq`, `alias`, `ssh`, `scp`, `rsync`, `fsck` 以及为了在这些操作中留有一点余地的 `cowsay`。

```
ubuntu@ubuntu:~$ cowsay "Cus it's the bomb!"
```

```
< Cus it' da bomb! >
^ ^^
\ (oo)
  (  _ )/\
  ||-----||
  ||     |
```

当然，在处理可能受损的机器上工作时，信任该机器上安装的二进制文件的输出是愚蠢的。准备一个包含这些命令静态链接版本的 CD，并运行这些二进制文件而不是运行（可能作为 rootkit 的被修改过的）已安装版本，始终是一个明智之举。

最后，现代 *nix 的两个 Windows 可能会忽略的命令行功能是：文件名补全和命令补全。试一下！开始输入文件名并按 TAB 键。如果没有发生什么，再次按一次。当你看到那个长文件名被自动补全，或者立即出现一个可能的补全列表时，你会奇怪自己以前没有它的情况下是怎么活过来的。顺便提一下，Windows `cmd.exe` 有文件名补全，但你可能需要调整注册表项来启用它。此外，通常按上方向键可以获取之前的命令历史，这可以节省大量的重复输入。Windows 也有类似的功能。

## Linux 安全模型亮点

Linux 和 *nix 在安全方面比 Windows 严格得多。安全性渗透在 *nix 操作系统的设计中，而不是像 Windows 那样有时只是事后考虑。例如，在 *nix 世界中，不存在这种……（此处原文似乎不完整，根据上下文翻译至此）。

上述，我们看到长格式的 shadow 和 passwd 文件。左侧的权限显示所有者、组和其他人可以做什么。`r` 是读，`w` 是写，`x` 是执行。在 *nix 中，权限可以用数字表示，例如 `-rw-r--` 可以表示为 644。对于 root 用户，或者在命令前加上 `sudo`。

# 理解 Unix：第 27 章

```bash
cat: foo: Permission denied
ubuntu@ubuntu:~$ chmod u+r foo # 添加用户/所有者权限
ubuntu@ubuntu:~$ ls -l foo
-r--r--r-- 1 ubuntu ubuntu 0 2008-04-14 20:25 0
ubuntu@ubuntu:~$ cat foo # 现在我们可以再次读取了，但它是一个空文件
ubuntu@ubuntu:~$
```

除了我们在示例中探索的这些读、写、执行权限外，*nix 对文件还具有“设置用户 ID (set UID)”和“设置组 ID (set GID)”权限的概念。在 Windows 的新建文件系统 (NTFS) 或文件分配表 (FAT) 中，没有类似的文件属性。这些可执行文件会将有效用户 ID 或组 ID 更改为程序执行时的身份。这带来的安全影响可能是严重的，它们在取证分析中非常重要，因为这些权限允许可执行文件以另一个用户的身份运行，无论是谁运行该程序。例如，许多需要硬件特权访问的命令被设置为用户 ID 为 root，这在权限的“用户/所有者”位置用“s”标出：

```bash
ubuntu@ubuntu:~$ ls -l /bin/ping
-rwxr-xr-x 1 root root 30856 2007-07-06 02:40 /bin/ping
```

当任何用户运行 `/bin/ping` 时，它都会以超级用户 (root) 的身份运行。

你不希望在系统中发现一个设置了用户 ID (SUID) 为 root 的 `/bin/bash` 副本或任何其他 shell。其影响是显而易见的。任何执行此类 shell 用户都可能变成 root。现代 shell 内置了防止这种经典攻击的保护，但所有 SUID root 的 shell 副本对取证调查员来说都应该是警信号。

这种类型的文件权限非常重要。文件权限根据以下内容定义：

- 所有者权限 (`u`，用户/所有者可以读取、写入或执行此文件吗？)

- 组权限 (`g`，组可以读取、写入或执行吗？)

- 全员权限 (`o`，系统上的其他人可以读取、写入或执行吗？)

- SUID/SGID 权限 (`s`，当执行它时，我们会更改有效用户 ID 或组 ID 吗？)

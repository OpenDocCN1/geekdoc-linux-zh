
# 44 UNIX 系统管理：入门指南

```
drwx-xr-xr-x 4 root bin      512 Mar 16 2001 demo
drwx-xr-xr-x 8 root bin      512 Mar 16 2001 dict -> ../share/lib/dict
drwxr-xr-xr-x 1 root root      512 Mar 16 2001
drwx-xr-xr-x 10 root bin      512 Mar 16 2001 dt
drwx-xr-xr-x 2 root bin      512 Mar 16 2001 games
drwx-xr-xr-x 23 root bin     4096 Mar 19 2001 include
drwx-xr-xr-x 1 root other       9 Mar 16 2001 java -> ./java1.2
drwx-xr-xr-x 6 root bin      512 Mar 16 2001 javalib.1
drwx-xr-xr-x 7 root bin      512 Mar 16 2001 javalib.2
drwx-xr-xr-x 9 root sys      512 Mar 16 2001 kernel
drwx-xr-xr-x 6 root bin      512 Mar 16 2001 lve
drwx-xr-xr-x 54 root bin     12288 Mar 19 2001 lib
drwx-xr-xr-x 8 root sys      512 Sep 25 15:24 local
drwxr-xr-xr-x 1 root root      512 Mar 16 2001 mail -> ../var/mail
drwxr-xr-xr-x 1 root root      512 Mar 16 2001 man -> ../share/man
drwx-xr-xr-x 4 root root      512 Mar 16 2001 net
drwxr-xr-xr-x 1 root bin      512 Mar 16 2001 news -> ../news
drwxr-xr-xr-x 2 root bin      512 Mar 16 2001 old
drwxr-xr-xr-x 8 root root      512 Mar 16 2001 os-admin - at the beginning of this line
drwx-xr-xr-x 5 root bin      512 Mar 16 2001 per15
-rw-r--r-- 1 root other      1024 Sep 25 18:10 per_reid
drwx-xr-xr-x 15 root sys     1024 Mar 19 2001 platform
drwx-xr-xr-x 1 root root      512 Mar 16 2001 preserve -> ../preserve
drwx-xr-xr-x 3 root root      512 Mar 16 2001 proc
drwx-xr-xr-x 8 root bin      512 Mar 16 2001 pub -> ../share/lib/pub
drwx-xr-xr-x 6 root root      512 Mar 16 2001 sadm
drwx-xr-xr-x 1 root root      512 Mar 19 2001 sbin
drwxr-xr-xr-x 1 root root      512 Mar 16 2001
drwx-xr-xr-x 5 root bin      512 Mar 16 2001
drwx-xr-xr-x 9 root sys      512 Mar 16 2001 snadm
drwx-xr-xr-x 1 root root      1024 Mar 16 2001 spool -> ../var/spool
drwx-xr-xr-x 1 root root      1024 Mar 16 2001 src -> ../share/src
drwx-xr-xr-x 1 root root      1024 Mar 16 2001 tmp -> ../var/tmp
drwx-xr-xr-x 4 root bin      2048 Mar 16 2001
drwx-xr-xr-x 5 root bin      512 Mar 16 2001 include
drwx-xr-xr-x 1 root bin      512 Mar 16 2001 lib
drwx-xr-xr-x 4 root bin      512 Mar 16 2001 xpg4
```

虽然上面的输出看起来很奇怪，但每个目录和文件包含固定数量的字段，如图 **2-2** 所示。

| 所有者 | 大小 | 名称 |
| :--- | :--- | :--- |
| -rww-xr-x | 4 root bin | 1844 Jul 13 15:03 |
| 修改日期/时间 (创建) | | |
| 文件类型 | 链接数 | |

你可以看到，UNIX 支持额外的文件类型，如表 **2-6** 所示。块特殊文件用于磁盘（软盘、硬件设备和 CD-ROM）。字符特殊文件用于终端或打印机等设备，信息以单个字符的形式输出。符号链接只是指向另一个文件的指针，可以跨不同的文件系统。socket 和管道文件用于进程间操作，以便它们共享信息和数据。

剩余的位代表文件的基本访问机制。总共 9 位用于定义三个访问级别：所有者、组和世界。所有者级别代表文件相关的实际用户名（如 `root`）。组代表文件相关的组（如 `other`），世界代表系统中定义的其他人。

在这些层级中的每一个中，三个访问权限如表 **2-7** 所示。

## 模块 2：基础 UNIX 命令

### 表 2-6 标准 UNIX 文件类型

| 文件标志 | 含义 |
| :--- | :--- |
| - | 无特定标志；表示普通文件 |
| b | 块特殊文件，用于硬件设备 |
| c | 字符特殊文件，用于硬件设备 |
| d | 目录 |
| l | 符号链接 |
| s | 套接文件 |
| p | 管道文件 |

### 表 2-7 文件访问位

| 访问位 | 含义 |
| :--- | :--- |
| r | 文件是读的。 |
| w | 文件是可写的。 |
| x | 文件可以执行或作为程序运行。如果是目录，可以搜索。 |

请注意，UNIX 支持额外的访问位。这些包括用于强制锁定的 `1`、用户/组设置 ID `s` 以及粘滞位 `t`（sticky bit）。强制锁定与在程序访问文件时锁定读取或写入权限有关。`s` 表示可以使用文件的所有者身份（如 `root`）执行。这是管理员以控制的方式让普通用户访问特权命令的方法。粘滞位提供了更有效地引用文件的能力。

每个文件都支持针对文件或目录三个安全元素的访问位。前三个表示所有者，接下来的三个是其他人。如图 **2-3** 所示。管理员可以使用这些权限位来控制对文件的访问。此外，文件的所有者也可以控制这些位。

每个位都控制如何访问文件。当 `r` 存在时，当 `w` 存在时文件是可写的；当 `x` 存在时，文件可以执行。在目录的情况下，`x` 表示可以搜索。当然，执行位只有在文件代表二进制程序或某些脚本时才有意义。

表 2-8 包含了 UNIX 文件和/或目录可能的不同文件权限示例。

| 所有者 | 其他 |
| :--- | :--- |
| rwx | rwx |

![](img/2928fe42a92e6fb43bbbe3768008092f_66_0.png)

# 46 UNIX 系统管理：入门指南 47

### 权限模式

| 含义 |
| :--- |
| -rw-r-- 所有者可读写，组和其他人只读。 |
| -rw------ 文件仅所有者可读写。 |
| -rw-rw---- 文件仅所有者和组可读写。 |
| -rwxr-xr-x 文件（目录）所有者可读、写、执行，组和其他人均可执行。 |
| -rwx----x 文件（目录）所有者可读、写、执行，组和其他人仅可执行。 |
| 表 2-8 权限模式示例 |

信息——而非用户数据。管理员将使用此字段来确定每个文件消耗磁盘空间。事实上，如果不完全自动化，监控磁盘空间和清理不需要/未使用的文件会占用大量时间。接其后的字段是文件修改字段，它显示了文件最后更新的时间。剩余的文件属性是文件名。

`ls` 命令的一个非常强大的参数是 `-R` 选项。它告诉程序递归显示给定路径名称下的所有目录/文件。例如，考虑图 2-4 所示的目录结构。

当对此目录执行 `ls -R` 命令时，我们得到：

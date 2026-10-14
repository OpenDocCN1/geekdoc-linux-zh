

## 1.102.6 使用 Red Hat 软件包管理器 (RPM)

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 8 | 考生应能够在用于软件包分发的 Linux 发行版上执行软件包管理。此目标包括能够安装、重新安装、升级和删除软件包，以及获取软件包的状态和版本信息。此目标还包括获取软件包信息，如版本、状态、依赖关系、完整性和签名。考生应能够确定软件包提供的哪些文件，以及找到特定文件来自哪个软件包。关键文件、术语和实用程序包括：/etc/rpmrc, /usr/lib/rpm/*, rpm, grep。 | Chapter 10, "Managing Packages" |

## Topic 103 GNU and UNIX Commands

## 1.103.1 Work on the Command Line

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应能够使用命令行与 shell 和命令进行交互。这包括输入有效的命令和命令序列；定义、引用和导出环境变量；使用命令历史和编辑功能；在路径中和路径外调用命令；使用命令替换；通过目录树递归应用命令；以及使用 man 来了解命令。关键文件、术语和实用程序包括：bash, echo, env, exec, export, man, pwd, set, unset, ~/.bash_history, ~/.profile。 | Chapter 1, "Starting to Use Linux" and "Exploring the File System" |

|  |  | Chapter 3, throughout |

## 1.103.2 Process Text Streams Using Filters

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 6 | 考生应能够对文本流应用过滤器。任务包括将文本文件和输出流通过文本实用程序过滤器发送以修改输出，以及使用 GNU textutils 包中包含的标准 UNIX 命令。关键文件、术语和实用程序包括：cat, cut, expand, fmt, head, join, nl, od, paste, pr, sed, sort, split, tac, tail, tr, unexpand, uniq, wc。 | Chapter 5, "Manipulating Files" |

## 1.103.3 Perform Basic File Management

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够使用基本的 UNIX 命令复制、移动和删除文件和目录。任务包括高级文件管理操作，例如递归复制多个文件、递归删除目录，以及移动符合通配符模式的文件。这包括使用简单和高级的通配符规范来引用文件，以及使用 find 根据类型、大小或时间查找和操作文件。关键文件、术语和实用程序包括：cp, find, mkdir, mv, ls, rm, rmdir, touch, file globbing。 | Chapter 1, "Exploring the File System" |
|  |  | Chapter 4, "Introducing the File System" |
|  |  | Chapter 5, "Regular Expressions" |

## 1.103.4 Use Streams, Pipes, and Redirects

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应能够重定向流并连接它们以便高效处理文本数据。任务包括重定向标准输入、标准输出和标准错误，将一个命令的输出通过管道传输到另一个命令的输入，使用一个命令的输出作为另一个命令的参数，以及将输出同时发送到 stdout 和文件。关键文件、术语和实用程序包括：tee, xargs, <, <<, >, >>, |, ` | Chapter 3, "Data Redirection" |

## 1.103.5 Create, Monitor, and Kill Processes

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应能够管理进程。这包括知道如何在前台和后台运行作业，将作业从后台调至前台以及反之亦然，启动一个在注销后仍运行且不连接终端的进程，以及发出信号使程序在注销后继续运行。任务还包括监控活动进程，选择和排序进程以显示，发送信号给进程，杀死进程，以及识别并杀死在 X 会话关闭后未终止的 X 应用程序。关键文件、术语和实用程序包括：&, bg, fg, jobs, kill, nohup, ps, top。 | Chapter 6, "Defining Processes" and "Managing Linux Processes" |

## 1.103.6 Modify Process Execution Priorities

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够管理进程执行优先级。任务包括以更高或更低的优先级运行程序，确定进程的优先级，以及更改正在运行进程的优先级。关键文件、术语和实用程序包括：nice, ps, renice, top。 | Chapter 6, "Managing Linux Processes" |

## 1.103.7 Search Text Files Using Regular Expressions

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够使用正则表达式操作文件和文本数据。此目标包括创建包含若干记号元素的简单正则表达式。它还包括使用正则表达式工具在文件系统或文件内容中执行搜索。关键文件、术语和实用程序包括：grep, regexp, sed。 | Chapter 5, "Manipulating Files" |

## 1.103.8 Perform Basic File-editing Operations Using vi

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生必须能够使用 vi 编辑文本文件。此目标包括 vi 导航、基本的 vi 节点、插入、编辑、删除、复制和查找文本。关键文件、术语和实用程序包括：vi, /, ?, h, j, k, l, G, H, L, i, c, d, dd, p, o, a, ZZ, :w!, :q!, :e!, :! | Chapter 3, "Editing Text with vi" |
|  |  | Chapter 5, "More Advanced Text Editing" |

## Topic 104 Devices, Linux File Systems, and File System Hierarchy Standard

## 1.104.1 Create Partitions and File Systems

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够配置磁盘分区，然后在诸如硬盘等介质上创建文件系统。此目标包括使用各种 mkfs 命令设置分区为各种文件系统，包括 ext2, ext3, reiserfs, vfat, 和 xfs。关键文件、术语和实用程序包括：fdisk, mkfs。 | Chapter 4, "Introducing the File System" |
|  |  | Chapter 8, "Configuring Disk Space" |
|  |  | Chapter 10, "Understanding the File System" |

## 1.104.2 Maintain the Integrity of File Systems

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够验证文件系统的完整性，监控可用空间和 inode，并修复简单的文件系统问题。此目标包括维护标准文件系统所需的命令，以及与日志文件系统相关联的额外数据。关键文件、术语和实用程序包括：du, df, fsck, e2fsck, mke2fs, debugfs, dumpe2fs, tune2fs。 | Chapter 10, "Understanding the File System" |

## 1.104.3 Control Mounting and Unmounting File Systems

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够配置文件系统的挂载。此目标包括能够手动挂载和卸载文件系统，在启动时配置文件系统挂载，以及配置用户可挂载的移动文件系统，如磁带驱动器、软盘和 CD。关键文件、术语和实用程序包括：/etc/fstab, mount, umount。 | Chapter 4, "Introducing the File System" |
|  |  | Chapter 10, "Understanding the File System" |

## 1.104.4 Managing Disk Quotas

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够为用户管理磁盘配额。此目标包括为文件系统设置磁盘配额，编辑、检查和生成用户配额报告。关键文件、术语和实用程序包括：quota, edquota, repquota, quotaon。 | Chapter 10, "Understanding the File System" |

## 1.104.5 Use File Permissions to Control Access to Files

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应能够通过权限控制文件访问。此目标包括常规文件和特殊文件以及目录的访问权限。还包括 suid、sgid 和粘滞位等访问模式，使用组字段为工作组授予文件访问权限，不可变标志，以及默认文件创建模式。关键文件、术语和实用程序包括：chmod, umask, chattr。 | Chapter 4, "File Permissions" |
|  |  | Chapter 11, "Complex File Permissions" |

## 1.104.6 Manage File Ownership

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够控制文件的所有者和组。此目标包括能够更改文件的所有者和组所有者，以及新文件的默认组所有者。关键文件、术语和实用程序包括：chmod, chown, chgrp。 | Chapter 4, "File Permissions" |

## 1.104.7 Create and Change Hard and Symbolic Links

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够为文件创建和管理硬链接和符号链接。此目标包括能够创建和识别链接，通过链接复制文件，以及使用链接文件支持系统管理任务。关键文件、术语和实用程序包括：ln。 | Chapter 4, "Introducing the File System" |



# 第 4 章：系统监控

## 4.9 使用 ping 监控

### 示例二：使用 ping 监控主机

变体：AT&T

语法：

```
ping [pattern]
echo [string]
mail [string]
sleep [value]
```

如果网络出现问题时，输出将像这样：

```
3 packets transmitted, 0 packets received, 100% packet loss
```

## 本章章节

第 4 章：系统监控；4.9 使用 ping 监控

- 4.1 启动时监控
- 4.2 从全新安装开始监控
- 4.3 使用 `tail` 监控
- 4.4 将日志减半
- 4.5 为进程发送邮件
- 4.6 监控磁盘空间
- 4.7 寻找磁盘大户
- 4.8 通过 `grep` 比较差异进行监控
- 4.9 使用 `ping` 监控
- 4.10 监控核心文件 (Core Files)
- 4.11 崩溃文件
- 4.12 记住夏令时制
- 4.13 检查时间

## UNIX 提示与技巧

## 第 4 章：系统监控

### 本章章节

- 4.1 启动时监控
- 4.5 为进程发送邮件
- 4.9 使用 `ping` 监控
- 4.13 检查时间
- 4.2 带有守护进程启动
- 4.6 监控磁盘空间
- 4.11 监控崩溃文件
- 4.7 寻找磁盘大户
- 4.3 使用 `tail` 监控
- 4.12 记住夏令时制
- 4.8 通过 `grep` 比较差异进行监控
- 4.4 将日志减半

## 4.10 监控核心文件

### 4.10.1 描述

留意核心文件（core files）是浪费磁盘空间的重要方法。如果用户不需要这些文件，就将它们删除。

### 示例一：定位核心文件

变体：AT&T, BSD  
Shell：全部  
语法：

```
find dirname -xdev [-local] [-mount] [-name file] expression
```

在使用 `find` 命令时，有许多可用选项。其中一个选项可以防止 `find` 跨越文件系统（包括 NFS 挂载的文件系统）。请检查你的 `man` 手页以查看你的版本使用的是哪一个。该函数的可用参数有 `-x`, `-xdev`, `-local` 和 `-mount`。

使用以下命令，在本地根文件系统中搜索所有三天内未被访问过的核心文件，并将它们显示在标准输出：

```
# find -xdev -name core -atime +3 -print
```

如果在你的环境中确定删除所有核心文件是安全的，`find` 可以在找到的核心文件上执行 `remove` 命令：

```
# find / -local -name core -exec rm -f {}
```

在这个版本的命令中，`find` 在系统本地搜索名为 `core` 的文件。如果找到，它将将其存储在缓冲区中，并对缓冲区中的文件执行 `rm` 命令。此过程将持续到 `find` 命令完成搜索。可以将其放在 `crontab` 中每晚运行一次。`crontab` 条目显示如下：

```
15 12 * * * find / -local -name core -exec rm -f {} \;
```

### 原因

当程序接收到 QUIT 信号时，它会将发送信号时内存中的内容写入磁盘。这些核心文件可能与系统内存一样大；它们等同于创建核心文件时运行应用程序所占用的内存。

### 实战经验

根文件系统的分区空间有时只有 7-30MB。如果创建了一个巨大的核心文件导致根目录写满，系统可能会缓慢变慢直至停止或崩溃。

密切关注这些文件非常重要。在今天，某些供应商可能已经在你运行的 `crontab` 中内置了此 `find` 命令。它是那些被遗忘的命令之一，会在糟糕的日子增加管理员的头疼。

核心文件可以写在系统的各个地方。每个核心文件所在的地方都可以被单独考虑，以确定是否需要立即删除该文件。当内存转储到核心文件中时，可以使用用户主目录、应用程序所在的目录或根目录。

- **用户主目录 (User Home)**：当转储核心文件时，它会被放在应用程序的用户目录中。在删除之前，你应该检查并验证用户是否在删除核心文件前遇到了应用程序问题，并且正在与需要核心文件来解决问题的用户合作。实际上，10 个用户中有 9 个需要核心文件，而其中一半的人甚至不知道该文件是什么或它是如何生成的。他们把文件留在目录里，认为这是系统作为其账户的一部分使用的核心文件。
- **应用程序目录 (Application Directory)**：如果应用程序运行守护进程并发生崩溃，应用程序可以捕获信号并将核心文件写入应用程序所知的环境变量设置的预定义目录。供应商这样做是为了可以告诉用户，必要的维护和支持文件可以帮助解决用户与开发者合作时遇到的问题。应用程序的用户可能正在与开发者合作解决他们遇到的任何问题。你可能想在删除这些文件之前进行检查。
- **根目录 (Root Directory)**：最终出现在根目录的核心文件应该被分析或删除。当以 root 身份运行的应用程序以 QUIT 信号结束，或者在某些 BSD 系统上，当操作系统因内存奇偶错误或其他硬件故障发生硬性崩溃时，核心文件就会存在于此。

由于这些文件是二进制文件，你可能想使用 `string` 命令来提取你需要的任何有用信息。文件大小可能非常大，所以你应该将命令通过到 `more`：

```
# strings core | more
```

## 4.11 监控崩溃文件

```
kernel putbuf:
pb 0: cunting filesystem: / filesystem: / (dev: 128/16)
pb 1: <NOTICE> Starting XFS recovery for filesystem: / (dev: 128/16)
pb 2: <NOTICE> Ending XFS recovery for filesystem: / (dev: 128/16)
pb 3: <WARNING> Process [explorer] 10768 generated trap, but has signal 11 held or ignored
pb 4: Process has been killed to prevent infinite loop
pb 5: <WARNING> Process [explorer] 23645 generated trap, but has signal 11 held or ignored
pb 6: Process has been killed to prevent infinite loop
pb 7: Recoverable memory error corrected by CPU at 0x9116190
pb 8: Memory Patrol Error in SIMM S2
pb 9: GIO Error/Addr 0x400:<TIME > 0x7f242c0
pb 10:
pb 11: <>PANIC: IRIX Killed by Bus Error
pb 12: at PC:088082ee ep:0xffffca20
pb 13:
pb 14:
pb 15: Dumping to dev 0x2200011 at block 0, space: 0x27fa5 pages
```

### 原因

这是一个你应该尽可能使用的极佳功能。当系统崩溃时，syslog 可能没有足够记录系统崩溃的原因。在这种情况下，你不会在系统日志文件中看到任何问题，除非这些问题是随着时间推移发展的。由于内容被转储（dumped），你更有可能知道系统崩溃的原因。

### 实战经验

由于这些是以二进制格式写入的核心类型文件，你可能想要使用 `strings` 命令。在大多数情况下，崩溃文件中包含有用信息。供应商也有自己的一套工具来从崩溃文件中提取问题，但他们不会将这些工具发布给我们的系统管理员。你最好的办法是尝试获取可能写入崩溃文件的错误信息。

```
# /var/adm/crash
# ls -al
-rw------- 1 root 3968160 Sep 21 11:28 unix.0.
# strings uniq.0 | grep -i errors | | more
```

```
panic string: <PANIC> IRIX Killed by Bus Error
pb 7: Recoverable memory error corrected by CPU at 0x9116190 <0x302>
pb 8: Memory Patrol Error in SIMM S2
pb 9: GIO Error/Addr 0x400:<TIME > 0x7f242c0
pb 11: <>PANIC: IRIX Killed by Bus Error
```

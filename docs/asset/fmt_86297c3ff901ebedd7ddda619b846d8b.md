
# Read the Manual

## Read the .h files

The manpage says the structure of utmp is in `utmp.h`. On most machines, the header files are stored in the directory `/include`. We use `more` to read the file:

```
#include <stdio.h>

#define UTMP_FILE "/var/adm/utmp"
#define WTMP_FILE "/var/adm/wtmp"
#include <sys/types.h> /* for pid_t, time_t */
/*
* Structure of utmp and wtmp files.
*
* Assuming these numbers are unwise.
*/
#define ut_name ut_user /* compatibility */
struct utmp {
    char ut_user[32]; /* User login name */
    char ut_id[14]; /* /etc/inittab id - IDENT_LEN in
    * init */

    char ut_line[32]; /* device name (console, linox) */
    short ut_type; /* type of entry */
    pid_t ut_pid; /* process id */
    struct exit_status { /* Process termination status */
        short e_termination; /* Process exit status */
        short e_exit;
    } ut_exit; /* The exit status of a process */
    * marked as DEAD_PROCESS.

    time_t ut_time; /* time entry was made */
    char ut_host[64]; /* host name same as */
    * MAXHOSTNAMELEN */

};
```

`/* Definitions for ut_type */`

`utmp.h` (60%)

After skipping messages and other introductory material, we find this structure definition. Log-in records, it appears, consist of eight members. The `ut_user` array stores the user log-in name.

As you read various pages, you introduce you to related, interesting, and useful topics. We have our mission, so we study the `<utmp>` file.

# 第2章 用户、文件与手册：谁是第一个

即用户连接的。在结构体的后续几行中，`ut_time` 用于存储日志时间，`ut_host` 用于存储远程计算机的名称。

该结构体还包含其他成员。这些成员并不对应于显示的内容，但在某些情况下可能会很有用。

你系统上的 `utmp` 记录的结构可能与此不同。不过，你系统上的 `utmp.h` 文件将描述你系统中 `utmp` 数据的格式。结构体中字段名称在不同的 Unix 版本中通常是相同的，但标记为“compatibility”（兼容性）的行表明它们有时会变化。头文件通常有详细的注释，注释中包含了有用信息。

## 2.4.1 我们现在知道 who 是如何工作的

通过阅读关于 `who` 和 `utmp` 主题的在线手册，并阅读头文件 `/usr/include/utmp.h`，我们学会了 `who` 是如何工作的。`who` 从文件中读取结构体。文件中每个登录会话包含一个结构体。我们知道结构的具体布局。信息流如图 2.2 所示。

![](img/99837708330d437de319a559cfa6cda7_58_0.png)

图 2.2

`who` 命令的数据流。

该文件是一个数组，因此 `who` 必须读取记录并打印信息。最简单的逻辑就是逐个读取并打印它们。有那么简单吗？

我们还没有查看过某个版本 `who` 的源代码，但我们已经通过在线信息学习了关于该命令的一切。手册告诉我们该命令的功能，头文件显示了它使用的数据。

判断你是否真的理解了某事的唯一方法就是亲身尝试。

## 2.5 问题 3：我可以写 who 吗？

在本章的下一部分，我们将编写一个与 `who` 工作原理相同的程序。我们继续参考在线文档，并通过将程序的输出与系统中 `who` 版本的输出进行比较来测试我们的程序。我们目前对该程序的分析显示，我们需要编写两个任务：

- 从文件中读取结构体
- 显示存储在结构体的信息

### 2.5.1 问题：我如何从文件中读取结构体？

你使用 `getc` 和 `fgets` 从文件中读取字符和行。那么原始数据的结构体呢？我们可以使用 `getc` 逐字符读取结构体吗，但那听起来很琐碎。我们想要从磁盘读取完整的结构体。

# 让我们阅读手册吧！

我们想找到关于文件和读取的 `manpages`。`-k` 选项只接受一个关键词，所以我们选择其中一个关键词并尝试

```
$ -k file
```

看看会出现哪些主题。关于文件有很多主题。在我的系统中，`command` 命令只打印了 537 行。我们想在这 537 行中搜索包含“read”单词的行。名为 `grep` 的 Unix 命令可以打印包含特定模式的行。我们在管道中使用 `grep` 如下：

```
$ man -k file | grep read
-llseek(2) - 重新定位读/写文件偏移
filevent(n) - 当通道变为可读或可写时执行脚本
gftype(1) - 将通用字体文件转换为人类可读格式
lseek(2) - 重新定位读/写文件偏移
macsave(1) - 从标准输入读取 Mac 文件
read(2) - 从文件描述符读取
readprofile(1) - 读取内核分析信息的工具
scr_dump, scr_restore, scr_init, scr_set(3) - 从（到）文件读（写）curses 屏幕 - 从标准输入读取并写入标准输出和文件
```

此列表中最有前景的项目是 `read(2)`。其他的听起来都像其他主题。

查看第 2 部分关于 `read` 的手册页：

```
$ man 2 read
READ(2) 系统调用 READ(2)
```

```
NAME
read - 从文件描述符读取
SYNOPSIS
#include <unistd.h>
size_t read(int fd, void *buf, size_t count)
DESCRIPTION
read() 尝试从文件描述符 fd 读取多达 count 字节到位于 buf 处的缓冲区。
```

# 第2章：谁是第一个

如果 `count` 为 0，`read()` 返回 0 且没有其他结果。如果 `count` 大于 `SIZE_MAX`，结果是未定义的。

## 返回值

成功时，返回读取的字节数（0 表示文件结束），文件位置将移动该字节数。如果此数字小于请求的字节数，则不是错误；这可能是因为当前可用字节较少（可能我们接近文件末尾，或者我们是从管道或终端读取），或者因为 `read()` 被信号中断。出错时，返回 -1 并适当设置 `errno`。在这种情况下，文件位置是否改变是未定义的。

此系统调用允许我们从文件读取指定数量的字节到缓冲区中。我们想要使用 `sizeof(struct utmp)` 来指定要读取的字节数。此手册页说 `read` 从文件描述符读取。我们该如何获取其中一个？通过查看 `read` 手册页，我们找到了其中一个。

## 2.5 问题 3：我能写谁 吗？

`close` 系统关闭由文件描述符 `fd` 指定连接。`close()` 在出错时返回 -1。例如，尝试关闭一个未指向打开文件的文件描述符是一个错误。其他错误在手册中描述。

### 2.5.3 whool.c

我们快要完成了。我们已经了解了它的工作原理，并且拥有了所需的三个系统调用：连接文件、从文件中提取数据块、以及关闭文件。顶层代码看起来如下：

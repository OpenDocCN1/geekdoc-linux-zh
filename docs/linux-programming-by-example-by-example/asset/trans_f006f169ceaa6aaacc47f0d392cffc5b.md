

- LOG_PERROR—打印到标准错误（stderr）。
- LOG_PID—在每条消息中包含进程的 PID。

facility 指定发送消息的程序类型，可以是表 9.1 中列出的值之一。

### 表 9.1：系统日志记录器设施值

| 设施 | 描述 |
| :--- | :--- |
| LOG_AUTHPRIV | 安全/授权消息 |
| LOG_CRON | 时钟守护进程；cron 和 at |
| LOG_DAEMON | 其他系统守护进程 |
| LOG_KERN | 内核消息 |
| LOG_LOCAL[0-7] | 保留供本地使用 |
| LOG_LPR | 行打印机子系统 |
| LOG_MAIL | 邮件子系统 |
| LOG_NEWS | Usenet 新闻子系统 |
| LOG_SYSLOG | 由 syslogd 生成的消息 |
| LOG_USER | 默认值 |
| LOG_UUCP | UUCP 系统 |

priority 指定消息的重要性。其可能的值列于表 9.2。

### 表 9.2：系统日志记录器优先级值

| 优先级 | 描述 |
| :--- | :--- |
| LOG_EMERG | 系统不可用 |
| LOG_ALERT | 立即采取行动 |
| LOG_CRIT | 严重情况 |
| LOG_ERR | 错误情况 |
| LOG_WARNING | 警告情况 |
| LOG_NOTICE | 正常但重要的情况 |
| LOG_INFO | 信息性消息 |
| LOG_DEBUG | 调试消息 |

严格来说，使用 `openlog` 和 `closelog` 是可选的，因为 `syslog` 会在第一次被调用时自动打开日志文件。

## 示例

![](img/be588b36b489136ce784030a08a1d3d4_228_0.png)

以下程序是 `lpdated` 的重写版本，该程序使用系统日志记录器：

```c
/*
 *  lpdated.c  - 简单的时间戳守护进程
 */
#include <sys/types.h>
#include <sys/stat.h>
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <errno.h>
#include <unistd.h>
#include <time.h>
#include <string.h>
#include <syslog.h>

int main(void)
{
      pid_t pid, sid;

      int fd, len;
      time_t timebuf;

      /* Open the system log */
      openlog("lpdated", LOG_PID, LOG_DAEMON);

      pid = fork();
      if (pid < 0) {
            syslog(LOG_ERR, "%s\n", "fork");
            exit(EXIT_FAILURE);
      }
      if (pid > 0)
      /* In the parent, let's bail */
      exit(EXIT_SUCCESS);

      /* In the child . . . */
      /* First, start a new session */
      if ((sid = setsid()) < 0) {
            syslog(LOG_ERR, "%s\n", "setsid");
            exit(EXIT_FAILURE);
      }
      /* Next, make / the current directory */
      if((chdir("/")) < 0) {
            syslog(LOG_ERR, "%s\n", "chdir");
            exit(EXIT_FAILURE);
      }
      /* Reset the file mode */
      umask(0);

      /* Close stdin, etc. */
      close(STDIN_FILENO);
      close(STDOUT_FILENO);
      close(STDERR_FILENO);

      /* Finally, do our work */
      len = strlen(ctime(&timebuf));
      while(1) {
            char *buf = malloc(sizeof(char) * (len + 1));
            if(buf == NULL) {
                  exit(EXIT_FAILURE);
            }
            if((fd = open("/var/log/lpdated.log",
                  O_CREAT | O_WRONLY | O_APPEND, 0600)) < 0) {
                  syslog(LOG_ERR, "%s\n", "open");
                  exit(EXIT_FAILURE);
            }
            time(&timebuf);
            strncpy(buf, ctime(&timebuf), len + 1);
            write(fd, buf, len + 1);
            close(fd);
            sleep(60);
      }
      closelog();
      exit(EXIT_SUCCESS);
}
```

在添加了 `syslog` 的日志记录功能后，如果您尝试以普通用户身份执行程序，`lpdated` 将会向系统日志（在 Linux 系统上通常是 `/var/log/messages`）写入一条类似于以下内容的条目：

> Sep 14 21:12:04 hoser lpdated[8192]: open

此日志条目表明，在指定的日期和时间，在名为 `hoser` 的主机上，一个名为 `lpdated` 的进程（PID 为 8192）向系统日志中写入了文本 `open`。参考 `lpdated` 的源代码，您将能够看到错误发生的位置。

尽管时间戳本身仍会写入 `/var/log/lpdated.log`，但 `lpdated` 生成的所有错误消息都会记录到系统日志中。以下的输出取自系统日志，它是在非 root 用户尝试运行该程序时生成的。方括号中的数字是 `lpdated` 的 PID。

![](img/be588b36b489136ce784030a08a1d3d4_230_0.png)

## 输出

> Jul 28 11:34:06 hoser lpdated[8895]: open

## 接下来是什么？

本章讨论了创建*守护进程*，即始终在后台运行且通常提供某种服务的程序。这标志着本书对系统编程主题的介绍结束。凭借第一部分“Linux 编程环境”中涵盖的基本开发工具知识，以及对底层系统编程（在第二部分“系统编程”中涵盖）的扎实理解，您已准备好在第三部分“Linux API”中学习 Linux 最常用的一些 API，即应用程序编程接口。

# 第三部分—LINUX API（应用程序编程接口）

- 10 数据库 API
- 11 使用 ncurses 进行屏幕操作
- 12 高级 ncurses 编程
- 13 声音 API：OSS/Free
- 14 创建和使用编程库

# 10—数据库 API

应用程序员通常需要在不要求（或不想承担）像 Informix 或 Oracle 这样全功能关系数据库的所有服务（或开销）的情况下，将数据存储在数据库中。本章将教您如何使用 Berkeley 数据库，这是一个嵌入式数据库库，在主要的 Linux 发行版中都很常见。本章讨论的版本是 2.7.7，但讨论内容适用于任何 2.x 版本。请注意，2.x API 包含了 1.x API 的所有功能，但也添加了许多新元素。本章涵盖以下主题：

- 创建新数据库
- 打开现有数据库
- 添加和删除记录
- 检索记录
- 搜索记录
- 在数据库中移动
- 关闭数据库

> **注意**
> Berkeley 数据库 2.7.5 版本的完整源代码分发可在随书网站获取。本书中的所有示例均使用章节源代码目录中的头文件和库副本构建。

## Berkeley 数据库

Berkeley 数据库，通常称为 Berkeley DB 或简称 DB，使用键值对来处理数据库中的元素。键是标识元素；值是数据元素。要找到你想要的数据，向 DB 呈现一个键，DB 将返回与之关联的值。键值对存储在一个称为 DBT（一个数据库对象）的简单结构中，它由一个内存引用（即一个指针）和以字节为单位的内存引用长度组成。键和值可以是任何类型的数据。存储数据的长度实际上没有限制——单个键或值必须适合系统的可用内存（物理 RAM）。

例如，如果您想创建一本关于本书章节的数据库，键值对可能如下所示：

| 键 | 值 |
| :--- | :--- |
| One | 编译程序 |
| Two | 控制构建过程：GNU make |
| Three | 关于项目 |
| Four | 进程 |
| Five | 信号 |

DB 数据库支持三种存储和访问方法：B+树、哈希和记录。基于记录的数据库按顺序存储固定或可变长度的数据；新记录可以插入到现有记录之间，或追加到一系列现有记录的末尾。基于哈希的数据库将记录存储在哈希表中以进行快速搜索。哈希函数可以由程序员提供，也可以使用内置的默认例程。B+树数据库按排序顺序存储数据。排序顺序由程序员提供的函数或按字典顺序对键进行排序的默认函数确定。图 10.1 展示了这三种存储和访问方法之间的关系。

![](img/be588b36b489136ce784030a08a1d3d4_234_0.png)

**图 10.1**
记录在 Berkeley DB 数据库中的存储方式。

DB 支持的存储和访问方法的具体实现超出了本书的范围（事实上，许多计算机科学家将他们的整个职业生涯都致力于研究排序和搜索算法），但其基本原理很简单。图 10.1 假设数据库包含八条记录，用数字一到八表示。B+树数据库将数据存储在与图 10.1 所示类似的结构中，使得定位特定记录极其快速且高效。基于哈希的数据库将数据存储在表中。表中单个记录的位置取决于基于记录键计算得出的任意值。基于记录编号的数据库按顺序存储记录。它们通过其记录编号进行访问和操作。

## 创建、打开和关闭数据库

要使用 DB，请在源代码中包含 `<db.h>` 并链接 libdb。a (-ldb)。每个 DB 函数在成功时返回零，在任何失败时返回非零值。在发生系统错误（如非法参数或磁盘错误）时，DB 返回可用于 `perror` 函数的 `errno` 值。其他返回代码将在讨论生成它们的函数时进行说明。


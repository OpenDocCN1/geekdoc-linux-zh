
Linus Torvalds

## 参见

```
insert_file_free(9), put_file_last(9)
```

# 索引

# 符号

# A

- `*`（特殊参数）, 15

- `@`（bash 特殊参数）, 15

- `\`（bash 转义字符）, 14

- `$`（美元符号）bash 特殊参数, 15, 扩展, 19, ftp 命令, 148

- `*`（感叹号）bash 特殊参数, 15, ftp 命令, 148

- `*`（telnet）, 512

- `>`（大于）运算符, 21

- `-`（连字符）bash 特殊参数, 15

- `<`（小于）运算符, 21

- `*`（管道）,bash, 12

- `#`（井号）bash 注释, 14 bash 特殊参数, 15

- `*`（问号）bash 特殊参数, 15, ftp 命令, 152

- `*` telnet, 512

- `auth`, 591

- `*`（下划线）bash 特殊参数, 15

- `/`（目录）, 1236

- `0`,bash 特殊参数, 15

- 8859-1 字符集, 1064

- 8859-2 字符集, 1064

- 8859-3 字符集, 1064

- 8859-4 字符集, 1064

- 8859-5 字符集, 1065

- 8859-6 字符集, 1065

- 8859-7 字符集, 1065

- 8859-8 字符集, 1065

- 8859-9 字符集, 1065

- Abas 字节，转换为便位图, 731

- `abort()` 函数, 892

- `abs()` 函数, 892-893

- 绝对值, 892-893

- 浮点数, 919

- 长整数, 960-961

- `accept`, 740-741

- `access`, 741-742

- `errors`, 741

- 返回值, 741

- 访问控制文件更改权限, 61-65

- `hosts_access`, 1133-1136

- `diagnostics`, 1133

- `files`, 1133

- 运算符, 1133-1134

- `patterns`, 1133-1134

- 远程查找,1134-1135

- `rules`, 1135

- `shell` 命令, 1134

- 通配符, 1134

- 语言扩展, 1137-1139

- 内存, 804-805

- NTP站点, 1167-1168

- `account` (ftp 命令), 148

- `acct`, 742

- `alias()` 函数, 893

- `acos()` 函数, 893-894

- `active`, 1104-1105

- `active_time`, 1104-1105

- `add` (命令), 96

- `ADD_ADDRESS` 环境, 变量, 529

- `add_timer`, 1244

- `addgroup`, 1258-1259

- `addnment()` 函数, 935-936

- Internet, 操作, 953-954

- 地址, 1244

- 缩写, 1245

- 大小写敏感, 1245

- 兼容性, 1245

- postmasters

# kernel_mktime

`kernel_mktime`—将启动结构体 `mktime` 转换为自 1970年1月1日 00:00:00 以来过的秒数。

# 语法概要

```
linux/kernel/mktime.c
long kernel_mktime(struct mktime *time);
```

## 描述

此例程由 `time_init(void)`, `linux/init/main.c` 调用。`kernel_mktime()` 将 `struct mktime`（从 CMOS 初始化）转换为一个编码的行数。

# 转换方法

首先创建一个数组 `month[12]`，其中存储到达闰年特定月份时经过的秒数。接下来，它从当前年份减去 70，使 1970 年成为起始年。此之后就是数学魔法；请自行查看。如果你知道它为什么这样做，请发送电子邮件（参见 nroff 源码）。

# 返回值

返回一个 `long` 类型的编码时间。

# 文件

`linux/kernel/mktime.c` 该例程的所在地

## 注释

此例程仅在内核启动期间调用。

从历史上看，该值（编码的 long）计算自纪元（Epoch）以来的秒数，纪元发生于 1970年1月1日 00:00:00，被称为协调世界时 (UTC)。在旧版手册中，此事件被称为格林尼治标准标准时间 (GMT)。

# 警告

`kernel_mktime()` 不检查年份是否大于 1969。惯例是将板载时钟设置为 GMT，让请求时间的进程在必要时将其转换为本地时间。

# 限制

仅供内核使用。

## 作者

Linus Torvalds

0.99.10, 1998年7月5日

# proc_sel

`proc_sel`—通过准则选择进程。

# 语法概要

```
linux/kernel/sys.c
#include <linux/resource.h>
static int proc_sel(struct task_struct *p, int which, int who);
```

## 描述

在优先级的某些方面将任务 `p` 与提供的信息或当前任务进行比较。如果 `who` 为零，则比较任务 `p` 和当前任务。否则，`who` 和 `*p` 是用于比较的提供的信息。

## 选项

`which` 的有效值为：

- `PRIO_PROCESS`：比较进程 ID。这里有一个异常。如果 `who` 不为零且任务 `p` 是当前任务，则返回 True。

- `PRIO_PGRP`：比较组 ID。

- `PRIO_USER`：比较用户 ID。

# 返回值

返回真值 (0, 1)。

## 作者

Linus Torvalds

## 参见

`sys_setpriority(2)`, `sys_getpriority(2)`

> Linux 0.99.10, 1993年7月7日

# put_file_last

`put_file_last`—将文件移动到文件表的“末尾”。

# 语法概要

```
linux/fs/file_table.c
static void put_last_free(struct file *file);
```

## 描述

此函数从文件表中移除文件并再次插入到末尾。可以通过 `first_file->prev` 访问。

## 作者

Linus Torvalds

## 参见

`insert_file_free(9)`, `remove_file_free(9)`

# insert_file_free

`insert_file_free`—将文件条目插入文件表中。

## 描述

这个指针构成的噩梦通过 `file` 处的根指针将文件添加到文件表中。这是文件表管理的构建模块。

## 参见

1val, 1993年7月7日

# remove_file_free

`remove_file_free`—从链列表中移除表条目。

# 语法概要

```
linux/fs/file_table.c
static void remove_file_free(struct file *file);
```

## 描述

此例程从表中移除文件。这主要用于将文件移动到列表末尾。

## 作者

Linus Torvalds

## 参见

```
insert_file_free(9), put_file_last(9)
```

# 索引

# 符号

# A

- `*`（特殊参数）, 15

- `@`（bash 特殊参数）, 15

- `\`（bash 转义字符）, 14

- `$`（美元符号）bash 特殊参数, 15, 扩展, 19, ftp 命令, 148

- `*`（感叹号）bash 特殊参数, 15, ftp 命令, 148

- `*`（telnet）, 512

- `>`（大于）运算符, 21

- `-`（连字符）bash 特殊参数, 15

- `<`（小于）运算符, 21

- `*`（管道）,bash, 12

- `#`（井号）bash 注释, 14 bash 特殊参数, 15

- `*`（问号）bash 特殊参数, 15, ftp 命令, 152

- `*` telnet, 512

- `auth`, 591

- `*`（下划线）bash 特殊参数, 15

- `/`（目录）, 1236

- `0`,bash 特殊参数, 15

- 8859-1 字符集, 1064

- 8859-2 字符集, 1064

- 8859-3 字符集, 1064

- 8859-4 字符集, 1064

- 8859-5 字符集, 1065

- 8859-6 字符集, 1065

- 8859-7 字符集, 1065

- 8859-8 字符集, 1065

- 8859-9 字符集, 1065

- Abas 字节，转换为便位图, 731

- `abort()` 函数, 892

- `abs()` 函数, 892-893

- 绝对值, 892-893

- 浮点数, 919

- 长整数, 960-961

- `accept`, 740-741

- `access`, 741-742

- `errors`, 741


TCSADRAIN 更改在向 `fd` 关联的对象传输所有输出，以及在更改之前已接收但未读取的所有输入后发生。

TCSFLUSH `tsendbreak()` 发送持续特定时间的零位流，或者如果使用的是串行数据传输。如果有持续时间，它发送至少 0.25 秒且最多不超过 0.5 秒的零位。如果没有持续时间，它发送持续 N 秒的零位，其中 N 至少为 0.25 且最多不超过 .5。

如果终端没有使用异步串行数据传输，`tsendbreak()` 返回但不执行任何操作。

`tcrain()` 等待向 `fd` 关联的对象传输所有输出。

`tcflush()` 丢弃到 `fd` 关联的对象但未传输的数据，或接收但未读取的数据，取决于 `queue_selector` 的值。

TCIFLUSH 刷新未读取的数据。

TCOFLUSH 刷新未传输的数据。

TCIOFLUSH 刷新所有未读取的数据和未传输的数据。

`tcflow()` 暂停对 `fd` 关联对象的传输或接收，取决于 `action` 的值：

TCOOFF 暂停输出。

TCOON 重启暂停的输出。

TCIOOFF 发送 STOP 字符，停止终端传输到系统。

TCION 发送 START 字符，开始终端传输到系统。

`termios`, `tcgetattr`, `tcsetattr`, `tsendbreak`, `tcdrain`, `tcflush`, `tcflow`, `tcgetspeed`, `cfetspeed`, `cfetspeed`, `cfetspeed`, `tcgetpgrp`, `tcsetpgrp`

打开终端文件时的默认设置是其输入和输出都不会挂起。

波特率函数用于获取和设置输入及输出波特率的值，`termios` 中的新值在成功调用 `tcsetattr()` 之前不会生效。

将速度设置为 80 会导致调制解调器挂起。`B38400` 对应的实际比特率可能会通过 `setserial(8)` 更改。

输入和输出波特率存储在 `termios` 结构体中。

`cfgetspeed()` 返回存储在由 `termios_p` 指向的 `termios` 结构体中的输出波特率；

`cfetspeed()` 将由 `termios_p` 指向的 `termios` 结构体中的输出波特率设置为 `speed`，该 `speed` 必须是以下值之一：

```
B0
B50
B75
B110
B134
B150
B200
B300
B600
B1200
B1800
B2400
B4800
B9600
B19200
B38400
B57600
B115200
B230400
```

零波特率 `B0` 用于终止连接。如果指定了 `B0`，调制解调器控制线将不再断位。通常情况下，这将断开线路。`CBAUDEX` 是超出 POSIX.1 定义之外速度（57600 及以后）的掩码。`B57600 & CBAUDEX` 为非零。

`cfgetspeed()` 返回存储在 `termios` 结构体中的输入波特率。

`cfetspeed()` 设置存储在 `termios` 结构体中的输入波特率。如果输入波特率设置为 0，它将等于输出波特率。

`tcgetpgrp()` 返回前台处理组的进程组 ID，错误时返回 -1。

`tcsetpgrp()` 将进程组 ID 设置为 `tcpgid`，`pgid` 必须是同一会话中进程组的 ID。

## 返回值

`cfgetspeed()` 返回存储在 `termios` 结构体中的输入波特率。

`cfetspeed()` 返回存储在 `termios` 结构体中的输出波特率。

`tcgetpgrp()` 返回前台处理组的进程组 ID，错误时返回 -1。

所有其他函数返回：

- 0 表示成功。
- -1 表示失败（并设置 `errno` 以指示错误）。

## 第二部分：系统调用

## 参见

`setserial(8)`

Linux, 1995年2月25日

## time

`time`—获取以秒为单位的时间

### 概要

```
#include <time.h>
time_t time(time_t *t);
```

### 描述

`time` 返回自 1970 年 1 月 1 日 00:00:00 GMT 来的的时间，以秒为单位。

如果 `t` 为空，则返回值也会存储在 `t` 指向的内存中。

### 符合

SVID, AT&T, POSIX, X/OPEN, BSD 4.3

（在 BSD 4.3 下，此函数被 `gettimeofday(2)` 取代。）

### 参见

`ctime(3)`, `date(1)`, `ftime(3)`, `gettimeofday(2)`

Linux, 1993年7月24日

## times

`times`—获取进程时间

### 概要

```
#include <sys/time.h>
clock_t times(struct times *buf);
```

### 描述

`times` 将当前进程时间存储在 `buf` 中。

`struct tms` 定义在 `/usr/include/sys/time.h` 中：

```
struct tms {
    time_t tms_utime;    /* 用户时间 */
    time_t tms_stime;     /* 系统时间 */
    time_t tms_cutime;   /* 子进程用户时间 */
    time_t tms_ctime;    /* 子进程系统时间 */
};
```

`times` 返回自系统启动以来经过的时钟滴答数（ticks）。

### 符合

SVID, AT&T, POSIX, X/OPEN, BSD 4.3

### 参见

`time(1)`, `getrusage(2)`, `wait(2)`

Linux 0.99.11, 1993年7月24日

## truncate, ftruncate

`truncate`, `ftruncate`—将文件截达到指定的长度

### 概要

```
#include <unistd.h>
int truncate(const char *path, size_t length);
truncate(int fd, size_t length)
```

### 描述

`truncate` 将由 `path` 指定或由 `fd` 的文件截断为最多 `length` 字节。如果文件之前比此大，则额外的数据将丢失。使用 `truncate` 时，必须以写模式打开文件。

### 返回值

成功时返回 0。错误时返回 -1，并适当设置 `errno`。

### 错误

`truncate` 的错误包括：

- `ENOTDIR` 路径前缀组件不是目录。
- `EINVAL` 路径名包含高位位的字符。
- `NAMETOOLONG` 路径名组件超过 255 个字符，或整个路径名超过 1023 个字符。
- `ENOENT` 指定的文件不存在。
- `EACCES` 路径前缀组件的搜索权限被拒绝。
- `EACCES` 指定的文件对用户不可写。
- `ELOOP` 路径名中遇到过多符号链接。
- `EISDIR` 文件是一个目录。
- `EROFS` 文件位于只读文件系统上。
- `ETXYS` 正在执行的（共享文本）文件（此处可能有误）。
- `EIO` 更新 `inode` 时 I/O 错误。
- `EFAULT` `path` 指向进程分配空间之外。

`truncate` 的错误包括：

- `EBADfd` 不是有效的描述符。
- `EINVAL` 引用的是套接字而非文件。
- `EINVAL` 未以写模式打开。

### 历史

这些函数出现在 BSD 4.2 中。

### BUG

这些调用应该泛化，以允许丢弃文件范围字节。

### 参见

`open(2)` BSD 手页, 1993年7月24日

## umask

`umask`—设置文件创建掩码

### 概要

```
#include <sys/stat.h>
int umask(int mask);
```

### 描述

`umask` 将 `umask` 设置为 0777。

### 返回值

返回掩码的上一个值。

### 符合

SVID, AT&T, POSIX, X/OPEN, BSD 4.3

### 参见

`creat(2)`, `open(2)` Linux 1993年7月24日

## uname

`uname`—获取当前内核的名称和信息

### 概要

```
#include <utname.h>
int uname(struct utname *buf);
```

### 描述

`uname` 在 `buf` 中返回系统信息。`utname` 结构体定义在 `/usr/include/utname.h` 中：

```
struct utname {
    char system[65];
    char nodename[65];
    char release[65];
    char version[65];
    char machine[65];
    char domainname[65];
};
```

### 返回值

成功时返回 0。错误时返回 -1，并适当设置 `errno`。

### 错误

`EFAULT` `buf` 无效。

### 符合

SVID, AT&T, POSIX, X/OPEN

### 参见

`uname(1)`, `gethostname(2)` Linux 1995年2月25日

## none

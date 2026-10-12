
```
$ fdformat /dev/fd0
Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.
Formatting... done
Verifying... done

$ su
Password:
# mount -t ext2 -o mand /dev/fd0 /mnt/floppy
# suspend

[1]+ Stopped su

$ ch14-lockall /mnt/floppy/x &
[2] 23311

$ ls -l /mnt/floppy/x
-rw-r-Sr-- 1 arnold devel 13 Apr 6 14:23 /mnt/floppy/x

$ echo something > /mnt/floppy/x
bash: /mnt/floppy/x: Resource temporarily unavailable

$ kill %2
[2]- Terminated ch14-lockall /mnt/floppy/x

$ echo something > /mnt/floppy/x

$ fg
su
# umount /mnt/floppy
# exit
$ 
```

![](img/766b5597246d532412fad21b1c59ccec_575_0.png)

只要 `ch14-lockall` 正在运行，它就持有锁。由于这是强制锁，shell 的 I/O 重定向会失败。一旦 `ch14-lockall` 退出，锁就被释放，I/O 重定向就会成功。如前所述，在 `GNU/Linux` 下，即使是 `root` 用户也无法绕过强制文件锁。

附带一提，软盘是学习如何使用操作系统文件系统工具的绝佳测试平台。如果你对软盘做了一些破坏数据的事情，很可能不会造成灾难性的后果，而在常规硬盘的活动分区上进行实验则风险大得多。

#### 14.3 更精确的时间

`time()` 系统调用和 `time_t` 类型以自纪元（Epoch）以来的秒数表示时间。一秒的分辨率确实不够；当今的机器速度很快，区分亚秒级时间间隔通常很有用。从 `4.2 BSD` 开始，Berkeley Unix 引入了一系列系统调用，使得获取和使用亚秒级时间成为可能。这些调用在所有现代 Unix 系统上都可用，包括 `GNU/Linux`。

##### 14.3.1 微秒级时间：`gettimeofday()`

第一个任务是获取当前时间：

```c
#include <sys/time.h>
```

```c
int gettimeofday(struct timeval *tv, void *tz);
```

`gettimeofday()` 获取当前时间。<sup>5</sup> 成功时返回 0，出错时返回 -1。参数如下：

- `struct timeval *tv`：此参数是一个指向 `struct timeval` 的指针，稍后描述，系统将把当前时间存入其中。

- `void *tz`：此参数不再使用；因此，它的类型是 `void *`，你应该始终传入 `NULL`。（man 手册页描述了它过去的作用，随后指出它已废弃。如果你对细节感兴趣，可以阅读它。）

时间由 `struct timeval` 结构体表示：

```c
struct timeval {
    long tv_sec;     /* seconds */
    long tv_usec;    /* microseconds */
};
```

`tv_sec` 值表示自纪元以来的秒数；`tv_usec` 是那一秒内的微秒数。

`GNU/Linux` 的 `gettimeofday(2)` man 手册页还记录了以下宏：

```c
#define timerisset(tvp) ((tvp)->tv_sec || (tvp)->tv_usec)

#define timercmp(tvp, uvp, cmp) \
    ((tvp)->tv_sec cmp (uvp)->tv_sec || \
    (tvp)->tv_sec == (uvp)->tv_sec && \
    (tvp)->tv_usec cmp (uvp)->tv_usec)

#define timerlear(tvp) ((tvp)->tv_sec = (tvp)->tv_usec = 0)
```

这些宏作用于 `struct timeval *` 值；也就是说，它们作用于结构体指针，其用途从名称和代码中都应该很显而易见。`timercmp()` 宏特别有趣：第三个参数是一个比较运算符，用于指示比较的类型。例如，考虑确定一个 `struct timeval` 是否小于另一个：

```c
struct timeval t1, t2;
...
if (timercmp(& t1, & t2, <))
/* t1 is less than t2 */
```

该宏展开为：

```c
((& t1)->tv_sec < (& t2)->tv_sec || \
(& t1)->tv_sec == (& t2)->tv_sec && \
(& t1)->tv_usec < (& t2)->tv_usec)
```

这意味着“如果 `t1.tv_sec` 小于 `t2.tv_sec`，或者如果它们相等且 `t1.tv_usec` 小于 `t2.tv_usec`，那么……”

> <sup>5</sup> `gettimeofday(2)` man 手册页记录了对应的 `settimeofday()` 函数，供超级用户（`root`）使用，以设置整个系统的时间。

##### 14.3.2 微秒级文件时间：`utimes()`

第 5.5.3 节“更改时间戳：`utime()`”，第 157 页，描述了用于设置给定文件的访问时间和修改时间的 `utime()` 系统调用。某些文件系统以微秒（或更高）分辨率存储这些时间。此类系统提供 `utimes()` 系统调用（注意名称末尾的 s），用于以微秒值设置访问和修改时间：

```c
#include <sys/time.h>

int utimes(char *filename, struct timeval tvp[2]);
```

`tvp` 参数应指向一个包含两个 `struct timeval` 结构体的数组；这些值分别用于访问时间和修改时间。如果 `tvp` 是 `NULL`，则系统使用当前时间。

POSIX 将此标记为“遗留”（legacy）函数，意味着它标准化只是为了支持旧代码，不应在新应用程序中使用。主要原因似乎是没有定义包含微秒值的接口来获取文件的访问和修改时间；`struct stat` 仅包含 `time_t` 值，而不是 `struct timeval` 值。

然而，如第 5.4.3 节“仅限 Linux：指定更高精度的文件时间”，第 143 页所述，`Linux 2.6`（及更高版本）确实通过 `stat()` 调用提供了纳秒级分辨率时间戳的访问权限。其他一些系统（如 `Solaris`）也是如此。<sup>6</sup> 因此，`utimes()` 比初看时更有用，尽管它正式的“遗留”地位，在你的程序中使用它没有任何理由回避。

> <sup>6</sup> 不幸的是，似乎目前没有关于 `struct stat` 成员名称的标准，使其成为一种不可移植的操作。

##### 14.3.3 间隔定时器：`setitimer()` 和 `getitimer()`

`alarm()` 函数（参见第 10.8.1 节“闹钟：`sleep()`、`alarm()` 和 SIGALRM”，第 382 页）安排在给定的秒数过去后发送 SIGALRM。其最小分辨率为 1 秒。这里，`4.2 BSD` 也引入了一个函数和三个接受亚秒级时间的不同定时器。

*内部定时器*（internal timer）就像一个重复的闹钟。你设置它第一次“响起”的时间，以及之后定时器重复的频率。这两个值都使用 `struct timeval` 对象；也就是说，它们（潜在地）具有微秒分辨率。定时器“响起”是通过递送信号实现的；因此，你需要为定时器安装信号处理程序，最好在设置定时器之前完成。

存在三种不同的定时器，如表 14.2 所述。

#### 表 14.2 间隔定时器

| 定时器 | 信号 | 功能 |
| :--- | :--- | :--- |
| `ITIMER_REAL` | SIGALRM | 在实时中运行。 |
| `ITIMER_VIRTUAL` | SIGVTALRM | 当进程在用户模式下执行时运行。 |
| `ITIMER_PROF` | SIGPROF | 当进程在用户模式或系统模式下时运行。 |

第一个定时器 `ITIMER_REAL` 的使用很直接。定时器在实时中倒计时，在给定时间过去后发送 SIGALRM。（因为发送了 SIGALRM，你不能将 `setitimer()` 调用与 `alarm()` 调用混合使用，将它们与 `sleep()` 调用混合使用也很危险；参见第 10.8.1 节“闹钟：`sleep()`、`alarm()` 和 SIGALRM”，第 382 页。）

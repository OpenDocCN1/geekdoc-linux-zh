
我们在 `getopt` `switch` 语句中的最后一个短语控制每秒比特数；我们没有在这里包含一个大型的嵌套 `switch` 语句，而是调用了已经描述过的 `symbolic_speed()` 来获取一个 `termios` 能理解的 `speed_t` 值，如第 228 行所示。

```c
/* 除非指定了 -b，否则不修改 speed */
if (speed) {
    cfsetspeed(pts, symbolic_speed(speed));
    cfsetspeed(pts, symbolic_speed(speed));
}
```

在确定了实际速度并获得了代表它的 `speedy` 值后，我们需要将该速度放入串口的 `termios` 结构中。由于 `termios` 结构支持具有不同输入和输出速度的异步设备，我们在这里需要将两者都设置为相同的值。

在将我们在 `termios` 结构副本中的更改提交到设备之前，我们在第 236 行为重要的信号注册了信号处理程序，否则这些信号可能会杀死我们，导致 tty 停留在它们的原始状态。关于信号处理程序的更多信息，请参阅第 13 章。

```c
sact.sa_handler = cleanup_termios;
sigaction(SIGHUP, &sact, NULL);
sigaction(SIGINT, &sact, NULL);
sigaction(SIGPIPE, &sact, NULL);
sigaction(SIGTERM, &sact, NULL);
```

一旦信号处理程序能够在 `robin` 被杀死时恢复旧的 `termios` 设置，我们就可以安全地应用新的 `termios` 设置。

```c
tcsetattr(pr, TCSANOW, &pts);
tcsetattr(pr, TCSANOW, &pts);
```

## 15.4 调试

调试 tty 代码并不总是容易的。选项在含义上重叠，并以各种方式相互影响，往往以你无意间的方式发生。但你仅通过调试器无法容易看到发生了什么，因为你试图管理的处理是在内核中发生的。

调试通过串口通信代码的一种有效方法是使用 `script` 程序。在开发 `robin` 期间，我们用串口线连接了两台计算机，并通过运行运行良好的 `kermit` 程序验证了连接的有效性。在本地计算机上运行 `kermit` 的同时，我们在远程计算机上运行 `script` 程序，它开始记录 `typescript` 中的所有字符。然后我们退出 `kermit` 在本地计算机上运行 `script`，在本地计算机的当前目录下放置一个 `typescript` 文件。我们尝试在 `script` 下运行 `robin`，并在运行后比较两端的 `typescript` 文件以查看字符的差异。由此，我们破解了所选处理选项的效果。

另一种调试方法利用了 `stty` 程序。如果你在测试程序时，认为识别出了 `termios` 设置中的错误，可以使用 `stty` 程序立即进行更改，而无需先重新编译你的程序。如果你在 `/dev/cua0` 上工作，并想设置 `ECHOIL` 标志，只需运行命令：

```
stty echoctl < /dev/cua0
```

在你的程序运行时即可。

同样，你可以通过 `stty -a < /dev/cua0` 查看你正在使用的端口的当前状态。

之前解释过的，很难用同一个 tty 来运行调试器和运行你正在调试的 tty 篡改程序。相反，你需要附加到进程上。这并不困难。在一个 X 终端会话中（在 X 下操作，这样你就可以同时看到两个 tty），运行你想调试的程序。如果需要，在你想附加的地方放置一个长时间的 `sleep()`。

# 第 15 章 终端与伪终端

```
$ ./robin -b 38400 /dev/cual
```

现在，从另一个 X 终端会话中，通过两种方法之一找到你正尝试调试的程序的 `pid`：

```
$ ps | grep robin
30483 ? S 0:00 /robin -b 38400 /dev/tty
30485 ? S 0:00 grep robin
$ pidof robin
30483
```

`pidof` 更方便，但可能在每个系统上都可用。记住你找到的数字（这里是 30483），并像往常一样启动调试会话。

```
$ gdb robin 30483
GDB is free software...
...
Attaching to program '.../robin', process 30483
Reading symbols from ...
0x40075d88 in sigsuspend ()
```

从这一点开始，你可以设置断点和观察点、单步执行程序或进行任何你喜欢的操作。

## 15.5 termios 参考

`termios` 接口由一个结构体、一组操作该结构体的函数以及许多可以单独设置的标志组成。

### 15.5 termios 参考

```c
#include <termios.h>

struct termios {
    tcflag_t c_iflag;   /* 输入模式标志 */
    tcflag_t c_oflag;   /* 输出模式标志 */
    tcflag_t c_cflag;   /* 控制模式标志 */
    tcflag_t c_lflag;   /* 本地模式标志 */
    cc_t c_line;        /* 行规律 **/
    cc_t c_cc[NCCS];    /* 控制字符 */
};
```

`c_line` 成员仅用于超出本书范围的非常特定的系统应用程序。然而，其他五个成员在几乎所有需要操作终端设置的情况下都是相关的。

### 15.5.1 函数

`termios` 接口定义了若干几个函数，它们均在 `<termios.h>` 中声明。其中四个是用于以移植方式操作 `struct termios` 结构体的便利函数；其余的是系统调用。以 `c` 开头的函数是便利函数；以 `tc` 开头的函数是终端控制系统调用。所有的终端控制系统调用在进程当前于后台运行并尝试操作其控制终端时，都会生成 `SIGTTOU` 信号（见第 14 章）。

另有说明外，这些函数返回 0 表示成功，返回 -1 表示失败。你可能用于终端控制的函数调用有：

```c
int tcgetattr(int fd, struct termios *t);
```

获取文件描述符 `fd` 的当前设置并将其放入 `t` 指向的结构体中。

```c
int tcsetattr(int fd, int options, struct termios *t);
```

将文件描述符 `fd` 的当前终端设置设置为 `t` 中指定的设置。始终使用 `tcgetattr()` 来填充 `t`，然后对其进行修改。永远不要手动填充 `t`：某些系统要求设置或清除 POSIX 指定标志之外的标志

- 6. 例如设置与 tty 设备通信的网络协议。

通过手动填充 `t` 是不可移植的。

`options` 参数决定了更改何时生效。

`TCSANOW` 更改立即生效。

`TCSADRAIN` 在所有已写入 `fd` 的输出传输完成后更改生效；它在生效前会清空队列。通常在更改输出参数时应使用此项。

`TCSAFLUSH` 在输出队列清空后更改生效；在更改生效前丢弃（刷新）输入队列。

如果系统无法处理某些设置（例如数据速率），则允许静默忽略这些设置而不返回任何错误。查看设置是否被接受的唯一方法是使用 `tcgetattr()` 并比较返回的结构体内容与你传递给 `tcsetattr()` 的内容。

因此，大多数可移植应用程序使用如下代码：

```c
#include <termios.h>

struct termios save;
struct termios set;
struct termios new;
int fd;
...
tcgetattr(fd, &save);
set = save;
cfsetpeed(&set, B2400);
cfsetpeed(&set, B2400);
tcsetattr(fd, &set);
tcgetattr(fd, &new);
if ((cfgetpeed(&set) != B2400) || (cfgetpeed(&set) != B2400)) {
    /* 报错 */
}
```

### 15.5 termios 参考

注意，你并不在乎 `termios` 设置是否生效，忽略该条件是可以的，就像在 `robin` 中一样。

```c
speed_t cfgetpeed(struct termios *t);
speed_t cfgetispeed(struct termios *t);
```

分别从 `t` 获取输出或输入速率。这些函数返回符号速率，与给 `cfsetspeed()` 和 `cfgetispeed()` 接收的相同。

```c
int cfsetspeed(struct termios *t, speed_t speed);
int cfgetispeed(struct termios *t, speed_t speed);
```

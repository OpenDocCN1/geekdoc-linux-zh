
这通常被称为 *原始* 模式，意味着不进行特殊的输入或输出处理，字符可以立即被读取，而无需等待一行文本的组装完成。没有单一的标志位可以设置原始模式；相反，你必须逐一设置各项属性。（*stty* 命令确实有一个 raw 选项。）

我们希望的原始终端 I/O 具有以下属性，尽管没有严格的定义，你可能需要根据自己的用途稍作调整：

- *精确的输入。* 清除 ICANON，并设置 IMIN 和 TIME。
- *无字符映射。* 清除 OPOST 以关闭输出处理。对于输入，清除 INLCR 和 ICRNL。将字符大小设置为 CS8。清除 ISTRIP 以获取全部八位，清除 INPCK 和 PARENB 以关闭奇偶校验。清除 IEXTEN 以关闭扩展字符处理。
- *无流控。* 清除 IXON。
- *无控制字符。* 清除 BRKINT 和 ISIG，并将所有控制字符设置为禁用值，即使那些是特定于实现定义的。
- *无回显。* 清除 ECHO。

这些操作被封装在函数 `tc_setraw` 中。请注意，它保存了旧的 *termios* 结构以备 `tc_restore` 使用（见前文）。

```c
bool tc_setraw(void)
{
    struct termios tbuf;
    long disable;
    int i;

#ifdef _POSIX_VDISABLE
    disable = _POSIX_VDISABLE;
#else
    /* treat undefined as error with errno = 0 */
    ec_neg1( errno = 0, disable = fpathconf (STDIN_FILENO, _PC_VDISABLE));
#endif

    ec_neg1( tcgetattr(STDIN_FILENO, &tbuf));
    have_attr = true;
    tbufsave = tbuf;
    tbuf.c_cflag &= ~(CSIZE | PARENB);
    tbuf.c_cflag |= CS8;
    tbuf.c_iflag &= ~(INLCR | ICRNL | ISTRIP | INPCK | IXON | BRKINT);
    tbuf.c_oflag &= ~OPOST;
    tbuf.c_lflag &= ~(ICANON | ISIG | IEXTEN | ECHO);
    for (i = 0; i < NCCS; i++)
        tbuf.c_cc[i] = (cc_t)disable;
    tbuf.c_cc[VMIN] = 5;
    tbuf.c_cc[VTIME] = 2;
    ec_neg1( tcsetattr(STDIN_FILENO, TCSAFLUSH, &tbuf) );
    return true;
    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}
```

下面是一个使用 `stty` 命令显示终端设置的 `tc_setraw` 测试程序：

```c
setbuf(stdout, NULL);
printf("Initial attributes:\n");
system("stty | fold -s -w 60");
printf("\r\nRaw attributes:\n");
tc_setraw();
system("stty | fold -s -w 60");
tc_restore();
printf("\r\nRestored attributes:\n");
system("stty | fold -s -w 60");
```

以下是我得到的输出（在 Solaris 上）。请注意，`tc_setraw` 关闭了所有 `c_cc` 字符，而不仅仅是我们所知道的标准字符。但是，它并没有关闭所有可能使终端变为非原始模式的标志，例如 `imaxbel`<sup>8</sup> 你可能会发现，对于你移植代码的每个系统，都必须调整你版本的 `tc_setraw`，或者使用 Curses 库（第 4.8 节），该库有自己将终端设置为原始模式的方法。

初始属性：  
速度 38400 波特；evenp  
行数 = 40；列数 = 110；xpixels = 0；ypixels = 0；  
swtch = <undef>；  
brkint -inpck icrnl -ixany imaxbel onlcr  
echo echoe echoct echoctl echoke iexten

原始属性：  
速度 38400 波特；-parity  
行数 = 40；列数 = 110；xpixels = 0；ypixels = 0；  
min = 5；time = 2；  
intr = <undef>；quit = <undef>；erase = <undef>；kill = <undef>；  
eof = ^e；eol = ^b；swtch = <undef>；start = <undef>；  
stop = <undef>；susp = <undef>；dasup = <undef>；  
rprnt = <undef>；flush = <undef>；werase = <undef>；lnext = <undef>；  
-inpck -istrip -ixon ixonb -opost  
-isig -icanon -echo echoe echokl echoctl echoke

恢复后的属性：  
速度 96400 波特；evenp  
行数 = 40；列数 = 110；xpixels = 0；ypixels = 0；  
swtch = <undef>；  
brkint -inpck icrnl -ixany imaxbel onlcr  
echo echoe echok echoctl echoke iexten

有时在调试过程中（甚至调试后！），一个已将终端置于原始模式的程序在能够恢复原始设置之前就会中止。用户有时认为计算机崩溃了，或者他们的终端“死机”了——他们甚至无法使用 EOF 来注销。但是，可以从原始模式恢复。首先，回想一下 ICRNL 已被清除；这意味着你必须使用 Ctrl-j 而不是回车键来结束输入行。<sup>9</sup> 其次，因为 ECHO 也关闭了，你将看不到你输入的内容。首先输入几个换行符；你应该会看到一系列 shell 提示符，但不会出现在左边界处，因为输出处理（OPOST）已关闭。然后输入 `stty sane`，接着输入一个换行符，一切应该就恢复正常了。

## 4.6 额外的终端控制系统调用

如我们在第 4.5.1 节中看到的那样，当你使用 `tcsetattr` 设置终端属性时，你可以使用 `TCSADRAIN` 操作来排空（等待）输出队列，在属性设置之前完成，并且你还可以使用 `TCSAFLUSH` 操作额外刷新（丢弃）输入队列中的任何字符。两个系统调用允许你单独控制排空和刷新，而无需同时设置属性：

**tcdrain** — 排空（等待）终端输出

```c
#include <termios.h>

int tcdrain(
    int fd            /* file descriptor */
);
/* Returns 0 on success or -1 on error (sets errno). */
```

**tcflush** — 刷新（丢弃）终端输出、输入或两者

```c
#include <termios.h>

int tcflush(
    int fd,          /* file descriptor */
    int queue        /* queue to be affected */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

这些函数作用于队列——即，从终端接收但尚未被任何进程读取的字符，或由进程写入但尚未传输到终端的字符。

`tcflush` 的第二个参数（*queue*）是以下之一：

- **TCIFLUSH** 刷新输入队列。
- **TCOFLUSH** 刷新输出队列。
- **TCIOFLUSH** 刷新两个队列。

因此，`tcsetattr` 的 `TCSADRAIN` 参数相当于在属性设置之前调用 `tcdrain`，而 `tcsetattr` 的 `TCSAFLUSH` 参数相当于调用 `tcdrain` 和 `tcflush`，其中队列参数为 `TCIFLUSH`。

下一个系统调用 `tcflow` 允许应用程序暂停或重启终端输入或输出：

**tcflow** — 暂停或重启终端输入或输出的流

```c
#include <termios.h>

int tcflow(
    int fd,          /* file descriptor */
    int action       /* direction and suspend/restart */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

*action* 参数是以下之一：

- **TCOOFF** 暂停输出。
- **TCOON** 重启已暂停的输出。
- **TCIOFF** 发送 STOP 字符，旨在使终端暂停输入。
- **TCION** 发送 START 字符，旨在使终端重启已暂停的输入。

应用程序可以使用 *TCOOF* 来在写入终端的每页之后暂停输出，以便用户在通过键盘输入 START 字符继续之前阅读（默认是 Ctrl-q，见第 4.5.7 节）。在调用 *tcflow* 并使用 *TCOOF* 后，应用程序可以继续写入输出页；当终端的队列已满时，下一个 *write* 操作将被阻塞，直到队列稍微排空。

然而，这不是用户期望的行为，也不是逐页显示应用程序通常的工作方式。像 *more* 和 *man* 这样的命令会输出一页，然后提示用户输入一个普通字符（例如空格或回车）以获取下一页。内部地，此类应用程序输出一页，输出提示符，并阻塞在 *read* 上（通常是在关闭标准输入和回显的情况下），等待用户输入继续字符。

在输入端，*TCIOFF* 和 *TCION* 历史上用于防止终端溢出输入队列，但如今这完全由驱动器和/或硬件处理。如今，*tcflow* 可能仅用于专用设备，而不是实际的终端。

同一类别的还有 *tcsendbreak*，它向终端发送断字符：

**tcsendbreak** — 向终端发送断字符

```c
#include <termios.h>

int tcsendbreak(
    int fd,            /* file descriptor */
    int duration       /* duration of break */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

“断字符”是发送到终端的一段时间内的 0 位流，通常作为将终端置于特殊“注意”模式的一种方式。

如果 *duration* 参数为 0，则持续时间在四分之一到二分之一秒之间。如果非零，其含义取决于具体实现。不过，不要担心可移植性——你很可能没有机会向终端发送断字符。

9. Shell 的一个很好的增强功能是，它除了换行符外，还应接受回车符作为行结束符。（该脚注首次出现在 1985 年——迄今尚无进展。）

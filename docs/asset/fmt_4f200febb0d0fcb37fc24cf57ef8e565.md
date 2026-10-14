
Control-j 是真实的换行符。

# CR

CR 是回车符（carriage return）。该字符会被传递给读取进程。在规范模式（设置了 `ICANON` 标志）且设置了 `ICRNL`（输入时将 CR 映射为 NL）标志（默认值）的情况下，该字符在传递给读取进程之前会首先转换为换行符（ASCII 十进制 10，`^J`）。如果设置了 `IGCR`（忽略 CR）标志，则该字符在输入时会被忽略（以防必须使用真正的换行符来终止输入行的情况）。输出一个 CR 字符会导致终端将光标移动到行首。

# DISCARD

DISCARD 是丢弃输出字符（discard）。虽然该字符定义在 `cc` 数组中，但它对 Linux 无影响。在某些其他 UNIX 实现中，输入此字符会导致程序的输出被丢弃。该字符是一个切换控制位——再次输入一次即可恢复输出的显示。这在程序产生大量输出而我们想要跳过部分输出时非常有用（这在传统的终端上有用得多，因为那时的行传输速度较慢，且没有其他“终端窗口”）。该字符不会被传递给读取进程。

# EOF

EOF 是标准的文件结束符（通常是 Control-D）。在行开头输入此字符会导致来自终端的读取进程（即 `read()`）检测到文件结束符。如果该字符不是行中的第一个字符，则该字符会导致 `read()` 立即完成，并返回该行中目前为止已输入的字符。在这两种情况下，EOF 字符都不会被传递给读取进程。

# EOL and EOF2

EOL 和 EOF2 是额外的行终止符，它们在规范模式下的作用与标准换行符（NL）字符相似，用于终止输入行并使其对读取进程可用。默认情况下，这些字符是未定义的。如果定义了它们，它们会被传递给读取进程。只有在设置了 `IXTEN`（扩展输入处理）标志（默认值）时，EOL 字符才会生效。

这些字符很少被使用。使用它们的一个应用场景是 telnet。通过将 EOL 或 EOF2 设置为 telnet 转义字符（通常是 Control-J），或者地设置为波浪号字符 `~`（如果在登录模式下运行），telnet 能够立即捕获到该字符，即使在规范模式下读取输入也是如此。

# ERASE

在规范模式下，输入 ERASE 字符会删除当前行中之前输入的字符。被删除的字符和 ERASE 字符本身都不会被传递给读取进程。

# INTR

INTR 是中断字符（interrupt）。如果设置了 `ISIG`（启用信号）标志（默认值），输入此字符会导致向终端的前台进程组发送中断信号（`SIGINT`）（见第 34.2 节）。INTR 字符本身不会被传递给读取进程。

# KILL

KILL 是删行字符（也称为 kill line）。在规范模式下

...

# LNEXT

LNEXT 是字面字符（literal character）。在某些情况下，我们可能希望将终端的一个特殊字符视为普通字符以输入到读取进程。输入下一个字符（通常是 Control-V）会导致下一个字符被视为字面量，从而避免终端驱动程序通常会对该字符进行的任何特殊解释。因此，我们可以输入 `Control-V Control-C` 这两个字符的序列，提供一个真实的 Control-C 字符（ASCII 3）作为读取进程的输入。LNEXT 字符本身不会被传递给读取进程。该字符仅在设置了 `IXTEN`（扩展输入处理）标志（默认值）的规范模式下被解释。

# NL

NL 是换行符（newline）。在规范模式下，该字符会终止输入行。NL 字符本身包含在返回给读取进程的行中。（在规范模式下，CR 通常会被转换为 NL）。输出一个 NL 会导致终端将光标向下移动一行。如果设置了 `OPOST` 和 `ONLCR`（将 NL 映射为 CR-NL）标志（默认值），则在输出时，换行符会被映射为 CR-NL。`ICRNL` 和 `ONLCR` 标志的组合意味着输入会被转换为 NL，然后作为 CR 加 NL。

# QUIT

如果设置了 `ISQUIT` 标志（默认值），输入 QUIT 字符会导致向终端的前台进程组发送退出信号（`SIGQUIT`）（见第 34.2 节）。QUIT 字符本身不会被传递给读取进程。

# REPRINT

REPRINT 是重打印输入字符（reprint）。在规范模式并设置了 `ITEXT` 标志（默认值）的情况下，输入此字符会导致终端重新显示当前尚未输入的行。如果其他程序写乱了终端显示，这非常有用。REPRINT 字符本身不会被传递给读取进程。

# START AND STOP

START 和 STOP 是启动输出和停止输出字符，当启用了 `IXON`（启动输出控制）标志（默认值）时生效。某些终端模拟器不支持 START 和 STOP 字符。输入 STOP 字符会停止终端输出。STOP 字符本身不会被传递给读取进程。如果设置了 `IXOFF` 且终端输入队列已满，终端驱动会自动发送 STOP 字符以限制输入。输入 START 字符会在之前被 STOP 字符停止后恢复输出。START 字符本身不会被传递给读取进程。`XOFF`（启用停止输入控制）标志设置后（此标志默认禁用），一旦空间可用，终端驱动会自动生成 START 字符。如果设置了 `IXON` 标志，任何字符（而不只是 START）都可以用来重启输出。START 和 STOP 字符用于计算机与终端设备之间的软件流控。

# SUSP

SUSP 是挂起字符（suspend）。如果设置了 `ISIG` 标志（默认值），输入此字符会导致向终端的前台进程组发送挂起信号（`SIGTSTP`）（见第 34.2 节）。SUSP 字符本身不会被传递给读取进程。

# WERASE

WERASE 是词删除字符（word erase）。在规范模式下，设置了 `IXEN` 标志（默认值）时，输入此字符会删除到词开头的所有字符。词被认为是字母、数字和下划线的序列。（在某些 UNIX 实现中，词被视为空格分隔。）

# 其他终端特殊字符

其他 UNIX 实现在表 62-1 中列出的字符外还提供了终端特殊字符。

BSD 提供了 DSUSP 和 STATUS 字符。DSUSP 字符（通常是 Control-Y）的操作方式与 SUSP 字符类似，仅当它尝试读取该字符时（即在读取之前的输入后）才挂起进程组。STATUS 字符会导致内核在终端上显示信息（包括其消耗的 CPU 时间），并向前台进程组发送 `SIGINFO` 信号。如果需要，进程可以捕获此信号并显示更多状态

信息。（Linux 提供了形式上类似的功能，即魔法 SysRq 键；详细信息请参阅内核源码文件 `Documentation/sysrq.txt`。）

System V 衍生版本使用 SWT 字符。该字符用于在 shell 层之间切换 shell，这是 System V 作控制（job control）的前身。

## 示例程序

列表 62-1 显示了如何使用 `tcgetattr()` 和 `tcsetattr()` 来终止中断字符。该程序将中断字符设置为程序命令行参数提供的数值值对应的字符；或者在未提供命令行参数时禁用中断字符。

接下来的这个 shell 会话演示了该程序的使用。我们首先将中断字符设置为 Control-L (ASCII 12)，然后用 `stty` 验证该更改：

```
$ /new_intr 12

$ stty

speed 38400 baud, line = 0;

intr = ^L;
```

然后我们启动了一个运行 `sleep(1)` 的进程。我们发现，输入 Control-C 不再具有其通常的终止进程的作用，但输入 Control-L 确实可以终止进程。

```
$ sleep 10

^C

Type Control-L to terminate $
```

Control-C 无影响；它被回显了

我们现在显示 shell 变量 `$?` 的值，它显示上一个命令的终止状态：

```
$ echo $?
130
```

我们看到进程的终止状态为 130。这表示进程被信号 130 – 128 = 2 杀死——信号号 2 是 `SIGINT`。

接下来，我们使用程序来禁用中断字符。

```
$ ./new_intr

$ stty

speed 38400 baud, line = 0;

intr = ^<def>
```

### 验证更改

现在我们发现 Control-C 和 Control-L 都不再产生 `SIGINT` 信号，我们必须使用 Control-\ 来终止程序：

```
$ sleep 10

^C

Type Control-\ to generate SIGINT

Quit

$ stty sane
```

Control-C 和 Control-L 仅被回显

将终端恢复正常状态

## 列表 62-1: 更改终端中断字符

```c
#include <termios.h>
#include <ctype.h>
#include "tlpi_hdr.h"
int
main(int argc, char *argv[])
{
    struct termios tp;
    int intrChar;
    if (argc > 1 && strcmp(argv[1], "--help") == 0)
```

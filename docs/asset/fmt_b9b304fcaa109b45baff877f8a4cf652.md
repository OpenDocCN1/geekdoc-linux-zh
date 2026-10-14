
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

我们看到进程的终止状态为 130。这表示进程被信号 130 – 128 = 2 杀死——信号号 2 是 SIGINT。

接下来，我们使用程序来禁用中断字符。

```
$ ./new_intr
$ stty
speed 38400 baud, line = 0;
intr = ^<def>
```

### 验证更改

现在我们发现 Control-C 和 Control-L 都不再产生 SIGINT 信号，我们必须使用 Control-\ 来终止程序：

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
        usageErr("%%s [intr-char]\n", argv[0]);
    /* Determine从命令行控制新的 INTR 设置 */
    if (argc == 1) {
        intrChar = fpath(STDIN_FILENO, _PC_VDISABLE);
        if (intrChar == -1)
            errExit("Couldn't determine VDISABLE");
    } else if (isdigit((unsigned char)argv[1][0])) {
        intrChar = strtol(argv[1], NULL, 0); /* 允许十六进制、八进制 */
    } else {
        intrChar = argv[1][0]; /* 字面字符 */
    }
    /* 获取终端设置，修改 INTR 字符，并将
       更改推回终端驱动程序 */
    if (tcgetattr(STDIN_FILENO, &tp) == -1)
        errExit("tcgetattr");
    tp.c_cc[INTR] = intrChar;
    if (tcsetattr(STDIN_FILENO, TCSFLUSH, &tp) == -1)
        errExit("tcsetattr");
    exit(EXIT_SUCCESS);
}
```

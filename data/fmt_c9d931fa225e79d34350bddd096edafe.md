
如果 `VTIME` 和 `VMIN` 均不为0，`VTIME` 指定了在至少有一个字节可用后 `read()` 等待的十分之一秒数。如果在调用 `read()` 时数据可用，定时器会立即启动。如果在调用 `read()` 时数据可用，则在第一个字节到达时启动定时器。`read()` 在至少到达 `VMIN` 个字节或定时器到期时返回，以先到者为准。它将始终返回一个字节，因为定时器在至少有一个字节可用后才开始计时。

如果 `VTIME` 和 `VMIN` 都为 0，`read()` 将始终立即返回，即使没有可用数据。同样，0 并不一定意味着文件结束状态。

## 15.6 伪 tty

伪 tty（或 `pty`）是一种机制，允许用户级程序（逻辑上）替代某个硬件的 tty 驱动程序。`pty` 有两个不同的端：模拟硬件的端称为 `pty` 主端（`pty-master`），而为程序提供正常 tty 接口的端称为 `pty` 从端（`pty-slave`）。从端看起来像一个普通的 tty；主端则像一个标准字符设备，它并不是一个 tty。

串口端口驱动程序通常实现为内核中的一段中断驱动代码，程序通过特定的设备文件与其通信。然而，事实并非如此。例如，至少存在一种基于 SCSI 的终端服务器，它使用 SCSI 协议的通用接口，让用户级程序与终端服务器通信，并通过 `ptys` 访问串口端口。

网络终端会话以相同的方式进行；`logind` 和 `telnetd` 程序将网络套接字连接到 `pty` 主端，并在 `pty` 从端上运行 `shell`，以建立像 tty 一样的网络连接，允许你通过非 tty 网络连接上运行交互式程序。`screen` 程序将多个 `pty` 连接复用到一个 tty 上（该 tty 可能是也可能不是 `pty`），并连接到用户。`expect` 程序让那些坚持必须在 tty 交互模式下运行的程序，在连接到 `pty` 主端的程序的控制下于 `pty` 从端运行。

### 15.6.1 打开伪 tty

遗憾的是，打开伪 tty 的过程在不同平台上有所不同。Linux 遵循 BSD 模型而非 SysV 模型。有256 个 `pty` 设备可用，为了找到第一个打开的设备，程序通常按从设备号顺序搜索设备。它们通过在 `ptpair.c` 中所示的特殊字典序方式进行搜索。遗憾的是，旧版本的 Linux 以及许多 Unix 变体仅提供 64 个设备。如果可用此类设备，按顺序搜索可能会让程序更快。

第 19 行的 `get_master()` 函数打开主 `pty` 并将文件描述符返回给父进程。如果它返回 0，则发生了错误。否则，它返回主 `pty` 文件描述符，并填充相应的从端名称。一旦从端被打开，你就负责释放内存。

```c
int get_master(char **name) {
    int i, j;
    int master = -1;
    *name = strdup("/dev/pty");

    for (i=0; i<16 && master <= 0; i++) {
        for (j=0; j<16 && master <= 0; j++) {
            snprintf(*name + strlen(*name), 256, "%d/%d", i, j);
            master = open(*name, O_RDWR);
            if (master < 0) {
                if (errno == ENOENT) {
                    /* 我们没有足够的 pty 设备 */
                    free(*name);
                    return (master);
                }
            }
        }
    }
    if (master < 0 && i == 16) {
        /* 尝试了所有 pty 失败 */
        free(*name);
        return (master);
    }
    chmod(name, S_IRUSR|S_IWUSR);
    master = open(name, O_RDWR);
    return(master);
}
```

`get slave()` 函数没有新内容。它包含的所有函数在其他地方都有描述，所以我们在这里不解释它。

### 15.6.2 伪 pty 示例

编写编写使用 `pty` 的最简单的程序，可能是打开一个 `pty` 对并在从端上运行 `shell`，将其连接到主端的程序。写完该程序后，你可以按照任何想要的方式扩展它。`ptytest.c` 是一个使用 `ptypair.c` 中定义的函数的示例。

```c
#include <errno.h>
#include <fcntl.h>
#include <grp.h>
#include <signal.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ioctl.h>
#include <sys/time.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <termios.h>
#include <unistd.h>
#include "ptypair.h"

volatile int propagate_sigwinch = 0;
```

```c
/*
 * 将窗口大小变化从输入文件描述符传播到
 * pty 的主端。
 */
void sigwinch_handler(int signal) {
    propagate_sigwinch = 1;
    
     
    /* pytest 尝试打开一个 pty 对，其在从端 pty 
    * 下方运行着一个 shell。
    */
int main(void) {
    int master;
    int pid;
    char *name;
    fd_set ready;
    #define BUFSIZE 1024
    char buf[1024];
    struct termios ot, t;
    struct winsize ws;
    int done = 0;
    struct sigaction act;
    
    if ((master = get_master_pty(&name)) < 0) {
        perror("pty: could not open master pty");
        return 1;
    }

    /* 设置 SIGWINCH 处理器 */
    act.sa_handler = sigwinch_handler;
    sigemptyset(&act.sa_mask);
    act.sa_flags = 0;
    if (sigaction(SIGWINCH, &act, NULL) < 0) {
        perror("pty: could not handle SIGWINCH");
        return 1;
    }

    if (ioctl(STDIN_FILENO, TIOCGWINZ, &ws) < 0) {
        perror("pty: could not get window size");
        exit(1);
    }
```

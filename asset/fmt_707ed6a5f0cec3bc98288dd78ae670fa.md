
```cpp
/* soputc.cpp - soputc */

#include <stdio.h>
#include <winsock.h>

#include "telnet.h"
#include "local.h"
```

```cpp
/* ---------------------------------------------------------- --
* soputc 将字符从键盘移动到套接字
 * ---------------------------------------------------------- -- *//* 使用的参数*/
int
soputc(SOCKET sfd, FILE *tfp, int c)
{
    if (isndisary) {
        if (c == IAC) {
            (void) soputc(TCIAC, sfd); /* 字节填充 IAC */
            (void) soputc(c, sfd);
            return 0;
        }
        c &= 0x7f; /* 仅限 7 位 ASCII */
        if (c == t_intr || c == t_quite) { /* 中断 */
            (void) soputc(TCIAC, sfd);
            (void) soputc(TCIP, sfd);
        } else if (c == sg_erase) { /* 擦字符 */
            (void) soputc(TCIAC, sfd);
            (void) soputc(TCBC, sfd);
        } else if (c == sg_kill) { /* 删除行 */
            (void) soputc(TCIAC, sfd);
            (void) soputc(TCEL, sfd);
        } else if (c == t_flush) { /* 取消输出 */
            (void) soputc(TCIAC, sfd);
            (void) soputc(TCAO, sfd);
        } else
            (void) soputc(c, sfd);
        return 0;
    }
}
```

在二进制模式下传输时，只需要对 `IAC` 字符进行填充。也就是说，`soputc` 必须将每个 `IAC` 字符替换为两个 `IAC` 字符。对于任何其他字符，`soputc` 仅仅是调用 `soputc` 来发送它。

### IAC IP

它显式地检查 NVT 定义的每个特殊字符。`soputc` 还必须处理没有 NVT 编码的字符。然而，NVT 协议规定，如果服务器没有请求客户端使用二进制传输，服务器将丢弃用户输入的大多数控制字符。

## 26.17 在用户终端上显示传入数据

从服务器通过 TCP 连接到达的数据可以被解码（如果服务器同意传输二进制），或者它可能由根据 NVT 规则编码的字符组成。客户端调用 `ttputc` 过程在用户的终端上显示传入的字符。

```cpp
/* ttputc.cpp ttputc */

#include <stdio.h>
#include <winsock.h>

#include "telnet.h"

int xputc(char, FILE);

/*
 * ttputc - 在网络虚拟终端上打印单个字符
 */
/* 使用的参数*/
int
ttputc(SOCKET sfd, FILE *tfp, int c)
{
    static last_char;
    int tc = 0;

    if (recvbinary) {
        (void) xputc(c, tfp);      /* 不经解释地打印 */
        return 0;
    }
    if (syncing)                /* 如果在 SYNCH 状态，无数据 */
        return 0;
}

    if ((last_char == VPCR && c == VPLF) ||
        (last_char == VPLF && c == VPCR)) {
        (void) xputc(VPLF, tfp);
        last_char = 0;
        return 0;
    }

    if (last_char == VPCR) {
        (void) xputc(VPCR, tfp);
    } else if (last_char == VPLF) {
        (void) xputc(VPLF, tfp);
    }

    if (c >= ' ' && c < IAC)         
        (void) xputc(c, tfp);
    } else {
        switch (c) {
            case VPLF:
                tc = 1;
            case VPCR:
                tc = 1;
            default:
                break;
        }
    }
    if (!tc) {
        (void) xputc(c, tfp);
    }
    last_char = c;
    return 0;
}
```

## 26.18 向服务器写入数据块

Telnet 调用 `sowrite` 向服务器写入一个数据块。如果服务器处于二进制模式，块中的每个 `IAC` 字符都必须填充。文件 `sowrite.cpp` 包含代码：

```cpp
/* sowrite.cpp - sowrite */

#include <stdio.h>
#include <winsock.h>

#include "trnsm.h"

extern int substate;

/*
 * sowrite - 对服务器进行输出处理
 */
void
sowrite(SOCKET sfd, FILE *tfp, u_char *buf, int c)
{
    for (int i = 0; i < c; i++) {
        u_char ch = buf[i];
        if (ch == IAC) {
            // 在二进制模式下，填充 IAC
            // 此为实现的占位符
        }
        fputc(ch, tfp);
    }
}
```

```c
if ((pt->ft_action)(sfd, tfp, c) < 0)
    sostate = KSREMOTE;    /* 发生错误 */
else
    sostate = pt->ft_next;
```

`Sowrite` 遍历指定块中的每个字符，并运行有限状态机（`fsms`）来处理每个字符。

## 26.19 与本地客户端交互

大多数 TELNET 客户端程序中，我们的实现允许用户与本地客户端程序进行交互。要实现这一点，用户输入键盘转义字符，后跟跟一个命令。表 26.1 列表列出了可以转义转义字符的可能命令及其含义：

| 符号名称 | 输入的字符 | 含义 |

| --- | --- | --- |

| KCDCONKSTATUS | ¶T | 立即终止会话。打印关于当前连接的状态信息。 |

| KCESAPE | ] | 将转义字符作为数据发送到服务器。 |

| KCSCRIPT | s | 开始向指定文件写入脚本。 |

| KCUNSCRIPT | u | 终止脚本。 |

> 图 26.1 TELNET 客户端在跟随 `KCESAPE` 之后解释为命令的输入字符。符号 † 表示通过按住 CONTROL 并输入 X 生成的字符。

文件 `telnet.h` 包含每个键盘字符的符号定义。例如，它定义转义字符 `KCESAPE` 为 `]`（即八进制值为 035 的字符）。

当客户端遇到转义字符时，它会将套接字输出 FSM 的状态从 `KSREMOTE` 更改为 `KSLOCAL`，并将随后的字符解释为命令。大多数命令由单个字符组成，套接字输出 FSM 通常回到 `KSREMOTE` 并执行与命令相关的操作。例如，如果字符 `KCDCON` 遇到 `KCESAPE`，它将调用过程 `dcon`。

*`telnet.h` 位于第 372 页。

† 套接字输出 FSM 在第 383 页的图 75.7 中描述。

## 26.20 响应非法命令

如果用户在键盘输出 FSM 调用动作过程后输入了未识别的字符，将调用动作过程 `sonotsup`，该过程会打印错误消息。文件 `sonotsup.cpp` 包含代码：

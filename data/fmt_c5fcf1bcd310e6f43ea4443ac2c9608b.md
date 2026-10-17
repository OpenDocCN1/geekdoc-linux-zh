
### 25.5 重写原理 FSM，以包含用于选项子协商的状态。

### 25.6 示例 FSM 使用紧凑表示来节省空间。估计使用传统表示法原理 FSM 所需的空间，并将其与紧凑表示所需的空间进行比较。

### 25.7 在什么条件下从连接的 `*recv*` 会返回 0？

### 25.8 阅读 TELNET 协议以找到同步的精确规则。为什么同步是必要的？

### 25.9 服务器可以在客户端发送文件结束符（EOF）后选择发送更多数据。客户端如何知道终止连接？

### 25.10 重写 `*twrite*` 使其不使用 FSM。每种实现方法的优缺点是什么？

### 25.11 当发生错误时，代码会打印一个晦涩的消息并退出。改进代码以打印用户能理解的消息。

### 25.12 在上一个练习中，检查你的系统可以返回的错误代码。所有错误对用户来说都有意义吗？为什么或为什么不？

### 25.13 有限状态机没有同步的显式状态。修改状态图以包含同步。需要多少额外状态？

### 25.14 为 FSM 添加用于脚本的状态是否有意义？如果是，需要修改哪些有限状态机？如果不是，请解释原因。

## 26.3 记录选项请求的类型

在状态 `TSIAC` 中（即在收到 `TCIAC` 字符后），`TCWILL` 或 `TCWONT` 的到达会导致状态转换到 `TSWOPT`。FSM 规定应该调用 `record` 过程。`rec` 记录导致状态转换的字符，以便以后使用。同样，FSM 使用 `recopt` 在转换到 `TSWOPT` 状态的期间记录字符 `TCDO`。文件 `recopt.cpp` 包含以下代码：

```
/* recopt.cpp - recopt, no_op */

#include <stdio.h>
#include <winsock.h>

/* char option_cmd; /* 值为 WILL, WONT, DO, 或 DONT */

-----------------------------------------------------------------------
* recopt - 记录选项类型
-----------------------------------------------------------------------
/* /ARGSUSED*/
int
recopt(SOCKET sfd, FILE *tfp, int c)
{
    option_cmd = c;
    return 0;
}

-----------------------------------------------------------------------
* no_op - 什么都不做
-----------------------------------------------------------------------
/* /ARGSUSED*/
int
no_op(SOCKET sfd, FILE *tfp, int c)
{
    return 0;
}
```

## 26.4 执行无操作

文件 `recept.cpp` 也包含过程 `no_op` 的代码。由于 FSM 必须对状态和输入字符的所有可能组合都有动作，因此过程 `no_op` 可用于那些不需要任何操作转换。例如，从状态 `TSDATA` 到 `TSIAC` 的转换不需要任何操作。因此，FSM 规定调用 `no_op`。

## 26.5 对 ECHO 选项响应 WILL/WONT

服务器发送 `WILL` 或 `WONT` 后紧跟 `ECHO` 选项，告知客户端它愿意回显字符或愿意停止回显字符。FSM 规定当此类消息到达时应该调用 `do_echo` 过程。

```
* do_echo.cpp - do_echo /*

#include <stdio.h>
#include <winsock.h>

#include "local.h"
#include "telnet.h"

unsigned char doecho;      /* 如果远程开启 ECHO 则为非零 */
extern u_char option_cmd;

----------------------------------------------------------------------
/*
* do_echo  处理 TELNET WILL/WONT ECHO 选项
----------------------------------------------------------------------
*/
int
do_scho(SOCKET sfd, FILE *tfp, int c)
{
    if (doecho) {
        if (option_cmd == TCWILL)
            return 0;      /* 已开启 ECHO */
    } else if (option_cmd == TCWONT)
        return 0;      /* 已未开启 ECHO */
    }
    if (option_cmd == TCWILL)
        ttyflags &= -ECHO;
    else
        ttyflags |= ECHO;
    doecho = !doecho;
```

```
(void) sputc(TCIAC, sfd);
if (doescho)
    (void) sputc(TCDO, sfd);
else
    (void) sputc(TDONT, sfd);
(void) sputc((char)c, sfd);
return 0;
```

TELNET 协议规定服务器可以发送 `WILL` 或 `WONT` 来宣布其执行某选项的意愿，也可以在响应客户端请求时发送此类消息。因此，如果客户端的请求包含 `DO` 或 `DONT`，则服务器的消息构成一个回复；否则，它构成一个公告。

客户端使用其状态来决定如何响应。如果客户端当前期望服务器执行字符回显，全局变量 `doescho` 包含非零值。如果服务器发送 `WILL` 而客户端已经开启了远程回显，则客户端不回复。同样，如果服务器发送 `WONT` 而客户端已禁用远程回显，则客户端不回复。然而，如果服务器发送 `WILL` 而客户端当前禁用了本地回显，则设置全局变量 `tryflags` 中的 `ECHO` 位以禁用本地字符回显（记住键盘线程会检查该位以决定是否回显按键）。如果当 `WONT` 到达时，客户端禁用了本地回显，则客户端假设服务器已禁用了远程回显。因此，客户端设置全局变量 `tryflags` 中的 `ECHO` 位以启用本地回显。客户端仅在更改本地回显时，才发送 `DO` 或 `DONT` 响应。

### 26.6 发送响应

当 `do_echo` 过程需要向服务器发送响应时，它调用带有两个参数的 `sputc`：一个要发送的字符以及用于发送的套接字描述符。因此，需要发送两个字符响应的 `do_echo` 过程必须调用两次 `sputc`（一次用于 `IAC`，一次用于 `DONT`）。由于响应应该通过到达服务器的连接发送，因此每次调用的第二个参数都是 `sfd`，即连接的套接字描述符。

`sputc` 的代码很简单；可以在 `sputc.cpp` 中找到。

```
/* sputc.cpp - sputc */
#include <winsock.h>

/*--------------------------------------*/
* sputc - 在套接字上放置一个字符
/*--------------------------------------*/
int
sputc(const char c, SOCKET sfd)
{
    return send(sfd, &c, 1, 0);
}
```

## 26.7 对不支持的选项发送 WILL/WONT

当客户端收到对其不支持选项的 `WILL` 或 `WONT` 请求时，它调用 `do_notsup` 来回复 `DONT`。

```
/* do_notsup.cpp - do_notsup */
#include <stdio.h>
#include <winsock.h>

#include "local.h"
#include "telnet.h"

extern u_char option_cmd;

/*--------------------------------------*/
* do_notsup - 处理不支持的 telnet "will/wont" 选项
/*--------------------------------------*/
/*ARGSUSED*/
int
dotsup(SOCKET sfd, FILE *tfp, int c)
{
    (void) sputc(TCIAC, sfd);
    (void) sputc(TCDONT, sfd);
    (void) sputc((char)c, sfd);
    return 0;
}
```

## 26.8 对 Go-Ahead 选项响应 WILL/WONT

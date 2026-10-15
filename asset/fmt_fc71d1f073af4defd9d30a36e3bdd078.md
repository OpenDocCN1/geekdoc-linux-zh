
```cpp
/* sofsm.cpp */
#include <stdio.h>
#include <winsock.h>

#include "telnet.h"
#include "tnfsm.h"

/* 特殊字符: * */
char t_flushc = '\017'; /* * ^ */
char t_intrc = '\003'; /* * \ */
char t_quitc = '\034'; /* * # */
char sg_erase = '\010'; /* * X */
char sg_kill = '\030';
```

```cpp
extern int soputc(SOCKET, FILE *, int), scrinit(SOCKET, FILE *, int),
sergetc(SOCKET, FILE *, int), scwrap(SOCKET, FILE *, int),
unscript(SOCKET, FILE *, int), dcon(SOCKET, FILE *, int),
status(SOCKET, FILE *, int), snotsup(SOCKET, FILE *, int),
no_op(SOCKET, FILE *, int), tnabort(SOCKET, FILE *, int);
```

```cpp
struct fsm_trans_stab[] = {
    /* State         Input           Next State       Action */
    /* 数据输入 */
    { KSREMOTE, KESCAPE, KSLOCAL, no_op },
    { KSREMOTE, KCANY, KREMOTE, soputc },
    /* 本地转义命令 */
    { KSLOCAL, KCSCRIPT, KSCOLLECT, scrinit },
    { KSLOCAL, KCUNSCRIPT, KREMOTE, unscript },
    { KSLOCAL, KESCAPE, KREMOTE, soputc },
    { KSLOCAL, KCDON, KREMOTE, dcon },
    { KSLOCAL, KCSTATUS, KREMOTE, status },
    { KSLOCAL, KCANY, KREMOTE, snotsup },
    /* 脚本文件名收集 */
    { KSCOLLECT, KCCR, KSREMOTE, scrwrap },
    { KSCOLLECT, KCANY, KSCOLLECT, scrgetc },
    { FSINVALID, KCANY, FSINVALID, tnabort },
}
```

```cpp
#define NTRANS (sizeof(sostab)/sizeof(sostab[0]))
```

```cpp
int sostate;
uchar bofsmm[NKSTATES][NCHRS];
```

数组 `sostab` 包含紧凑表示，变量 `sostate` 包含一个给出了套接输出 FSM 当前状态的整数。

## 25.21 选项子协商有限状态机

25.8 展示了客户端中使用的第三个 FSM。它处理在选项子协商期间到达的字符序列。因为它只识别一种可能的选项子协商（终端类型），FSM 只需要三个状态。

![](img/7fd1ea9db2b1f52482f69f28c8dd336d_399_0.png)

动作过程：

- A - `no_op`
- B - `subtermtype`

图 25.8 用于选项子协商的简单 FSM。客户端在每次完成选项子协商时都会重新初始化该机器。

思考子协商最简单的方法是想象它描述了主 FSM 中 `TUSSUBNEG` 状态的内部结构。当主 FSM 运行在 `TUSSUBNEG` 状态时，它会调用子过程处理每个迁入的字符。`Subopt` 运行子协商 FSM。如图 2.5 所示，如果机器找到了终端类型，它将移动到 `_END_` 状态。否则，它将移动到 `TUSSUBNEG` 状态。一旦进入 `TUSSUBNEG`，FSM 将对选项做出决策：如果动词是 `SEND`，它将调用 `subtype`。

## 25.22 子协商的定义

文件 `fsm.cpp` 包含了子协商的声明。

```cpp
/* fsm.cpp - subnegotiation */
#include <stdio.h>
#include <winsock.h>

#include "telnet.h"
#include "tnfsm.h"

extern int soputc(SOCKET, FILE *, int), scrinit(SOCKET, FILE *, int),
sergetc(SOCKET, FILE *, int), scwrap(SOCKET, FILE *, int),
               unscript(SOCKET, FILE *, int), dcon(SOCKET, FILE *, int),
               status(SOCKET, FILE *, int), snotsup(SOCKET, FILE *, int),
               no_op(SOCKET, FILE *, int), tnabort(SOCKET, FILE *, int);

struct fsm_trans substab[] = {
    /* State         Input           Next State       Action */
    { T_START,    KCANY, T_START,   no_op },
    { T_START,    KTYPE, TUSSUBNEG, subtype },
    { TUSSUBNEG, KCANY, TUSSUBNEG, no_op },
    { TUSSUBNEG, KESCAPE, T_END,    no_op },
};

extern int subtype(SOCKET, FILE *, int);

int tsubostate;
u_char tsubofsmm[NKSTATES][NCHRS];
```

## 25.23 FSM 初始化

在启动时，客户端调用 `fsmbuild` 初始化所有状态机。如 `fsmbuild` 文件所示，它为每个机器分配了一个初始状态。

```cpp
/* fsmbuild - fsmbuild */
#include <stdio.h>
#include <winsock.h>

#include "telnet.h"
#include "tnfsm.h"

extern struct fsm_trans ttstab[];
extern u_char ttfsm[][NCHRS], sofsm[][NCHRS], subfsm[][NCHRS];
extern int ttstate, socstate, substate;

/*
 * fsmbuild - 构建有限状态数据
 */
fsmbuild() {

fsminit(ttfsm, ttstab, NTSTATES);
ttstate = TSDATA;

fsminit(sofsm, substab, NKSTATES);
socstate = KSREMOTE;

fsminit(subfsm, substab, NSSTATES);
substate = SS_START;
}
```

## 25.24 TELNET 客户端的参数

文件 `tclient.cpp` 包含了当用户调用客户端时执行的主程序：


```c
extern int do_echo(SOCKET fd, FILE *tfp, int c);

struct fsm_trans ttstab[] = {
    /* 状态             输入           目标状态       动作 */
    /*                ------------------------- */
    { TSDATA,          TCANY,           TSIAC,           no_op },
    { TSDATA,          TCANY,           TSDATA,          ttput },
    { TSIAC,           TCIAC,           TSDATA,          ttput },
    { TSIAC,           TSEB,           TSSUBNEG,       no_op },
    { TSIAC,           TCDM,            TSDATA,          tcdm },
    { TSIAC,           TCWILL,          TSWOPT,          recept },
    { TSIAC,           TCWONT,          TSWOPT,          recept },
    { TSIAC,           TCDO,            TSDFT,          recept },
    { TSIAC,           TCION,            TSDFT,          recept },
    { TSIAC,           TCANY,           TSDATA,          no_op },
    /* 选项协商 */
    { TSSUBNEGO,       TCIAC,           TSSUBIAC,       no_op },
    { TSSUBNEGO,       TCANY,           TSSUBNEG,       subopt },
    { TSIAC,           TCSE,            TSDATA,          subend },
    { TSIAC,           TCANY,           TSSUBIAC,       subopt },
    /* 选项子协商 */
    { TSWOPT,          TOTERTYPE,       TSDATA,          will_termtype },
    { TSWOPT,          TOTBINARY,       TSDATA,          will_txbinary },
    { TSWOPT,          TCANY,           TSDATA,          will_notsup },
    { FSINVALID,       TCANY,           FSINVALID,       tnabort }
};

/*----------------------------------------------------------------------*/
* fsminit - 有限状态机初始化器
/*----------------------------------------------------------------------*/
void
fsminit(u_char ftfsm[][NCHRS], struct fsm_trans ttab[], int nstates)
{
    struct fsm_trans       *pt;
```

## Sec. 25.18 构建 FSM 转移矩阵

`int` `sn`, `ti`, `cn`;

```c
for (cn=0; cn<nCRS; ++cn)
    for (ti=0; ti<nstates; ++ti)
        fsm[ti][cn] = TINVALID;
```

```c
for (ti=0; ttab[ti].ft_state != FSINVALID; ++ti) {
    pt = &ttab[ti];
    sn = pt->ft_state;
    if (pt->ft_char == TCANY)
        for (cn=0; cn<nCRS; ++cn)
            if (fsm[sn][cn] == TINVALID)
                fsm[sn][cn] = ti;
    else
        fsm[sn][pt->ft_char] = ti;
}
```

```c
/* 将所有未初始化的索引设置为无效转移
for (cn=0; cn<nCRS; ++cn)
    for (ti=0; ti<nstates; ++ti)
        if (fsm[ti][cn] == TINVALID)
            fsm[ti][cn] = ti;
```

过程 `fsminit` 需要三个参数。参数 `fsm` 指定一个必须初始化的转移矩阵。参数 `ttab` 给出了紧凑 FSM 表示的地址，`nstates` 指定了生成的 FSM 中的状态数量。

`Fsminit` 首先将整个转移矩阵初始化为 `TINVALID`。它遍历紧凑表示的每个元素，并将该元素指定的状态转移添加到转移矩阵中。最后，它再次遍历转移，将任何未填充的转移更改为指向紧凑表示末尾的无效转移。

`fsminit` 中的大部分代码都是直观的。在添加转移时，`fsminit` 必须区分显式转移和缩写。为了理解这些代码，请记住紧凑表示使用 `TCANY` 来表示所有未显式指定的字符。因此，当 `fsminit` 检查单个转移时，它会检查触发转移的字符。如果条目指定的字符是 `TCANY`，`fsminit` 将遍历所有可能的字符，并将转移添加到任何未初始化的字符上。如果条目指定的是 `TCANY` 以外的任何字符，`fsminit` 将为单字符填充转移数组。

## Sec 25.19 Socket 输出有限状态机

图 25.3 显示的有限状态机定义了客户端针对从服务器到达的每个字符所采取的动作。另一个独立且更简单的有限状态机描述了客户端如何处理来自键盘到达的字符。我们将与键盘输入相关的 FSM 称为 socket 输出 FSM。这个名字听起来可能很寻常。图 25.6 显示了客户端软件如何支持这样一个命名。

![](img/0ff5db763d2952e789585a5178acf3bc_396_0.png)

图 25.6 客户端软件组织。主线程等待通往远程服务器的 TCP 连接或通往键盘的本地连接就绪。然后，它从就绪的套接字读取一个字符，并调用 FSM 过程进行处理。处理键盘数据的 socket 输出 FSM 与用于向远程服务器传递输出的套接字相关。

与原理有限状态机不同，用于 socket 输出的有限状态机非常直观。如图 25.7 所示，该机器包含三个状态。本质上，`KSREMOTE` 状态处理正常情况。当机器保持在 `KSREMOTE` 时，客户端会将用户在键盘上输入的每个字符通过 TCP 连接发送到服务器。

![](img/0ff5db763d2952e789585a5178acf3bc_397_0.png)

动作过程：

- A - `dcon`

- F - `scrwrap`

- B - `sonotsup`

- G - `sopute`

- C - `no_op`

- H - `status`

- D - `scrgetc`

- J - `suspend`

- E - `scrint`

- K - `unscript`

**图 25.7** 用于定义用户输入的每个字符的动作的 socket 输出 FSM。客户端将大多数数据字符发送到远程服务器。然而，该设计允许用户跳出数据连接与本地客户端进行通信。

socket 输出 FSM 从 `KSREMOTE` 状态开始。因此，当它首次启动时，客户端将每个按键发送到远程服务器。当用户输入键盘上的 键时，客户端进入 `KSLOCAL` 状态并等待下一个按键。大多数在转义键之后的按键没有意义，但少数按键会导致客户端采取行动并返回 `KSREMOTE` 状态。只有 `KSCRIPT` 会导致客户端进入 `KSCOLLECT` 状态，在该状态下它收集一个用于脚本的文件名。

## Sec 25.20 Socket 输出 FSM 的定义

```c
#define NTRANS (sizeof(sostab)/sizeof(sostab[0]))
```

```c
int sostate;
u_char bofsm[NKRSTATES][NCHRS];
```

数组 `sostab` 包含紧凑表示，变量 `sostate` 包含一个整数，给出 socket 输出 FSM 的当前状态。

## Sec 25.21 选项子协商有限状态机

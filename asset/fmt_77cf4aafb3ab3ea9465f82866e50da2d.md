
| BSDLY | 退格格延迟掩码。值为 `BS8` 或 `BS1`。 |

| VTDLY | 垂直制表延迟掩码。值为 `VT0` 或 `VT1`。 |

| FFDLY | 换页延迟掩码。值为 `FF0` 或 `FF1`。 |

`c_cflag` 标志位常量为：

| 标志 | 描述 |
| :--- | :--- |
| `CSIZE` | 字符大小掩码。值为 `CS5`、`CS6`、`CS7` 或 `CS8`。 |
| `CSTOPB` | 设置两个位，而不是一个。 |
| `CREAD` | 启用接收器。 |
| `PAREN` | 输出生成奇偶校验，输入进行奇偶校验。 |
| `PAROD` | 输入和输出的奇偶校验为奇。 |
| `HUPCL` | 在最后一个进程关闭设备后降低调制控制线（挂起）。 |
| `CLOCAL` | 忽略调制调器控制线。 |
| `CIBAUD` | 输入掩码（未使用）。 |
| `CRCTS` | 流控。 |

`c_iflag` 标志位常量为：

| 标志 | 描述 |
| :--- | :--- |
| `ISIG` | 当接收到 `INTR`、`QUIT`、`SUSP` 或 `DSUSP` 任何字符时，产生相应的信号。 |
| `IANON` | 规范模式。这启用了特殊字符 `EOF`、`EOL`、`E2`、`ERASE`、`KILL`、`REPRINT`、`STTY` 和 `WERASE`，并按行进行缓冲。 |
| `XCASE` | 如果也设置，终端为大写。只有输入会被转换为小写，但被 `\` 之前的置的字符除外。在输出时，大写字母前会有 `\` ，且小写字母会被转换为大写字母。 |
| `ECHO` | 如果也设置，`ERASE` 字符会删除输入字符，`WERASE` 会擦除整行。 |
| `EOECH` | 如果也设置，`KILL` 字符会擦除当前行。 |
| `ECHOL` | 如果也设置，即使未设置 `ECHO`，也会回显最后一个字符。 |
| `ECHOCTL` | 如果也设置，除 `TAB`、`NL`、`START` 和 `STOP` 以外的 ASCII 控制字符将回显为 "`x`" ，其中 `x` 是 ASCII 代码为 `0x28` 或大于控制信号的字符。 |
| `EOPRTR` | 如果 If$ 和 `ECHO` 也设置，字符将在被删除时进行打印。 |
| `EOKE` | 如果也设置，`KILL` 将根据 `ECHO` 和 `EOPRTR` 的指定，杀死行上的每个字符。 |
| 标志 | 描述 |
| :--- | :--- |
| `FLUSH` | 输出被冲刷。该标志通过输入 `DISCARD` 字符来切换状态。 |
| `NOFLSH` | 在产生 `SIGINT` 和 `SIGQUIT` 信号时不禁用输入输出队列的冲刷，并在产生 `SIGSUSP` 信号时不冲刷输入队列。 |
| `TOSTOP` | 向尝试写入其控制终端的后台进程组发送 `SIGSTOP` 信号。 |
| `PENDIN` | 当读取下一个字符时，输入队列中的所有字符将重新打印（bash 采用这种处理方式）。 |
| `IEXTEN` | 启用实现定义的输入处理。 |

`tcgetattr()` 获取与 `fd` 指向的对象相关的参数，并将其存储在 `termios.p` 定义的 `termios` 结构中。此函数可以从后台进程调用；但终端属性随后可能会被前台进程更改。

# 第三部分：库函数

`tcsetattr()` 根据 `termios_p` 指向的 `termios` 结构设置与终端相关的参数（除非需要底层硬件支持但尚不可用的支持），`termios_p.optional_actions` 指定了更改何时生效：

`TCSOW`

更改立即发生。

`TCSADRAIN`

更改在所有写入 `fd` 的输出传输后发生。更改影响输出的参数时应使用此函数。

`TCSAFLUSH`

更改在所有写入 `fd` 指向对象的输出传输后发生，并且在进行更改之前接收到的所有输入都不会被丢弃。

`tcsendbreak()` 如果终端使用异步串口数据传输，则会传输一个持续的零值位流。如果持续时间为零，它将传输零值位至少 0.25 秒，不超过 0.5 秒。如果持续时间不零，它将传输持续时间秒的零值位，至少0.25 秒，不超过 0.5 秒。

如果终端没有使用异步串口传输，`tcsendbreak()` 将不执行任何操作返回。

`tcdrain()` 等待所有写入 `fd` 指向对象的输出传输完成。

`tcflush()` 根据 `selector` 的值丢弃 `fd` 指向对象中未传输的数据，或已接收但未读的数据：

- `TCIFLUSH`: 冲刷已接收但未读的数据
- `TCOFLUSH`: 冲刷已写入但未传输的数据
- `IOFLUSH`: 同时冲刷已接收但未读和已写入但未传输的数据

`tcflow()` 根据 `action` 挂起 `fd` 指向对象上的数据传输或接收：

- `TCOFF`: 挂起输出
- `TCCON`: 重启输出
- `IOFF`: 发送 `STOP` 字符，停止终端设备向系统传输数据
- `TCION`: 发送 `START` 字符，启动终端设备传输数据

（注：原文后续部分存在大量乱码或重复占位符，根据高级工程师规范，此处已过滤无意义的重复/错误文本）

## toascii

`toascii`—将字符转换为 ASCII

### 概要

```
#include <ctype.h>
int toascii(int c);
```

### 描述

`toascii()` 通过清除高位位，将 `c` 转换为符合 ASCII 字符集的 7 位无符号字符（unsigned char）。

### 返回值

返回的是转换后字符的值。

### 符合

SVID, BSD

### 缺陷

如果你使用此函数，许多人会感到不快。此函数会将带重音的字母转换为随机字符。

### 参见

`isascii(3)`, `toupper(3)`, `tolower(3)`

GNU, 1995年9月16日

## toupper, tolower

`toupper`, `tolower`—将字母转换为大写或小写

### 概要

```
#include <ctype.h>
int toupper(int c);
int tolower(int c);
```

### 描述

如果可能，`toupper()` 将字母 `c` 转换为大写。

如果可能，`tolower()` 将字母 `c` 转换为小写。

### 返回值

返回的是转换后字母的值；如果无法转换，则返回 `c`。

### 符合

ANSI C, BSD 4.3

### 缺陷

构成大写或小写字母的细节取决于当前的语言区域（locale）。例如，默认情况下不识别重音符号（umlauts），因此不会对它们进行任何转换。

在某些非英语区域中，某些小写字母没有对应的大写形式；例如德语的尖 s（ß）。

### 第三部分：库函数

### 参见

`isalpha(3)`, `setlocale(3)`, `locale(7)`

GNU, 1993年4月4日

## tsearch, tfind, tdelete, twalk

`tsearch`, `tfind`, `tdelete`—管理二叉树

### 概要

```
#include <search.h>
void tsearch(const void *key, void **root,
int (compare)(const void *, const void *));
void *tfind(const void *key, const void **root,
int (compare)(const void *, const void *));
void tdelete(const void *key, void **root);
int (compare)(const void *, const void *));
void twalk(const void *root, const char *action)(const void *)
const VISIT visit,
int *depth);
```

### 描述

`tsearch`, `tfind` 和 `tdelete` 管理一个二叉树。它们是 Knuth (6.2.2) 算法 T 的泛化版本。树中每个节点的第一个字段是指向对应数据的指针。（调用程序必须存储实际数据。）`compar` 将项目与一个比较值进行比较，它接受指向两个项目的指针。它返回一个负、零或正整数，取决于第一个项目小于还是大于第二个项目。

`tsearch` 搜索一个项目。`key` 指向要搜索的项，`root` 指向指向树根的变量。如果树为空，应将变量 `root` 设置为 `NULL`。如果在树中找到该项，`tsearch` 返回该项的指针。如果未找到，`tsearch` 会将其添加并返回指向新添加项的指针。

`tfind` 类似于 `tsearch`，不同在于如果未找到该项，则返回 `NULL`。

`tdelete` 从树中删除一个项。其参数与 `tsearch` 相同。

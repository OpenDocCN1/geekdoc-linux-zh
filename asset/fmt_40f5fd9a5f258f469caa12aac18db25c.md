
不要置信，你的电脑内部声器是 Linux 控制台的一部分，因此是一个字符设备。因此，存在 `ioctl()` 请求来操作它。对于内部声器，有以下2 个请求：

- `1.` `KDMMTONE`：使用内核定时器产生一段鸣叫。示例：`ioctl(fd, KDMMTONE,(long) argument)`。
- `2.` `KIOCSOUND`：产生无限鸣叫或停止正在响的鸣叫。示例：`ioctl(fd,KIOCSOUND,(int) tone)`。

参数由低字字的音值和高字字的持续组成。音值不是频率。PC 主板定时器 `8254` 的时钟为 `1.19 MHz`，因此是 `1190000/频率`。持续以定时器周期为单位。两个 `ioctl` 调用都会立即返回，因此你可以在不阻塞程序的情况下产生声音。`KDMMTONE` 应该用于警告信号，因为你不需要担心停止声音。

### 7.2 为声卡编程

如果你想在硬件层面折腾声卡，你一定知道通过 `outb()` 和 `inb()` 的组合可以告诉声卡你正在寻找的设备。

# 69 第 7 章 音频编程

通过在程序中使用声卡驱动，程序很有可能在其他 i386 系统上运行；一些聪明的人决定为 Linux、isc、FreeBSD 以及大多数其他 i386 系统使用相同的驱动程序。如果其他架构上的 Linux 提供了相同的音频设备接口，这将有助于程序的移植。声卡不是 Linux 控制台的一部分，而是一个特殊的设备。声卡主要提供三个三个主要功能：

- 数字采样输入/输出
- 频率调制输出
- 一个 midi 接口

这些功能中的每一个都有自己的设备驱动接口。数字样本使用 `/dev/dsp`，频率调制使用 `/dev/sequencer`，midi 接口使用 `/dev/midi`。音量设置（如音量、平衡或低音）可以通过 `/dev/mixer` 接口进行控制。出于兼容性考虑，还存在一个 `/dev/audio` 设备，它可以读取 SUN μ-law 音频数据，但它映射到数字样本设备。

如果你猜到使用 `ioctl()` 来操作这些设备那是正确的。`ioctl()` 请求定义在 `<linux/soundcard.h>` 中，并以 `SNDCTL...` 开头。

> 由于我没有声卡，这里由别人继续写
> ven van der Meer v0.3.3, 1995年1月19日

# 第 8 章

## 字符单元图形

本章涉及不是基于像素而是基于字符的屏幕输入输出。当我们说字符时，指的是可以根据字符集更改的像素组合。你的显卡已经提供了一个或多个字符集，并默认以文本（字符集）模式运行，因为文本的处理速度比像素图形快得多。终端的操作远比将其作为简单的（哑）且无聊的文本显示器要得多。我将描述如何使用你的 linux 终端（尤其是 linux 控制台）提供的特殊功能。

- `printf`, `sprintf`, `fprintf`, `scanf`, `sscanf`, `sscanf`

通过 libc 中的这些函数，你可以将格式化字符串输出到 `stdout`（标准输出）、`stderr`（标准错误）或其他定义为 `FILE *stream` 的流（例如文件）。`Scanf(...)` 提供了一种从从 `stdin` 读取格式化输入的类似方法。

- `termcap`

`TERM`inal `CAP`abilitie（终端能力）数据库是 ASCII 文件 `/etc/termcap` 中的一组终端描述条目。在此处，你可以找到关于如何显示特殊字符、如何执行操作（删除、插入字符或行等）以及如何初始化终端的信息。该数据库被用于例如能力查询（参见 `termcap(3x)`）。通过此数据库，程序可以使用相同的代码处理各种终端。使用 termcap 数据库和库函数仅提供对终端的低级访问。更改属性或颜色、参数化输出和优化必须由程序员自己完成。

## terminfo 数据库

`TERM`inal `INF`Oration（终端信息）数据库基于 termcap 数据库，也描述了终端能力，但层级比 termcap 高。使用 terminfo，程序可以轻松地更改屏幕属性，使用如功能键等特殊键等。该数据库可以在 `/usr/lib/terminfo/[A-z,0-9]*` 中找到。每个文件描述一个终端。

## curses

Terminfo 是程序中处理终端的良好基础。`(BSD)CURSES` 库为你提供了对终端的高级访问，并基于 terminfo 数据库。Curses 允许你在屏幕上打开并操作窗口，提供了一套输入输出函数，并可以在 150 多个终端上独立地更改视频属性。curses 库可以在 `/usr/lib/libcurses.a` 中找到。这是 curses 的 BSD 版本。

- `ncurses`

`Ncurses` 是下一个改进。在 `1.8.6` 版本中，它与 `SYSVR4` 中定义的 `AT&T curses` 兼容，并具有一些扩展，如颜色操作、输出的特殊优化、终端特定优化等。它已经在 Sun-OS、HP 和 Linux 等许多系统上通过测试。我建议使用 ncurses 而不是其他。在 SYSV Unix 系统（如 Sun 的 Solaris）上应该存在一个与 ncurses 功能相同的 curses 库（实际上 solaris curses 有更多的函数和鼠标支持）。

在后续章节中，我将描述如何使用不同的包来访问终端。在 Linux 中，我们有 GNU 版本的 termcap，可以使用 ncurses 代替 curses。

## 8.1 libc 中的 I/O 函数

### 8.1.1 格式化输出

libc 中的 `printf(...)` 函数提供格式化输出并允许对参数进行转换。

- `int fprintf(FILE *stream, const char *format, ...)`，将转换输出
- 输出将写入流。
- 转换后的参数数量。
- 精度的可能值。

- `int printf(const char *format, ...)` - 等于 `fprintf(stdout, ...)`。
- `int sprintf(char *s, const char *format, ...)` - 与 `printf(...)` 相同，但输出将写入字符 `s`（后跟一个 `\0`）。

## 8.1 LIBC 中的 I/O 函数

**表 8.1: Libc - printf 转换**

| 字符 | 格式化为 |
| :--- | :--- |
| d | 有符号整数 - int |
| o | 无符号，八进制 - int |
| x,X | 十六整数 - int |
| u | 十进制，无符号 - unsigned int |
| c | 单个字符 - char |
| s | 字符串 - char * |
| e,E, g | 科学计数法 - double |
| p | 指针 - void * |
| n | 整数 - int * |

libc 中的 `printf(...)` 函数提供格式化输出并允许对参数进行转换。

- `int fprintf(FILE *stream, const char *format, ...)`，将转换输出
- 输出将写入流。
- 转换后的参数数量。
- 精度的可能值。

- `int printf(const char *format, ...)` - 等于 `fprintf(stdout, ...)`。
- `int sprintf(char *s, const char *format, ...)` - 与 `printf(...)` 相同，但输出将写入字符 `s`（后跟一个 `\0`）。

（注意：必须为 s 分配足够的内存。）

- `vprintf(const char *format, valist arg)`
- `vprintf(FILE *stream, const char *format, valist arg)`
- `vprintf(char *s, const char *format, valist arg)`
与上述函数相同，仅参数列表设置为 `arg`。

- `int scanf(FILE *stream, const char *format, ...)`

正如 `printf(...)` 用于格式化输出一样，你可以使用 `scanf(...)` 进行格式化输入。`scanf(...)` 从流中读取并根据 `format` 中定义的规则转换输入。结果将放在 `...` 提供的参数中（注意：参数必须是指针）。当 format 中没有更多转换规则时读取结束。当第一个转换到达文件尾或发生错误时，`scanf(...)` 返回 `EOF`。否则，它返回转换后的参数数量。

`format` 可以包含如何格式化输入参数的规则（参见第74页的表 8.2）。它还可以包含：

空格或制表符，这些会被忽略。
任何普通字符（% 处外）。这些字符必须出现在输入中的对应位置。

表 8.2: Libc - scanf 类型

| 字符 | 输入 - 参数类型 |
| :--- | :--- |
| d | 十进制整数 - int * |
| i | 整数 - int * (输入为 | |
| o | 八进制整数 - int * (带有或不带前导 0) |
| u | 十进制，无符号 - unsigned int * |
| x | 十六整数 - int * (带有或不带前导 0x) |
| c | 单个或多个字符 - char * (不带 \0) |
| s | 字符串 - char * |
| e,E, g,G | double |
| p | 指针 - void * |
| n | 整数 - int * |
| % | |





| s | 字符（不包含空格、制表符等） - char *（包含 \0） |
| --- | --- |
| e,f,gf p | float - float *（例如 [- Jm.ddddde+xx) 指针 - void * |
| n | 转换后的参数数量 - int * |
| [...] | 输入中的非空字符 - char * |
| [...] | 排除这些非空字符 - char * |
| % | % |

当指针为短类型时，`h` 可以位于 `d,i,n,o,u` 和 `x` 之前；当指针为长类型时，`l` 可以位于 `d,i,n,o,u` 和 `x` 之前；当指针为长双精度时，`l` 可以位于 `e,f` 和 `g` 之前，且 `L` 同样如此。

- 转换规则，它与一个 `%` 组合，以及一个可选字符 `*`（这将允许 `fscanf(...)` 将结果赋值给参数）、一个可选字符 `h`、`l` 或 `L`（用于目标长度）、一个数字，以及一个转换字符。

- `int scanf(const char *format, ...)`
- 与 `fscanf(stdin, ...)`相同
- `int sscanf(char *str, const char *format, ...)`

- 与 `scanf(...)`相同，但输入来自 `str`。

## 8.2 Termcap 库

### 8.2.1 简介

termcap 库是用于 termcap 数据库的 API，通常位于 `/etc/termcap/`。该库函数允许以下操作：

- 获取当前终端的描述：`tgetent(...)`。
- 搜索描述信息：`tgetnum(...)`、`tgetflag(...)`、`tgetstr(...)`
- 以终端特定的格式编码数值参数：`tparam(...)`、`tgoto(...)`
- 计算并执行填充 `tputs(...)`

使用 termcap 库的程序必须包含 `termcap.h` 并应链接到：

```
gcc [flags] files -ltermcap
```

Termcap 函数是终端无关的程序，但仅为程序员提供对终端的低级访问。对于更高层次的包，应该使用 curses 或 ncurses。

### 8.2.2 查找终端描述

```c
int tgetent(void *buffer, const char *termtype)
```

在 Linux 操作系统上，当前终端名称包含在环境变量 `TERM` 中。因此，`termtype` 是调用 `getenv(3)` 的结果。
对于 `buffer`，在使用 GNU 版本的 termcap 时不需要分配内存。这是我们在 Linux 下可以假设的这一点！否则，你必须分配 2048 字节。（以前 buffer 只需要 1024 字节，但现在大小翻倍了）。

`tgetent(...)` 成功时返回 1，找到数据库但没有 TERM 项时返回 0。其他错误将返回不同的值。
下面的示例将解释如何使用 `tgetent(...)`：

```c
#define 0 char *termtype=getenv("TERM"); int ok;

ok=tgetent(buffer,termtype); 

if(ok==1)

    /* 正确，我们找到了该项 */ 

else if(ok==0)

    /* 哎，TERM 有问题 */

    /* 先检查 termtype，然后检查 termcap 数据库 */

else

    /* 额，致命错误 */
```

默认情况下，termcap 使用 `/etc/termcap/` 作为数据库。如果设置了环境变量 `TERMAP`（例如 `$HOME/termcap`），则所有函数将使用 termcap 而不是 `/etc/termcap`。如果 `TERMAP` 开头没有斜杠，则定义的值被用作终端名称。

### 8.2.3 查看终端描述

每一条信息被称为一个“能力”（capability），每个能力都是两个字母的代码，每个两个字母代码后面都跟着该能力的值。可能的类型有：

- 数值型：例如 `co` – 列数
- 布尔型或标志：例如 `hc` – 硬拷贝终端（hardcopy terminal）
- 字符串：例如 `st` – 设置制表位

每个能力与单一值类型相关。（`co` 始终是数值型，`hc` 始终是标志，`st` 始终是字符串）。有三种不同类型的值，因此也有三个不同的函数来查询它们。`char *name` 是能力的两个字母代码。）

```c
. int tgetnum(char *name)
```

获取数值型的能力值，例如 `co`。如果该能力可用，`tgetnum(...)` 返回该数值，否则返回 1。（注意：返回的值不是负数。）

```c
. int tgetflag(char *name)
```

获取布尔型（或标志）能力值。如果标志存在返回 1，否则返回 0。

```c
. char tgetstr(char *name, char **)
```

获取字符串型的能力值。返回字符串的指针，如果不存在则返回 `NULL`。对于 GNU 版本，如果 `area` 为 `NULL`，termcap 将自行分配内存。Termcap 永远不会再次引用此指针，因此不要忘记在离开程序前释放内存。这种方法是优的，因为你不知道指针需要多少空间，所以让 termcap 为你完成这一切。

```c
char *clstr, *cmstr; int lines, cols;

void term_caps()
{ 
    *tmp;
    clstr=tgetstr("cl",0); /* 清屏 */ 
    cmstr=tgetstr("cm",0); /* 移动 y,x */
    lines=tgetnum("co"); /* 终端行 */ 
    cols=tgetnum("co"); /* 终端列 */
    tmp=tgetstr("pc",0); 
    tmp=tgetstr("cl",0); /* 清屏 */
    tmp=tgetstr("up",0); 
}
```

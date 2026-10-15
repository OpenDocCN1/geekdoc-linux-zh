
> `tty` 指的是由 Teletype 公司制造的原始打印终端。

## 5.5 终端连接的属性

在第一个示例中，我们使用 `stty` 更改用于纠正输入错误的按键。退格键（Backspace）或删除键是典型设置，但你可以将任何字符设置为删除键。在第二个示例中，我们关闭了按键回显。登录输入密码时，按键不会显示在屏幕上。在其他时候，按键会回显到屏幕上。在第三个示例中，我们使用 `stty` 更改驱动设置。

### 5.5.4 终端驱动设置

`stty` 是如何工作的？终端驱动程序包含若干设置。这些设置分为四类：

- `input`（输入）：驱动程序处理来自终端的数据
- `output`（输出）：驱动程序发送到终端的数据
- `control`（控制）：驱动程序处理
- `local`（本地）：驱动程序的操作

输入处理包括小写剥离。输出处理包括换行转换。控制包括偶偶校验、奇数校验位。本地处理包括回显关闭。

### 5.5.5 终端驱动程序编程：函数

库函数 `tcgetattr` 和 `tcsetattr` 提供了对终端驱动程序的访问。这些是：

- (a) 从驱动程序获取属性。
- (b) 修改任何需要的设置。
- (c) 发回驱动程序。

通用步骤如图 5.11 所示：

```
#include <termios.h>
struct termios settings;
tcgetattr(fd, &settings);
tcattr(fd, TCSANOW, &settings);
```

![](img/99837708330d437de319a559cfa6cda7_176_0.png)

图 5.11

使用 `tcgetattr` 和 `tcsetattr` 控制终端驱动程序。

### 5.5.6 终端驱动程序：位

`struct termios` 数据类型包含几个标志位和一个控制字符数组。所有 Unix 版本都包含以下内容：

```
struct termios {
    tc_flag_t c_iflag;      /* 输入模式标志位 */
    tc_flag_t c_oflag;      /* 输出模式标志位 */
    tc_flag_t c_cflag;      /* 控制模式标志位 */
    tc_flag_t c_lflag;      /* 本地模式标志位 */
    cc_t c_cc[NCS];         /* 控制字符 */
    speed_t c_ispeed;       /* 输入速度 */
    speed_t c_ospeed;       /* 输出速度 */
};
```

# 第 5 章 连接控制：学习 stty

流出驱动程序的数据波特率存储在 `c_speed` 和 `c_peed` 成员中。

每个标志集中的单独标志位如图 5.12 所示：

| c_iflag | IMAXOFF | IXOFF | IXANY | IXON | IUCLC | ICNL | INCR | ISTRIP | PARMBK | BRK | IGNBR |
| c_oflag | VTDLY | FDDLY | BSLY | CRDLY | NIDLY | OF | OFILL | ONLRET | OCR | OLUC | OPOST |
| c_cflag | CSIZE | CSTOPB | CREAD | PAREN | PAROD | HUPCL | CLOCAL | CRCTS |
| c_lflag | ISIG | ICAN | PENDIN | TOSTOP | NOFLSH | IEXTEN | ECHON | ECHO | ECHOK | ECHO | FLUSH |
| c_cc | VTIME | VEOL | VMIN | VEOF | VKILL | VERASE | VUIT | VINTER |

> 图 5.12 `termios` 成员中的位和字符。

图中描述的四个成员是标志集。每个标志集包含该组操作位。例如，`c_iflag` 成员包含一个用于值 `INLCR` 的位。`c_cflag` 成员包含用于奇偶校验的位，掩码称为 `PAROD`。这些掩码都定义在 `termios.h` 中。当你从驱动程序读取当前属性到 `termios` 结构体时，该结构体中的所有值都可以被检查和修改。

`c_cc` 是控制字符数组。执行各种控制函数的按键存储在该数组中。数组中的每个位置都由 `termios.h` 中的常量定义。例如，赋值 `attrib.c_cc[VERASE]=\b` 告诉驱动程序将退格键视为擦除字符。

## 5.5 终端连接的属性

## 编写终端驱动程序：位操作

现在我们已经知道如何从驱动程序获取设置以及如何将设置写回驱动程序，让我们来看修改驱动属性的技术。

每个属性都是某个标志集中的一个位。属性的掩码定义在 `termios.h` 中。要测试一个属性，使用该位的掩码对标志集进行掩码操作。要启用该属性，开启该位；要禁用该属性，关闭该位。如下所示：

| 操作 | 代码 |
|---|---|
| 测试一个位 | `if( flagset & MASK ) . .` |
| 设置一个位 | `flagset |= MASK` |
| 清除一个位 | `flagset &= -MASK` |

### 5.5.7 编写终端驱动程序：示例程序

#### 示例：echostate.c - 显示显位状态

我们的第一个示例程序告诉我们终端是否设置为回显字符。我们读取设置，测试一个位并报告结果：

```c
/* echostate.c
* 报告 fd 0 的 tty 驱动中显位的当前状态
* 显示如何从驱动程序读取属性并测试位
*/

#include <stdio.h>
#include <termios.h>

main() {
    struct termios info;
    int rv;

    rv = tcgetattr(0
```

该程序读取文件描述符 `0` 的终端属性。`0` 是标准输入的文件描述符，通常连接到键盘的文件描述符。这里是该程序的编译和运行示例：

```
$ cc echostate.c -o echostate
./echostate
echo is on , since its bit is 1
$ stty -echo
$ ./echostat: not found
$ echo is OFF, since its bit is 0
```

示例显示命令 `stty -echo` 禁用了驱动中的按键回显。用户随后又输入了两个命令，但这些命令没有显示在屏幕上。另一方面，响应这两行输入的输出确实出现了。

#### 示例：setecho.c - 更改显位状态

我们的第二个示例程序开启或关闭键盘回显。如果命令行参数以 "y" 开头，则开启终端的回显标志位。否则，关闭回显。程序如下：

```c
/* setecho.c
 * 用法: setecho [n]
 * 显示: 如何读取、更改、重置 tty 属性
 */

#include <stdio.h>
#include <termios.h>

#define oops(s,x) ( perror(s); exit(x); )

main(int ac, char *av[])
{
    struct termios info;

    if (ac == 1)
        exit(0);

    if (tcgetattr(0,&info) == -1)    /* 获取属性 */
        oops("tcgetattr",1);

    if (av[1][0] == 'y')
        info.c_cflag |= ECHO;           /* 开启位 */
    else
        info.c_cflag &= ~ECHO;          /* 关闭位 */

    if (tcsetattr(0,TCSANOW,&info) == -1) /* 设置属性 */
        oops("tcsetattr",2);

}
```

我们测试并运行了两个程序以及普通的 `stty`：

```
$ echostate; setecho n; echostate ; stty echo
echo is on, since its bit is 1
echo is OFF, since its bit is 0
$ stty -echo; echostate ; setecho y
echo is OFF, since its bit is 0
```

在第一个命令中，我们使用了 `setecho` 来关闭。然后我们使用 `stty` 开启回显。驱动和设置存储在内核中，而不是进程中。一个进程可以更改设置，另一个进程可以读取或更改。

#### 示例：showtty.c - 显示多个属性

我们可以重复 `setecho.c` 和 `echostate.c` 中的技术来构建一个完整的 `stty`。`tty` 驱动包含三种设置：特殊字符、数值和位。以下代码包含显示这些类型数据的函数：

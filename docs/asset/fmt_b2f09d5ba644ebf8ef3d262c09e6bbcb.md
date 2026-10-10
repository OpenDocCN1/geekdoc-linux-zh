
```c
#include <stdio.h>
#include <unistd.h>

char *menu[] = {
  "a add record",
  "d delete record",
  "q quit",
  NULL,
};

getchoice(char *greet, char *choices[], FILE *in, FILE *out);

main()
```

176

```c
{
int choice = 0;
FILE *input;
FILE *output;

if(!isatty(fileno(stdout))) {
    fprintf(stderr,"You are not a terminal, OK.\n");
}

input = fopen("/dev/tty", "r");
output = fopen("/dev/tty", "w");
if(!input || output) {
    fprintf(stderr,"Unable to open /dev/tty\n");
    exit(1);
}
do {
    choice = getchoice("Please select an action", menu, input, output);
    printf("You have chosen: %c\n", choice);
} while(choice != 'q');
exit(0);
}

int getchoice(char *greet, char *choices[], FILE *in, FILE *out) {
    int chosen = 0;
    int selected;
    char *option;

do {
        fprintf(out,"Choice: %s\n",greet);
        option = choices;
        while (*option) {
            fprintf(out,"%s\n",*option);
            option++;
        }
        do {
            selected = fgetc(in);
        } while (selected == '\n');
        option = choices;
        while (*option) {
            if (selected == *option[0]) {
                chosen = 1;
                break;
            }
            option++;
        }
        if(!chosen) {
            fprintf(out,"Incorrect choice, select again\n");
        }
    } while(!chosen);
    return selected;
}
```

# 第5章

现在，当我们在重定向输出的情况下运行程序时，我们仍然可以看到提示信息，并且正常的程序输出是分开的。

```
$ menu3 > file
You are not a data terminal, OK.
Choice: Please select an action
a - add new record
d - delete record
q - quit
Choice: Please select an action
a - add new record
d - delete record
q - quit

$ cat file
You have chosen: d
You have chosen: q
```

# 终端驱动程序与通用终端接口

有时，程序对终端需要更精细的控制，这是通过简单的文件操作无法实现的。`Linux` 提供了一组接口，允许我们控制终端驱动程序的行为，从而让我们对终端输入输出的处理获得更大的控制权。

## 概述

如图 5-1 所示，我们可以通过一组函数调用（通用终端接口，简称 `GTI`）来控制终端。这保持了数据（读/写）接口的简洁，同时允许对终端行为进行详细控制。这并不是说终端 `I/O` 接口是简洁的——它必须处理各种不同的硬件。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_219_0.png)

图 5-1

## 终端

在 `UNIX` 术语中，控制接口设置了一个“行规范”（line discipline），允许程序在指定终端驱动程序的行为时具有相当的活性。

我们可以控制的主要特征有：

- 行编辑：选择是否允许使用退格键（Backspace）编辑。

- 缓冲：选择是立即读取字符，还是在可配置的延迟后读取。

- 回显（Echo）：允许我们控制回显，例如在读取密码时。

- `CR/LF`：确定输入和输出的映射：当你打印一个 `\n` 时会发生什么。

- 线路速率：在 `PC` 控制台上很少使用，但对于串口线上的调制解调器和终端来说非常重要。

# 硬件模型

在详细查看通用终端接口之前，理解它旨在驱动的硬件模型是非常重要的。

图 5-2 所示的逻辑安排（对于某些 `UNIX` 站点，物理上也将是这样的）是让 `UNIX` 机器通过串口端口连接到调制解调器，然后通过电话线和另一个调制解调器连接到远程终端。事实上，这是一些小型互联网服务提供商（`ISP`）使用的设置。它是客户端/服务器范式的远亲，用于程序在主主机上运行而用户在哑终端上工作的场景。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_220_0.png)

图 5-2

179

如果你在运行 `Linux` 的 `PC` 上工作，这看起来可能是一个过于复杂的模型。然而，由于两位作者都有调制解调器，如果我们选择的话，我们可以使用像 `minicom` 这样的终端仿真程序，通过一对调制解调器和一条电话线在对方的机器上运行远程登录会话。

使用这种硬件模型的优势是，大多数现实情况将是这个最复杂情况的子集。支持这些情况将比模型忽略此类功能要容易得多。

# termios 结构体

`termios` 是 `POSIX` 指定的标准接口，与 `System V` 的接口 `termio` 类似。终端接口通过设置 `termios` 类型结构体中的值并使用一组较小的函数调用来控制。两者都定义在头文件 `termios.h` 中。

> 带有 `termios.h` 中定义的函数调用的程序需要与适当的函数库链接。这通常是 `curses` 库，因此在编译本章中的示例时，你需要在编译器命令末尾添加 `-lcurses`。在某些较旧的 `Linux` 系统上，`curses` 库是由名为“new curses”或 `ncurses` 的版本提供的。在这种情况下，库名和链接参数分别变为 `-lncurses`。

用于影响终端的可操作值分为各种模式：

- 输入（Input）

- 输出（Output）

- 控制（Control）

- 本地（Local）

- 特殊控制字符（Special control characters）

最小的 `termios` 结构体通常声明如下（尽管 `X/Open` 规范允许包含额外的字段）。

```c
#include <termios.h>
struct termios {
    tc_flag_t c_iflag;
    tc_flag_t c_oflag;
    tc_flag_t c_cflag;
    tc_flag_t c_lflag;
    cc_t      c_cc[NCCS];
```

成员名称与上列表中列出的五种参数类型对应。

180

我们可以通过调用函数 `tcgetattr` 来为终端初始化 `termios` 结构体，其原型如下：

```c
#include <termios.h>

int tcgetattr(int fd, struct termios *ter_p);
```

此函数将终端接口变量的当前值调入 `ter_p` 指向的结构体中。如果随后更改了这些值，我们可以使用 `tcsetattr` 函数重新配置终端接口，如下：

```c
#include <termios.h>

int tcsetattr(int fd, int actions, const struct termios *ter_p);
```

`tcsetattr` 的 `actions` 控制更改如何应用。三种可能性是：

- `TCSANOW`：立即更改值。

- `TCSRAIN`：在输出完成后更改值。

- `TCSFLUSH`：在输出完成后更改值，并丢弃任何尚未返回的输入。

> 保存和恢复这些设置始终是程序的责任。

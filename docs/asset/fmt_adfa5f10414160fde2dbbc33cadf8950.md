
`c_iflag` 成员控制输入处理选项。它影响终端驱动程序在将输入发送到程序之前如何处理输入。`c_oflag` 成员控制输出处理，并决定终端驱动程序在将输出发送到屏幕或其他输出设备之前如何处理输出。决定终端设备硬件特性的各种控制标志设置在 `c_cflag` 成员中。存储在 `c_lflag` 中的本地标志操作终端特性，例如输入字符是否在屏幕上回。`c_cc` 数组包含了特殊字符序列（如 ^C (退出) 和 ^H (删除)）的值以及它们的行为。`c_line` 成员指示控制协议，例如 SLIP、PPP 或 X.25 —— 我们将不会讨论这个成员，因为它的用法超出了本书的涉及范围。

终端以两种模式之一运行：规范模式（或称为“熟热”模式，cooked mode），在该模式下，终端驱动程序处理特殊字符并一次一行将输入输入程序；以及非规范模式（原始模式，raw mode），在该模式下，键盘输入是不处理且不缓冲的。这是一个使用规范模式的应用示例。另一方面，屏幕编辑器 v1 使用非规范模式；v1 按原接收输入。

表 26.1 终端控制常用的标志

| 标志 | 成员 | 描述 |
|---|---|---|
| IGNBRK | c_iflag | 忽略 BREAK（中断信号）。 |
| BRKINT | c_iflag | 发生 BREAK 时产生 SIGINT。 |
| INLCR | c_iflag | 将 NL 转换为 CR。 |
| IGNCR | c_iflag | 输入时忽略 CR。 |
| ICRNL | c_iflag | 将 CR 转换为 NL。 |
| IXON | c_iflag | 启用输入字符控制。 |
| ONL | c_oflag | 将 NL 转换为输出。 |
| OPOST | c_oflag | 后处理输出。 |
| ONCR | c_oflag | 将 CR 转换为 NL。 |
| INCR | c_oflag | 将 CR 转换为 NL。 |
| KIP | c_oflag | 将输出转换为 CR。 |
| IXOFF | c_oflag | 启用输出字符控制。 |
| HUPCL | c_cflag | 关闭连接。 |
| CLOCAL | c_cflag | 本地设备。 |
| ICANON | c_lflag | 启用规范模式。 |
| ECHO | c_lflag | 回显输入字符。 |
| ECHOONL | c_lflag | 在规范模式下回显。 |

控制字符数组 `c_cc` 包含了至少十一个特殊字符，如 ^D EOF、^C INTR 和 ^U KILL。这十一个中有九个可以更改。CR 始终。

## 属性控制函数

`termios` 接口包含了控制特性的函数。基本函数是 `tcgetattr()` 和 `tcsetattr()`。`tcgetattr()` 初始化 `termios` 数据结构，设置终端特性。查询和更改这些设置意味着操作数据结构。完成后，使用 `tcsetattr()` 更新终端。`tcgetattr()` 和 `tcsetattr()` 的原型在下文中解释。

```c
int tcgetattr(int fd, struct termios *tp);
```

`tcgetattr()` 查询与文件描述符相关的参数，并存储在 `tp` 指向的 `termios` 结构中。成功返回 0，错误返回 -1。

```c
int tcsetattr(int fd, int action, struct termios *tp);
```

`tcsetattr()` 使用 `tp` 指向的 `termios` 结构设置与文件描述符相关的参数。`action` 参数控制更改何时生效，使用以下值：

- `TCSANOW` 立即更改。
- `TCSASAIN` —— 在所有输出发送到终端后更改。更改输出设置时使用此函数。
- `TCSAFLUSH` —— 在所有输出发送到终端后更改，但丢弃任何等待的输入。

## 速度控制函数

第一个函数设置终端设备的输入和输出速度。由于接口很老，它以波特率（baud）定义速度，尽管正确的术语是每秒比特（bps）。这些函数成对出现，一组用于获取和设置输出速度，另一组用于获取和设置输入速度。它们在 `<termios.h>` 头文件中声明的原型列如下，并附有行为的简短描述。

```c
int cfgetspeed(struct termios *tp);
```

`cfgetspeed()` 返回 `tp` 指向的 `termios` 结构中存储的输入行速度。

```c
int cfsetspeed(struct termios *tp, speed_t speed);
```

`cfsetspeed()` 设置 `tp` 指向的 `termios` 结构中存储的输入行速度 `speed`。

## 用户界面的编程

`cfgetpeed()` 返回存储在由 `tp` 指向的 `termios` 结构体中的输出行速率。

```c
int cfsetpeed(struct termios *tp, speed_t speed);
```

`cfsetpeed()` 将由 `tp` 指向的 `termios` 结构体中的输出行速率设置为 `speed`。

`speed` 参数必须是以下常量之一：

- `B0`（关闭连接） `B1800`
- `B50` `B2400`
- `B75` `B4800`
- `B110` `B9600`
- `B134` `B19200`
- `B150` `B38400`
- `B200` `B57600`
- `B300` `B115200`
- `B600` `B230400`

## 行控制函数

行控制函数查询并设置与数据如何、何时以及是否流向终端设备的各种属性。这些函数允许你对终端设备的行为进行细粒度的控制。例如，要在继续执行之前强制完成所有待处理的输出，可以使用 `tcdrain()`，其原型定义如下：

```c
int tcdrain(int fd);
```

`tcdrain()` 等待所有输出都已写入文件描述符 `fd` 后才返回。

要强制刷新输出、输入或两者，请使用 `tcflush()` 函数。其原型定义如下：

```c
int tcflush(int fd, int queue);
```

`tcflush()` 刷新队列到文件描述符 `fd` 的输入、输出（或两者）。`queue` 参数指定要刷新的数据，列表如下：

- `TCIFLUSH`—刷新已接收但未读取的输入数据。
- `TCFLUSH`—刷新已写入但未传输的输出数据。
- `TCIOFLUSH`—刷新已接收但未读取的输入数据以及已写入未发送的输出数据。

## 终端控制

# 第 26 章

实际的流控制（无论开启还是关闭）都是通过 `tcflow()` 函数控制的，原型定义如下：

```c
int tcflow(int fd, int action);
```

`tcflow()` 根据 `action` 的值启动或停止文件描述符 `fd` 上的数据传输或接收：

- `TCOON`—启动输出
- `TCOFF`—停止输出
- `TCION`—启动输入
- `TCIOFF`—停止输入

## 进程控制函数

`termios` 接口定义的进程控制函数允许你获取运行在终端上的进程（程序）的信息。获取这些信息的关键是进程组。例如，要找到给定终端上的进程组号，可以使用 `tcgetpgrp()`，其原型定义如下：

```c
pid_t tcgetpgrp(int fd);
```

`tcgetpgrp()` 返回在文件描述符 `fd` 上打开终端的前台进程组 `pgrp_id` 的组 ID，出错时返回 -1。

如果你的程序具有足够的访问权限（等同于 root），可以使用 `tcsetpgrp()` 更改进程组标识符。其原型定义如下：

```c
int_t tcsetpgrp(int fd, pid_t pgrp_id);
```

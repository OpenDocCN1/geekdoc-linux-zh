
- `/dev/lp0` - `/dev/lpn` 这些是并行设备 0-n，其中 `n` 取决于你的硬件。
- `/dev/js0` - `/dev/jsn` 这些是摇杆设备 0-n，其中 `<= n <= 1`。

`/dev/ttyS*` 和 `/dev/cua*` 设备之间的区别在于，调用 `open()` 时被预期用作切出设备，因此通过 `open()` 获取默认设置，而 `/dev/ttyS*` 设备则将为拨入和拨出调用进行初始化。默认情况下，这些设备是打开它们的进程的控制设备。普通请求应该处理这些特殊设备，POSIX 倾向于定义新函数来处理异步终端，这很大程度上取决于严格的术语。两种方法都需要包含 `<termios.h>`。

```
method ioctl:
```

`TCSBRK`, `TCSBRKP`, `TCGETA` (获取属性), `TCSETS` (设置属性) 终端 I/O 控制 (`TIOC`) 请求：`TIOCSOFTCAR` (设置载波), `TIOCSOFTCAR` (获取载波), `TIOCSCTTY` (设置控制终端), `TIOCGET` (获取调制器行), `TIOCSET` (设置调制器行), `TIOCGSERIAL`, `TIOCSERIAL`, `TIOCSERCONFIG`, `TIOCSERGWILD`, `TIOCSERSWILD`, `TIOCSTRUCT`, `TIOCMBIS`, `TIOCMIC`, ... `method POSIX`: `tcgetattr()`, `tcsetattr()`, `tcbreakbreak()`, `tdrain()`, `tcflush()`, `tcflow()`, `tcgetgrp()`, `cfetspeed()`, `cfetspeed()`, 其他方法: `outb`, `infb` 用于靠近编程的硬件，如打印机端口，而不是打印机。

## 第 9 章 I/O 端口编程

### 9.1 鼠标编程

鼠标要么连接到串口，要么连接到并行接口。这些接口是特殊设备，映射方式如下：

- `/dev/ttyS0` - `/dev/ttySn` 这些是 RS232 串口设备 0-n，其中 `n` 取决于你的硬件。
- `/dev/cua0` - `/dev/cuan` 这些是 RS232 串口设备 0-n，其中 `n` 取决于你的硬件。
- `/dev/lp0` - `/dev/lpn` 这些是并行设备 0-n，其中 `n` 取决于你的硬件。
- `/dev/js0` - `/dev/jsn` 这些是摇杆设备 0-n，其中 `<= n <= 1`。

`/dev/ttyS*` 和 `/dev/cua*` 设备之间的区别在于，调用 `open()` 时被预期用作切出设备，因此通过 `open()` 获取默认设置，而 `/dev/ttyS*` 设备则将为拨入和拨出调用进行初始化。默认情况下，这些设备是打开它们的进程的控制设备。普通请求应该处理这些特殊设备，POSIX 倾向于定义新函数来处理异步终端，这很大程度上取决于严格的术语。两种方法都需要包含 `<termios.h>`。

```
method ioctl:
```

`TCSBRK`, `TCSBRKP`, `TCGETA` (获取属性), `TCSETS` (设置属性) 终端 I/O 控制 (`TIOC`) 请求：`TIOCSOFTCAR` (设置载波), `TIOCSOFTCAR` (获取载波), `TIOCSCTTY` (设置控制终端), `TIOCGET` (获取调制器行), `TIOCSET` (设置调制器行), `TIOCGSERIAL`, `TIOCSERIAL`, `TIOCSERCONFIG`, `TIOCSERGWILD`, `TIOCSERSWILD`, `TIOCSTRUCT`, `TIOCMBIS`, `TIOCMIC`, ... `method POSIX`: `tcgetattr()`, `tcsetattr()`, `tcbreakbreak()`, `tdrain()`, `tcflush()`, `tcflow()`, `tcgetgrp()`, `cfetspeed()`, `cfetspeed()`, 其他方法: `outb`, `infb` 用于靠近编程的硬件，如打印机端口，而不是打印机。

## 第 10 章

## 应用程序到 Linux 的迁移

Matt Welsh

`mdw@cs.cornell.edu` 1995年1月26日

### 10.1 引言

将 Unix 应用程序移植到 Linux 系统非常容易。Linux 以及其所使用的 GNU C 库在设计时考虑了应用程序的可移植性，这意味着许多应用程序只需通过 `make` 即可编译。那些复杂的应用程序通常使用了某些特定实现的晦涩特性，或者强烈依赖于未记录或未定义的行为。

Linux 基本上符合 IEEE Std 103.1-1988 (POSIX.1)，但尚未正式获得该认证。同样，Linux 也实现了许多在 SVID 和 BSD 系列中找到的功能，但再次并非在所有情况下都遵循它们。总的来说，Linux 的设计旨在与其他 Unix 实现兼容，方便应用程序迁移，并在许多情况下改进或纠正了这些实现中的行为。

例如，传递给 `select` 系统调用的超时参数在 Linux 的执行期间实际上被减少了。没有预期这种情况的应用程序在 Linux 下编译时会出现问题。

本文旨在概述在迁移到 Linux 时遇到的主要问题，并强调了 Linux、POSIX.1、SVID 和 BSD 在以下领域的差异：

## 10.2 信号处理

长期以来，信号的定义和语义一直对不同的 Unix 实现进行了多种修改。今天，信号分为两大两类：不可靠信号和可靠信号。不可靠信号是指在调用后其信号处理器不会保持安装状态的信号。这些“一次性”信号必须在信号处理器内部重新安装信号处理器。...

如果程序希望信号保持已安装状态。由于此，会存在一种竞态条件：在处理程序安装之前，信号可能会再次到达，这可能导致信号丢失或触发信号的原始行为（例如杀死进程）。因此，这些信号是“不可靠的”，因为信号捕获和处理程序程序的操作的操作是非原子的。

在不可靠的语义下，系统调用在被信号中断时不会自动重启。因此，为了让程序能够处理所有情况，程序需要在每次系统调用后检查 `errno` 的值，如果其值为 `EINTR`，则重新发出该系统调用。

类似地，不可靠的信号语义没有提供一种简单的方法来实现原子暂停操作（让进程进入睡眠状态直到信号到达）。由于重新安装信号处理器的不可靠性，在某些情况下，信号可能会到达而程序却无法察觉。

相反，在可靠的信号语义下，信号处理器在调用后保持不变，从而避免了重新安装的竞态条件。此外，某些系统调用可以重启，并且通过 POSIX `sigpend` 函数提供了原子暂停操作。

### 10.2.1 SVR4、BSD 和 POSIX.1 下的信号

SVR4 的信号实现包含了 `signal`、`sigset`、`sighold`、`sigelse`、`sigignore` 和 `sigpause` 函数。SVR4 下 `signal` 函数与经典的 UNIX V7 信号相同，仅提供不可靠信号。其他函数提供了自动重新安装信号处理器的信号，但不支持系统调用重启。

在 BSD 下，支持 `signal`、`sigvec`、`sigblock`、`sigsetmask` 和 `sigpause` 函数。所有函数默认都提供系统调用重启的可靠信号，但程序员可以根据意愿禁用该行为。

在 POSIX.1 下，提供了 `sigaction`、`sigprocmask`、`sigpending` 和 `sigsuspend`。注意这里没有 `signal` 函数，且根据 POSIX.1 它已被弃用。这些函数提供了可靠信号，但 POSIX 未定义系统调用重启。如果在 SVR4 和 BSD 下使用 `sigaction`，系统调用重启默认是禁用的，但如果指定标志 `SASTART` 则可以开启。

因此，在程序中使用信号的“最佳”方法是使用 `sigaction`，它允许你显式指定信号处理器的行为。

然而，许多应用程序仍然在使用 `signal`，正如我们上面看到的，`signal` 在 SVR4 和 BSD 下提供了不同的语义。

### 10.2.2 Linux 信号选项

Linux 定义了 `sigaction` 结构中 `saflags` 成员的以下值：

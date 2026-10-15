

```
speed = INITIAL_SPEED ;

/* Start the real time interval timer with delay interval size */
set_timer( ITIMER_REAL, 1000/speed, 1000/speed );

/* main processing loop omitted but would be here */
endwin();
return 0;
}
```

## 6.12 非轮询输入

bouncestr.c 程序使用定时器生成中断来更新屏幕，但它通过本质上是轮询循环的方式获取用户输入：主程序反复轮询终端以获取输入。如果 CPU 不会被其他进程使用，或者程序在主循环中没有其他任务要执行，这种做法是可以的，但这是一种低效的检查输入可用性的方法，而在处理器的生命周期中，输入发生的频率极低。我们应该对程序成为 CPU 占用大户的想法感到不满，即使每次调用 getch() 检查用户输入时进程都被阻塞，程序也卡在轮询 I/O 循环中。进程基本上反复调用 getch()、阻塞、在用户输入时被唤醒、做一点工作然后再次阻塞。如果程序的输入部分也是信号驱动的会更高效，这意味着程序会要求内核在输入可以传递给它时通知它，也许是通过信号处理机制。在这种情况下，程序基本上处于空闲状态，等待任何信号的到来，要么是定时器更新屏幕的信号，要么是内核因为输入可用而发出的信号。

非轮询输入有两种不同类型：信号驱动和异步。要理解它们之间的区别，重要的是要知道输入首先从设备移动到内核地址空间中的缓冲区，然后再移动到进程的地址空间。

- 在信号驱动 I/O 中，程序告诉内核在输入被放置到内核地址空间后通知它。一旦进程被通知输入已在内核地址空间中，如果它发出 read() 系统调用，因为数据立即可用，所以它不会阻塞。换句话说，在进程被通知后执行的 read() 被保证会立即返回数据。
- 在异步 I/O 中，进程告诉内核在输入从设备移动到内核地址空间然后再移动到进程地址空间中的缓冲区后通知它。在这种 I/O 类型中，当进程收到信号时，read() 已经执行，并且用户进程已经拥有数据，但不一定在它必须进入的内存位置中。

信号驱动 I/O 在 UNIX 中可通过在文件描述符中设置 O_ASYNC 标志然后建立适当的信号来实现。异步 I/O 可通过 POSIX 异步 I/O 接口 AIO 获得。令人困惑的是，启用信号驱动 I/O 的标志被称为 O_ASYNC。我们将首先通过修改 bouncestr.c 程序来探索信号驱动 I/O。然后我们将创建一个使用 AIO 接口的异步 I/O 的 bouncestr.c 程序版本。

### 6.12.1 使用 O_ASYNC 标志的非轮询 I/O

当你在文件描述符上设置 O_ASYNC 标志时，它会导致来自该描述符文件连接的输入被部分异步传递。准确地说，这意味着当设备上有输入可用时，内核会将其复制到内核地址空间中的位置，之后内核会向进程发送 SIGIO 信号。要通过此方法设置信号驱动输入，程序必须执行以下操作：

- 1. 通过调用

      fcntl(F_SETOWN, getpid());

告诉内核在数据准备好读取时应向哪个进程发送 SIGIO 信号。

SETOWN 操作使第二个参数中的进程 ID 成为要接收的信号的所有者。通常程序希望接收信号本身，因此它使用 getpid() 调用此操作。

- 2. 使用以下命令检索标准输入设备的现有标志

      fcntl(0, F_GETFL);

- 3. 使用以下命令在连接上设置 O_ASYNC 标志

      fcntl(0,F_SETFL,(fd_flags|O_ASYNC));

- 4. 假设 on_input() 是将处理 SIGIO 信号的函数，注册该信号处理程序：

```
struct sigaction newhandler;
sigset_t          blocked;
newhandler.sa_handler = on_input;
newhandler.sa_flags = SA_RESTART;
sigemptyset(&blocked);
newhandler.sa_mask = blocked;
sigaction(SIGIO, &newhandler, NULL);
```

on_input() 处理程序可以调用 NCurses getch() 函数，并且保证会收到用户输入的单个字符。这样它就不必在循环中执行阻塞读取，而可以在循环中做其他事情。

所有这些都放在程序 bouncestr_async.c 中。上述前三步可以放在名为 enable_keybd_signals() 的函数中：

```
void enable_keybd_signals()
{
    int fd_flags;

    fcntl(0, F_SETOWN, getpid());
    fd_flags = fcntl(0, F_GETFL);
    fcntl(0, F_SETFL, (fd_flags|O_ASYNC));
}
```

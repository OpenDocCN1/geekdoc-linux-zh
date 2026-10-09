

```c
(void)initscr();
ec_ERR(raw());
while (true) {
    ec_ERR(clear());
    ec_ERR(mvwaddstr(2, 9, "What do you want to do?"));
    ec_ERR(mvwaddstr(3, 9, "1. Check out tape/DVD"));
    ec_ERR(mvwaddstr(4, 9, "2. Reserve tape/DVD"));
    ec_ERR(mvwaddstr(5, 9, "3. Register new member"));
    ec_ERR(mvwaddstr(6, 9, "4. Search for title/actor"));
    ec_ERR(mvwaddstr(7, 9, "5. Quit"));
    ec_ERR(mvwaddstr(9, 9, "(Type item number to continue)"));
    ec_ERR(c = getch());
    switch (c) {
        case '1':
        case '2':
        case '3':
        case '4':
            ec_ERR(clear());
            snprintf(s, sizeof(s), "You typed %c", c);
            ec_ERR(mvwaddstr(4, 9, s));
            ec_ERR(mvwaddstr(9, 9, "(Press any key to continue)"));
            ec_ERR(getch());
            break;
        case '5':
            ok = true;
            EC_CLEANUP;
        default:
            ec_ERR(beep());
    }
}

EC_CLEANUP_BGN
(void)clear();
(void)refresh();
(void)endwin();
exit(ok ? EXIT_SUCCESS : EXIT_FAILURE);
EC_CLEANUP_END
```

关于此程序的几点说明：

- 大多数 Curses 函数在出错时会返回 ERR，因此我专门针对它们定义了一个 **ec_ERR** 宏。Curses 的文档并未说明它使用 errno，但我保留了原样，因为我知道如果确实获取到一条消息，其值可能没有意义。
- Curses 要求以 **initscr** 开始，并以 **endwin** 结束。
- **tc_setraw** 的 Curses 版本是 **raw**。

本书中不再涉及 *Curses* 的其他内容，因为它不是内核服务。$^{10}$

*Curses* 是 SUS2 和 SUS3 的一部分，因此你可以在 SUS2 网站 www.unix-systems.org/version2/online.html 上在线阅读规范。在大多数系统上，你也可以输入 `man curses` 或 `man ncurses`（*Curses* 的一个免费版本）。

### 4.9 STREAMS I/O

STREAMS 是一些 UNIX 实现中的一种机制，允许以模块化方式实现字符设备驱动程序。应用程序可以在一定程度上将各种 STREAMS 模块串联起来，以获得所需的驱动程序功能。这在某种程度上类似于 UNIX 过滤器在 shell 层面的工作方式；例如，`who` 命令可能没有排序输出的选项，但如果你想要的话，可以通过管道将其输入到 `sort` 中。

我将在下一节中展示一个基于 STREAMS 的伪终端示例。在那里我将做的是 `open` 一个设备文件以获取伪终端，然后使用 `ioctl` 将两个 STREAMS 模块（`ldterm` 和 `ptem`）“推送”到该模块上，使其表现得像一个终端。与 shell 管道不同，在 shell 管道中你可以从数十种过滤器中选择，并以数百种创造性的方式组合它们；STREAMS 模块通常以配方式（cookbook fashion）方式使用——你推送文档告诉你需要推送的模块，并且就像烹饪一样，如果你随意推送东西，不会得到任何美味的结果。（不应将 STREAMS 与标准 I/O 流概念混淆，后者用于 `fopen`、`fwrite` 等。两者完全没有关系。）

SUS1 和 SUS2 要求具备 STREAMS 功能，但 SUS3 并不要求。将 `_XOPEN_VERSION` 设置为 500（表示它是 SUS2）的 Linux 不提供 STREAMS，因此从某种意义上说它是非符合标准的。

除了我在下一节中使用 STREAMS 进行伪终端以及本书中的其他几处提及之外，我将不会全面介绍 STREAMS。了解更多关于它们的最好方法是参考 SUS 或 Sun 的网站 www.sun.com，在那里你可以找到 *STREAMS Programming Guide*。

> 10. 此外，如果我们包含 *Curses*，我们就必须包含 X，而那会要我们的命。（在此语境中，“我们”指的是“你和我”。）

### 4.10 伪终端

正常的终端设备驱动程序将进程连接到实际的终端，如图 4.5a 所示，其中终端处的用户正在运行 vi。伪终端设备驱动程序对于交互式（从属）进程（vi）而言表现得与终端完全一样，但另一端连接的是主进程，而不是实际设备。这允许主进程将输入提供给从属进程，就好像输入来自实际终端一样，并捕获从属进程的输出，就好像输出要去往实际终端一样。从属进程可以像往常一样使用 tcgetattr、tcsetattr 和其他仅限终端的系统调用，并且它们都将按预期工作。

![](img/41b4c8f6d6a5c349eee321a301703d97_270_0.png)

a) 连接到终端的 tty 驱动程序

b) 连接到进程的 pty 驱动程序

图 4.5 终端驱动程序与伪终端驱动程序。

你可以将伪终端连接到进程的概念类比为通过 shell 重定向其输入和输出，但使用的是某种终端而不是管道。事实上，vi 无法使用管道：

```sh
$ vi >tmp
ex/vi: Vi's standard input and output must be a terminal
```

伪终端最常见的用途之一是由 telnetd 服务器使用，如图 4.6 所示。它通过网络与 telnet 客户端通信，并通过伪终端与 telnet 用户执行的操作进行通信。在实践中，telnet 会话通常以 shell 开始，就像实际终端会话一样；在

![](img/41b4c8f6d6a5c349eee321a301703d97_271_0.png)

图 4.6 由 telnet 服务器（telnetd）使用的伪终端。

图中，$vi$ 正在运行，因为用户向 shell 输入了 $vi$ 命令。事实上，如今使用 telnet 或 $xterm$ 比使用实际终端更为常见，因为大多数用户通过网络而不是直接拨号连接 UNIX 计算机。（他们可能拨号连接互联网服务提供商（ISP），但这只是为了让他们进入互联网。）我不会展示如何实现 telnetd 服务器（参见练习 4.6）；我们只关注图中的伪终端部分。

在伪终端的主侧，主进程获取从属进程写入的内容。在 $vi$ 和其他面向屏幕的程序的情况下，这些数据包括转义序列（例如，用于清屏），如我们在 4.8 节中所见。终端驱动程序或伪终端驱动程序都关心这些序列是什么。另一方面，使用 $tcsetattr$ 执行的控制操作完全由驱动程序处理，不会到达主进程。因此，在图 4.6 中，$vi$ 生成的转义序列一直传输到左侧计算机上运行的 telnet 进程。如果它在全屏模式下运行，它可以将其直接发送到实际终端。更常见的是，telnet 进程根本不连接到终端驱动程序，而是运行在窗口系统下。在这种情况下，它必须知道如何将这些转义序列转换为窗口系统显示窗口中字符所需的内容。这样的程序被称为*终端模拟器*。因此，请记住终端模拟器和伪终端是两件非常不同的事情：前者处理转义序列，后者替代终端驱动程序，以便将 I/O 重新路由到主进程。

#### 4.10.1 伪终端库

> 由于本节使用了一些第 5 章中的系统调用（例如 fork），你可能希望在阅读完该章之后再阅读本节。

伪终端（从现在起称为“pty”），像所有其他设备一样，由特殊文件表示，其名称因系统而异。不幸的是，将进程连接到 pty 并不像执行以下操作那样简单直接：

```sh
$ vi </dev/pty/01 > /dev/pty/01
```

它更复杂：我们必须获取 pty 的名称，执行一些系统调用来准备它，并将其设置为控制终端。其中一些系统调用由 SUS1（1.5.1 节）及后续标准标准化，但诸如 FreeBSD 等 pre-SUS 系统以完全不同的方式处理此事。更糟糕的是，使用 STREAMS 实现 ptys 的系统需要额外的步骤，并且 SUS2 和 SUS3 之间发生了一些变化。

我将把系统之间的差异封装到一个小型函数库中，每个函数都以 pty_ 开头。然后，我将使用这个 pty 库来实现一个记录/播放应用程序作为示例。

以下是使用 ptys 的总体方案，分为九个步骤：

- 1. 打开 pty 的主侧以进行读写。
- 2. 获取对 pty 的访问权限（如下文所述）。
- 3. 从主侧的名称或文件描述符获取从侧的名称。暂时不要打开它。
- 4. 执行 fork 系统调用（5.5 节）以创建子进程。
- 5. 在子进程中，调用 setsid（4.3.2 节）使其放弃其控制终端。
- 6. 在子进程中，打开 pty 的从侧。它将变成新的控制终端。在支持 STREAMS 的系统（例如 Solaris）上，你必须设置 STREAM。在 BSD 系统上，你必须显式使用以下命令使其成为控制终端：
    ```c
    ec_neg1(ioctl(fd, TIOCSCTTY));
    ```
- 7. 将子进程的标准输入、输出和错误文件描述符重定向到 pty。


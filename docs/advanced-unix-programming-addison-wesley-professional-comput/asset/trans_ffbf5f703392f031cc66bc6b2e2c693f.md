
## 4.2 从终端读取

本节解释了如何从终端读取数据，包括当终端没有就绪读取的数据时，如何避免被阻塞。

### 4.2.1 正常终端 I/O

我将首先解释正常的终端输入和输出是如何工作的；也就是说，当你首次登录且尚未使用 `stty` 命令按个人喜好进行自定义之前，它们的工作方式。随后，在后续章节中，我将展示如何调用 `fcntl` 和 `tcsetattr` 系统调用以改变正常行为。

访问终端进行输入或输出有三种方式：

1. 你可以打开字符特殊文件 `/dev/tty` 进行读取、写入，或者最常见的是两者兼有。这个特殊文件是进程的**控制终端（controlling terminal）**的同义词（参见第 4.3.1 节）。
2. 如果你知道特殊文件的实际名称（例如 `/dev/tty04`），你可以直接打开它。如果你只需要控制终端，使用通用名称 `/dev/tty` 并没有任何劣势。在应用程序中，它主要用于访问除控制终端以外的其他终端。
3. 按照惯例，每个进程继承三个已经打开的文件描述符：标准输入、标准输出和标准错误输出。这些描述符可能指向也可能不指向控制终端，但通常无论如何都应该使用它们，因为如果它们指向的是普通文件或管道，那是因为用户或父进程决定重定向输入或输出。

终端的基本 I/O 系统调用是 `open`、`read`、`write` 和 `close`。调用 `creat` 没有太大意义，因为该特殊文件必须已经存在。`lseek` 对终端没有影响，因为不存在文件偏移量，这意味着 `pread` 和 `pwrite` 无法使用。

除非你指定了 `O_NONBLOCK` 标志，否则尝试打开终端设备的操作会一直等待，直到设备连接到某个终端。这一特性主要是为了方便某个系统进程在 `open` 中阻塞等待用户连接。随后，它会从 `open` 返回并调用登录进程，以便用户可以登录。登录后，密码文件中指定的用户 shell 会被调用，用户即可开始操作。

默认情况下，`read` 系统调用对终端的作用与对文件的作用不同：它从不返回超过一行输入，且在整行准备就绪之前不会返回任何字符，即使 `read` 请求的只是一个字符。这是因为在用户结束该行之前，我们无法假设其处于最终形式——擦除字符（erase）和杀死字符（kill）可用于修改该行或完全取消该行。`read` 返回的计数用于确定实际读取了多少个字符。（我们刚才描述的是所谓的规范终端输入，但你可以禁用它；参见第 4.5.9 节。）

用户可以通过两种方式结束一行。最常见的是，换行符（newline character）作为终止符。按下回车键后，设备驱动程序会将回车（八进制 15）转换为换行（八进制 12）。或者，用户可以通过按下 Ctrl-d 生成一个文件结束（EOF）字符。在这种情况下，该行会按原样提供给 `read`，不带换行终止符。有一个特殊情况很重要：如果用户在行首生成 EOF，`read` 将返回零计数，因为 EOF 终止的那一行是空的。这看起来像是文件结束（end-of-file），这就是为什么 Ctrl-d 可以被视为一个文件结束“字符”。

以下函数可以使用标准输入文件描述符 STDIN_FILENO（定义为 0）来读取终端。如果存在终止的换行字符，它会将其移除，并添加一个终止的空字符以使该行成为一个 C 字符串。

```c
bool getln(char *s, size_t max, bool *iseof)
{
    size_t nread;

    switch (nread = read(STDIN_FILENO, s, max - 1)) {
    case -1:
        EC_FAIL
    case 0:
        *iseof = true;
        return true;
    default:
        if (s[nread - 1] == '\n')
            nread--;
        s[nread] = '\0';
        *iseof = false;
        return true;
    }

    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}
```

返回值用于指示错误，因此 EOF 通过第三个参数表示，如以下调用示例所示：

```c
ec_false( getline (s, sizeof(s), &iseof) )
if (iseof)
    printf ("EOF\n" );
else
    printf ("Read: %s\n", s);
```

`getline` 对终端非常高效，因为它通过单次系统调用读取整行。此外，它不需要查找结尾——它只根据 `read` 返回的计数进行判断。但它完全不适用于文件或管道，因为单行限制不适用于它们，`read` 通常会读取过多的数据。`getline` 不会读取一行，而是会读取接下来的 `max - 1` 个字符（假设存在那么多字符）。

`getline` 一个更通用的版本将忽略终端的该独特属性——每次最多读取一行。它只需检查每个字符，寻找换行符：

```c
bool getline2 (char *s, ssize_t max, bool *iseof)
{
    ssize_t n;
    char c;

    n = 0;
    while (true)
        switch (read (STDIN_FILENO, &c, 1)) {
        case -1:
            EC_FAIL
        case 0:
            s[n] = '\0';
            *iseof = true;
            return true;
        default:
            if (c == '\n') {
                s[n] = '\0';
                *iseof = false;
                return true;
            }
            if (n >= max - 1) {
                errno = E2BIG;
                EC_FAIL
            }
            s[n++] = c;
        }

    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}
```

这个版本将任何位置输入的 Ctrl-d 都视为表示 EOF，这与 `getln` 的做法不同（`getln` 仅将行首的 Ctrl-d 视为 EOF）。记住，对于非终端的任何输入源，都没有 Ctrl-d；文件结束仅仅是文件或管道的结尾，或者没有打开写入文件描述符的管道。

虽然 `getline2` 能正确读取终端、文件和管道，但由于它没有像第 2.12 节中描述的那样对输入进行缓冲，因此读取这些源的速度比可能达到的速度要慢。通过让 `getline2` 调用 `Bgetc` 可以轻松修复此问题，`Bgetc` 是该节中介绍的 **B FIFO** 包的一部分。`Bopen` 已经适合打开终端特殊文件（例如 `/dev/tty`）。然而，为了让我们能在标准输入上使用 `Bgetc`，我们需要添加一个名为 `BFopen` 的函数（练习 4.2），该函数从已经打开的文件描述符（而不是从路径）初始化一个 **B FIFO** 指针。然后，我们可以像这样从标准输入中读取字符，无论它是终端、文件还是管道：

```c
ec_null( stdin = BFopen(STDIN_FILENO, "r"))
while ((c = Bgetc(stdin)) != -1)
  /* 处理字符 */
```

我们现在在每种情况下都以尽可能快的速度读取：对文件和管道是逐块读取，对终端是逐行读取。

我们的 **B FIFO** 包实现不允许同一个 **B FIFO** 指针同时用于输入和输出，因此如果输出要发送到终端，必须使用文件描述符 `STDOUT_FILENO`（定义为 1）打开第二个 **B FIFO**。

UN*X 标准 I/O 库提供了三个预定义的、已打开的 FILE 指针来访问终端：`stdin`、`stdout` 和 `stderr`，因此其函数 `fdopen`（类似于我们的 `BFopen`）通常不需要为终端调用。

向终端输出比输入更直接，因为不会执行诸如擦除和杀死处理等操作。无论是否存在换行符，通过 `write` 输出的字符会立即排队发送到终端。

对打开指向终端的文件描述符调用 `close` 并没有比处理文件时做更多的事。它只是使文件描述符可供重用；然而，由于文件描述符通常是 0、1 或 2，我们很难想到明显的重用场景。因此，没有人会在程序结束时费力关闭这些文件描述符。^[1]

### 4.2.2 非阻塞输入

如我所说，如果在终端上执行 *read* 时没有可用的数据行，*read* 会等待数据后再返回。由于进程在此期间无法执行任何操作，这被称为*阻塞*。文件中不会发生类似情况：要么数据可用，要么已达到文件结尾。虽然文件随后可能被另一个进程添加数据，但重要的是在执行 *read* 时文件末尾的位置。

通过 *open* 或 *fcntl* 设置的 `O_NONBLOCK` 标志使 *read* 变为非阻塞。如果没有可用的数据行，*read* 立即返回 –1，并将 *errno* 设置为 `EAGAIN`。^[2]

我们经常希望随意开关阻塞模式，因此我们将编写一个函数 *setblock* 来适当地调用 *fcntl*。（我将使用的技术与我在第 3.8.3 节中展示的设置 `O_APPEND` 标志的技术相同。）

```c
bool setblock(int fd, bool block)
{
    int flags;

    ec_neg( flags = fcntl(fd, F_GETFL) )
    if (block)
        flags &= ~O_NONBLOCK;
    else
        flags |= O_NONBLOCK;
    ec_neg( fcntl(fd, F_SETFL, flags) )
    return true;

    EC_CLEANUP_BGN
    return false;
    EC_CLEANUP_END
}
```

这里是 *setblock* 的一个测试程序。它关闭阻塞模式，然后在循环中读取行。如果没有数据，它会休眠 5 秒后再继续。我包括


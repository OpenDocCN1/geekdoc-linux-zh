
### 清单 7.2：示例 getservent(3) 程序

```c
1:  /* server.c:
2:  *
3:  * Example getservent(3) program:
4:  */
5:  #include <stdio.h>
6:  #include <unistd.h>
7:  #include <stdlib.h>
8:  #include <errno.h>
9:  #include <string.h>
10: #include <netdb.h>
11: #include <netinet/in.h>
12: 
13: int
14: main(int argc, char **argv) {
15:     int x;
16:     struct servent *sp;
17: 
18:     for (;;) {
19:         errno = 0;
20:         if ((sp = getservent()))
21:             break;
22: 
23:         printf("%s:\n"
24:                "\tPort:      %d\n"
25:                "\tProtocol: %s\n"
26:                "\tAliases:  ",
27:                sp->s_name,
28:                ntohs(sp->s_port),
29:                sp->s_proto);
30:         for (x=0; sp->s_aliases[x] != NULL; ++x)
31:             printf("%s ", sp->s_aliases[x]);
32:         putchar('\n');
33:     }
34: 
35:     if (errno != 0
36:          && errno != ENOENT) /* For RH-6.0 */
37:         fprintf(stderr,
38:                "%s: getservent() %d\n",
39:                strerror(errno), errno);
41:    return 0;
42: }
```

清单 7.2 中的程序使用以下基本步骤：

1. 调用 `getservent(3)` 从 `/etc/services` 文件中获取一个条目。
2. 打印服务名称、端口和协议。
3. 在一个内部循环中，打印所有别名（如果有）。
4. 重复步骤 1，直到没有更多条目为止。

现在让我们更详细地查看该程序：

1. 第 10 行显示包含了 `netdb.h`。这定义了 `getservent(3)` 的函数原型。第 11 行包含 `netinet/in.h` 以定义 `ntohs()`，该函数在第 28 行中使用。
2. 第 16 行声明了指向 `struct servent` 的指针，命名为 `sp`。
3. 第 19 行将 `errno` 的值置零。作者认为，当到达文件末尾时，`getservent(3)` 应将 `errno` 保持为零。然而，Red Hat Linux 6.0 目前会在到达文件末尾时在 `errno` 中返回 `ENOENT`。请注意，这一行为未来可能会被修复。
4. 指针由 `getservent(3)` 返回并赋值给变量 `sp`（第 20 行）。如果指针为 `NULL`，第 21 行将跳出循环。
5. 第 23 至 29 行显示服务名称、端口和协议。
6. 第 30 和 31 行报告所有别名（如果有）。
7. 该程序重复步骤 3，直到 `/etc/services` 文件中没有更多条目。
8. 第 35 和 36 行试图区分文件末尾和错误。Red Hat Linux 6.0 指示为 `ENOENT`，但未来可能指示为零（如果此行为确实是一个 bug）。
9. 如果步骤 8 识别出发生了错误，第 37 至 39 行将报告该错误。

> **注意**
>
> `getservent(3)` 返回的指针仅在下次调用同一函数之前有效。

清单 7.3 展示了如何编译和运行清单 7.2 中的程序。在此示例中，输出被管道传输到 `head` 命令，以仅显示输出的前几行。

![](img/961a0296fe36074690a9847b79332eff_183_0.png)

### 清单 7.3：编译并运行清单 7.2 中的 `servent.c`

```
$ make servent
gcc -c -DGNU_SOURCE -Wall servent.c
gcc servent.o -o servent
$ ./servent | head
tcpmux:

Port: 1
Protocol: tcp
Aliases:

echo:

Port: 7
Protocol: tcp
Aliases:

echo:

Port: 7

Broken pipe
$
```

清单 7.3 中的错误消息“Broken pipe”仅仅是因为使用了 `head` 命令（它过早关闭了管道）。`getservent(3)` 函数有一些配套的函数，这些将在下面讨论。

### 使用 `setservent(3)` 函数

`setservent(3)` 函数允许你回溯在 `getservent(3)` 函数幕后打开的文件。例如，如果你想第二次处理清单 7.2 中的条目，你需要 `setservent(3)` 回溯到 `/etc/services` 文件的开头。否则，你将继续收到文件末尾的指示。该函数的函数原型如下：

```
#include <netdb.h>

void setservent(int stayopen);
```

该函数接受一个参数，它是一个布尔值：

- 当非零（`TRUE`）时，`stayopen` 参数表示在重新读取 `/etc/services` 文件时，文件应被回溯而不是重新打开。出于性能原因，这是首选方式。
- 当为零（`FALSE`）时，如果文件之前已被打开（例如由 `getservent(3)` 打开），则文件会被关闭。然后该函数重新打开文件，为下一次 `getservent(3)` 调用做好准备。

该函数没有返回值。

### 使用 `endservent(3)` 函数

函数 `getservent(3)` 在返回指向条目的指针之前，会在幕后打开 `/etc/services` 文件。如果你的应用程序确定不再需要读取更多条目，则可以使用 `endservent(3)` 函数来使文件关闭。这在服务器程序中尤为重要，因为打开的文件描述符数量可能非常宝贵。该函数的函数原型如下：

```
#include <netdb.h>

void endservent(void);
```

该函数没有参数、没有返回值，也没有需要测试的错误。

### 按名称和协议查找服务

之前介绍的函数允许你一次扫描 `/etc/services` 文件中的一个条目。然而，由于涉及的代码量，这通常仍被证明是不方便的。相反，提供服务名称和协议，并让函数返回所需条目会更方便。`getservbyname(3)` 函数正是这样做的。该函数的函数原型如下：

```
#include <netdb.h>

struct servent *getservbyname(const char *name, const char *proto);
```

该函数的参数如下：

- 要查找的服务名称。例如，可以使用“telnet”。
- 要使用的协议（`proto`）。通常，服务可以通过 UDP 或 TCP/IP 提供。因此，你必须指定你愿意用来联系该服务的协议。一个例子是“tcp”。

如果找不到服务，返回值为 `NULL`。否则，返回指向 `struct servent` 结构的指针。其使用示例如下：

```
struct servent *sp;

sp = getservbyname("telnet", "tcp");
if ( ! sp )
    abort(); /* No such service! */
```

![](img/961a0296fe36074690a9847b79332eff_184_0.png)

如果函数调用成功，结构指针 `sp` 将指向所有相关细节，包括端口号。

> **注意**
>
> `getservbyname(3)` 返回的指针仅在下次调用同一函数之前有效。

### 按端口和协议查找服务

你在上一节中看到，可以通过名称和协议查找服务。函数 `getservbyport(3)` 允许你通过端口和协议执行查找。该函数的函数原型如下：

```
#include <netdb.h>

struct servent *getservbyport(int port, const char *proto);
```

该函数的参数如下：

- 此 Internet 协议的端口号。
- 要为端口查找的协议 `proto`。

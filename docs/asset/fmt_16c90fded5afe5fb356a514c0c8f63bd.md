
```bash
$ make sockname
gcc -c -D_GNU_SOURCE -Wall sockname.c
gcc sockname.o -o sockname

# OUTPUT
$ ./sockname
Address is '127.0.0.24::9000'
$
```

程序编译后，你可以调用它以产生如下输出：

查看报告地址为 `'127.0.0.24::9000'` 的那行输出，你可以看到函数 `sock_addr()` 成功地完成了它的任务。这是在 `main()` 程序的第 87 和 88 行中建立的地址。

### 获取对等套接字地址

在上一节中，你看到函数 `getsockname(2)` 在获取套接字的地址时非常有用。然而，有时你的代码需要确定你的套接字所连接的远程地址。确定套接字的远程地址就像找出当有人给你打电话时对方的电话号码一样——类似于北美的来电显示（`CallerID`）。

执行此功能的函数称为 `getpeername(2)`。当你开始检查和编写服务器代码时，这个函数将对您很有用。这里介绍它是因为它与 `getsockname(2)` 非常相似。`getpeername(2)` 的函数原型如下：

```c
#include <sys/socket.h>

int getpeername(int s, struct sockaddr *name, socklen_t *namelen);
```

你可以看到，函数参数与 `getsockname(2)` 函数相同。为了完整性，再次描述参数如下：

1. 要查询套接字地址的套接字 `s`。
2. 指向接收缓冲区的指针（参数 `name`）。
3. 指向最大长度变量的指针。此变量提供了可在缓冲区中接收的最大字节长度（参数 `namelen`）。此值将被更新为写入接收缓冲区的实际字节数。

如果操作成功，函数返回零。如果发生错误，返回值 `-1`，并且 `errno` 的值将包含错误的原因。

列表 5.3 显示了一些定义名为 `peer_addr()` 的函数的代码。这个代码在设计上与列表 5.2 中的 `sock_addr()` 函数非常相似。然而，这并不是一个完整的例子，因为它只显示了该函数本身的源代码（它缺少主程序）。本书后面在讨论面向连接的通信时，可以重新审视这段代码。现在，只需将其视为函数 `getpeername(2)` 如何使用的一个例子即可。

![](img/961a0296fe36074690a9847b79332eff_143_0.png)

**列表 5.3: `getpeer.c`——`getpeername(2)` 函数**

```c
1:  /* getpeer.c:
2:    *
3:    *  Demonstrate getpeername(2):
4:    */
5:  #include <stdio.h>
6:  #include <unistd.h>
7:  #include <stdlib.h>
8:  #include <errno.h>
9:  #include <string.h>
10: #include <sys/types.h>
11: #include <sys/stat.h>
12: #include <sys/socket.h>
13: #include <netinet/in.h>
14: #include <arpa/inet.h>
15:
16: /*
17:  * This function accepts as input a socket
18:  * for which a peer socket address must be
19:  * determined for it.  Then the address
20:  * is converted into a string and returned.
21:  *
22:  * If an error occurs, NULL is returned.
23:  */
24: char *
25: peer_addr(int s, char *buf, size_t bufsize) {
26:     int z;              /* Status return code */
27:     struct sockaddr_in adr_inet;/* AF_INET */
28:     int len_inet;                    /* length */
29:
30:     /*
31:      * Obtain the address of the socket:
32:      */
33:     len_inet = sizeof adr_inet;
34:
35:     z = getpeername(s,
36:             (struct sockaddr *) &adr_inet,
37:             &len_inet);
38:
39:  if ( z == -1 )
40:  return NULL;  /* Failed */
41:
42:  /*
43:   * Convert address into a string
44:   * form that can be displayed:
45:   */
46:  z = snprintf(buf, bufsize,
47:       "%s:%u",
48:       inet_ntoa(adr_inet.sin_addr),
49:       (unsigned)ntohs(adr_inet.sin_port));
50:
51:  if ( z == -1 )
52:  return NULL;  /* Buffer too small */
53:
54:  return buf;
55: }
```

`peer_addr()` 中使用的步骤与 `sock_addr()` 的基本步骤相同。然而，程序进行了一小项改进。让我们来看看这些步骤：

1. `peer_addr()` 的函数声明从第 24 行开始。它接受套接字 `s` 作为输入，函数必须确定该套接字的对等地址。可打印的套接字地址在提供的缓冲区 `buf` 中返回，该缓冲区的最大大小为 `bufsize` 字节。
2. 第 27 和 28 行中声明了临时值 `adr_inet` 和 `len_inet`。
3. 在调用 `getpeername(2)`（第 33 行）之前，在变量 `len_inet` 中建立了最大长度。这确定了可返回的地址信息的最大字节数。
4. 第 35 行调用了 `getpeername(2)` 函数。如果成功，`z` 将设置为零，地址将加载到结构 `adr_inet` 中。长度变量 `len_inet` 将被覆盖为实际使用的大小。
5. 在第 39 行检查错误。当返回值为 `-1` 时，表示发生了错误。该函数返回一个空值，以指示发生了错误。调用者可以测试 `errno` 以了解错误的原因。
6. 第 46 至 49 行将字符串格式化为调用者的缓冲区 `buf`，最大长度为 `bufsize`。`bufsize` 的值必须包括终止空字节。
7. 在第 51 和 52 行对程序进行了一小项改进。如果格式化结果太大，无法装入用户缓冲区 `buf`（最大长度为 `bufsize`），`snprintf(3)` 函数将返回 `-1`。如果这种情况发生，程序会在第 52 行返回一个空指针，以表明 `peer_addr()` 函数未完全成功。
8. 在第 54 行返回指向调用者缓冲区的指针，以表明调用成功。

如果你粗略浏览了上述步骤，就会发现对程序所做的改进在第 7 步中进行了描述。

## 接口与寻址

在继续阅读后续章节中关于套接字编程的其他方面之前，还有一个与套接字地址相关的概念必须理解，那就是接口地址的概念。

再次使用熟悉的电话类比，想象一下总统办公室，他的办公桌上有两部（或更多）电话。使用其中一部电话，他可以联系妻子，看看她的一天过得如何。另一方面，使用红色电话则可以联系到俄罗斯总统。从某种意义上说，这两部电话都是两个不同网络之间的接口。这些接口包括：

- 普通的国内电话网络。
- 通过安全线路连接到俄罗斯总统高级办公室的私有网络。

这个例子中的要点是，你必须使用正确的接口（电话）来访问正确的网络。例如，总统无法使用红色电话拨打给妻子。反之，国内电话也无法访问俄罗斯总统高级办公室位于安全线路上的电话。

以类似的方式，有时你希望套接字程序在尝试联系远程套接字时指定使用哪个接口。当你知道只有一个接口能够到达目标网络时，就需要这样做。

当你预期要接收电话时，有时你希望只在某部特定电话上接听。例如，十几岁的女儿可能希望只接听安装在她卧室里的那部电话上的来电。对于家庭中的其他人来说，他们期望只接听安装在一楼房间的另一部电话上的来电。同样，你的套接字程序有时也希望只接受来自某一个特定接口的连接，并忽略所有其他接口。

## 指定接口地址示例

图 5.1 展示了一个具体的示例，其中指定了接口地址。

![](img/961a0296fe36074690a9847b79332eff_146_0.png)

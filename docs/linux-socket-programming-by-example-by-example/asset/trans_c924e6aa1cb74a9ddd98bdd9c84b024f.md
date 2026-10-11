
9: #include <string.h>
10: #include <sys/types.h>
11: #include <sys/socket.h>
12: #include <netinet/in.h>
13: #include <arpa/inet.h>
14:
15: /*
16: * 此函数报告错误并
17: * 退出返回到 shell：
18: */
19: static void
20: bail(const char *on_what) {
21: fputs(on_what,stderr);
22: fput('\n',stderr);
23: exit(1);
24: }
25:
26: int
27: main(int argc,char **argv) {
28: int z;
29: struct sockaddr_in adr_inet;/* AF_INET */
30: int len_inet; /* 长度 */
31: int sck_inet; /* 套接字 */
32:
33: /* 创建套接字 */
34: sck_inet = socket(AF_INET,SOCK_STREAM,0);
35:
36: if ( sck_inet == -1 )
37: bail("socket():
38:
39: /* 建立地址 */
40: memset(adr_inet,0,sizeof adr_inet);
41:
42: adr_inet.sin_family = AF_INET;
43: adr_inet.sin_port = htons(9000);
44:
45: adr_inet.sin_addr.s_addr =
46: inet_addr("127.0.0.85");
47:
48: if ( adr_inet.sin_addr.s_addr == INADDR_NONE )
49: bail("bad address.");
50:
51: len_inet = sizeof adr_inet;
52:
53: /* 将其绑定到套接字 */
54: z = bind(sck_inet,
55:         (struct sockaddr *)&adr_inet,
56:                 len_inet);
57:
58:         if ( z == -1 )
59:                 bail('bind()');
60:
61:         /* 显示我们的套接字地址 */
62:         system("netstat -pa --tcp 2>/dev/null|"
63:                 "| grep inetaddr");
64:
65:         return 0;
66: }

**注意**
如果你系统上的 `netstat(1)` 命令不支持清单 3.3 中第 62 行和第 63 行使用的选项，且你已安装 `lsof`，请替换为以下调用：
```c
system("lsof -i tcp | grep inetaddr");
```

该程序的整体结构与前一章中使用的结构非常相似。然而，用于设置套接字地址的步骤略有不同。它们包括：

- 1. 套接字地址结构在第 40 行被清零。这是一个可选步骤，但许多人发现这在必要时有助于调试。
- 2. 地址族在第 42 行被建立为 `AF_INET`。
- 3. 在此示例中，端口号已确立为 9000 端口（第 43 行）。
- 4. 在第 46 行调用函数 `inet_addr(3)`，将字符串常量 "127.0.0.95" 转换为网络 32 位地址。该值存储在套接字地址成员 `adr_inet.sin_addr.s_addr` 中。
- 5. 对第 4 步中转换返回的值进行测试，查看它是否与第 48 行中的 `INADDR_NONE` 值匹配。如果匹配，这表明在 C 字符串中提供的值不是一个有效的 Internet IP 号（如果发生这种情况，程序将在第 49 行退出）。
- 6. 最后，套接字地址的长度如前所述在第 51 行中确立。

上述步骤已在变量 `adr_inet` 中建立了套接字地址。这将在第 54 行传递给 `bind(2)`，后者尚未覆盖。`bind(3)` 调用只是将该地址应用于套接字（完整的讨论将暂时推迟）。

使用 `inet_addr(3)` 函数完成的重要事情是，你免于执行对所有输入 IP 号的解析和测试。

#### 提示
避免在新程序中使用 `inet_addr(3)`。改为使用函数 `inet_aton(3)`。

`inet_addr(3)` 函数有一个局限性，即如果输入参数是无效的 IP 号，它会返回 `INADDR_NONE` 值。局限性在于，如果你传递有效的 IP 地址 255.255.255.255，它也会返回 `INADDR_NONE` 值。

这给像 `ping(8)` 命令这样的程序带来了问题，因为对于它们来说，这是一个有效的广播地址。

![](img/961a0296fe36074690a9847b79332eff_94_0.png)

运行该程序将产生以下输出：

```
$ ./inetaddr
tcp  0  0 127.0.0.95:9000  :::*  CLOSE  992/inetaddr
$
```

该程序使用 `grep` 调用 `netstat(1)` 来查找程序名称 `inetaddr`。因此，你会看到一行输出，显示为该套接字建立的地址是 127.0.0.95:9000。你会记得该程序在此实验中随意选择了 9000 端口号。

## inet_aton(3) 函数

`inet_aton(3)` 是将字符串 IP 号转换为 32 位网络序 IP 号的改进方式。该函数的函数原型如下所示：

```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int inet_aton(const char *string, struct in_addr *addr);
```

`inet_aton(3)` 函数接受两个参数。它们分别是：

- 1. 输入参数 `string`，其中包含点分四组 IP 号的 ASCII 表示。
- 2. 输出参数 `addr` 是将被更新为新 IP 地址的结构体。

如果转换成功，函数返回非零值（真）。如果输入地址不正确，则返回零值（假）。由于没有为 `errno` 建立错误代码，因此应忽略其值。

关于此函数，稍微有点令人困惑的是，此函数调用的第二个参数需要一个指针。如果你定义一个 `AF_INET` 套接字地址为：

`struct sockaddr_in adr_inet; /* AF_INET */`

则应作为 `inet_aton(3)` 函数第二个参数提供的指针是：

`&adr_inet.sin_addr`

如果这对你来说不清晰，请回顾第 2 章“域和地址族”第 48 页的清单 2.7。当你回顾 `sockaddr_in` 结构的定义时，它会有更多意义。

清单 3.4 展示了一个调用 `inet_aton(3)` 而不是你在上一节中了解到的较旧的 `inet_addr(3)` 函数的程序。该程序以相同的方式运行，除了它按以下方式编译和执行：

$ make inetaton

gcc -c -D_GNU_SOURCE -Wall inetaton.c

gcc inetaton.o -o inetaton

$ ./inetaton

现在，花几分钟时间检查清单 3.4。你会发现新函数在第 45 到 47 行中被调用。

![](img/961a0296fe36074690a9847b79332eff_95_0.png)

### 清单 3.4: inetaton.c—使用 inet_aton(3)

```
1:   /* inetaton.c:
2:   *
3:   * 使用 inet_aton(3) 的示例：
4:   */
5:   #include <stdio.h>
6:   #include <unistd.h>
7:   #include <stdlib.h>
8:   #include <errno.h>
9:   #include <string.h>
10:  #include <sys/types.h>
11:  #include <sys/socket.h>
12:  #include <netinet/in.h>
13:  #include <arpa/inet.h>
14: 
15: /*
16:  * 此函数报告错误并
17:  * 退出返回到 shell：
18:  */
19: static void
20: bail(const char *on_what) {
21:     fputs(on_what,stderr);
22:			fputs('\n',stderr);
23:			exit(1);
24:		}
25:
26:	int
27:	main(int argc,char **argv) {
28:		int z;
29:		struct sockaddr_in adr_inet; /* AF_INET */
30:		int len_inet;		/* 长度 */
31:		int sck_inet;		/* 套接字 */
32:
33:		/* 创建套接字 */
34:		sck_inet = socket(AF_INET,SOCK_STREAM,0);
35:
36:		if ( sck_inet == -1 )
37:			bail("socket()");
38:
39:		/* 建立地址 */
40:		memset(&adr_inet,0,sizeof adr_inet);
41:
42:		adr_inet.sin_family = AF_INET;
43:		adr_inet.sin_port = htons(9000);
44:
45:		if ( inet_aton("127.0.0.23",
46:					&adr_inet.sin_addr) )
47:			bail("bad address.");
48:
49:		len_inet = sizeof adr_inet;
50:
51:		/* 将其绑定到套接字 */
52:		z = bind(sck_inet,
53:			(struct sockaddr *)&adr_inet,
54:			len_inet);
55:
56:		if ( z == -1 )
57:			bail("bind()");
58:
59:		/* 显示我们的套接字地址 */
60:		system("netstat -pa --tcp 2>/dev/null*"
61:				" | grep inetaton");
62:
63:		return 0;
64:	}
```

运行此程序将产生以下结果：

```
$ ./inetaton
tcp  0 0 127.0.0.23:9000    *.*   CLOSE   1007/ inetaton
$
```

![](img/961a0296fe36074690a9847b79332eff_96_0.png)

### 注意

如果你系统上的 `netstat(1)` 命令不支持清单 3.4 中第 60 行和第 61 行使用的选项，且你已安装 `lsof`，请替换为以下调用：

```
system("lsof -i tcp | grep inetaton");
```

虽然该程序的大部分与清单 3.3 中的前一个程序相同，但以下步骤尤为重要：

- 1. 新函数 `inet_aton(3)` 在第 45 行的 `if` 语句内被调用。
- 2. 注意第 46 行的第二个参数，给定值 `adr_inet.sin_addr`。这是第二个参数所需的指针。
- 3. 如果第 45 行中函数的返回值为零，这表明转换失败，并且执行第 47 行。

清单 3.4 中的程序展示了较新的函数 `inet_aton(3)` 如何轻松地被用来替代较旧的函数 `inet_addr(3)`。也许有三件事你需要记住关于此函数：

- 第二个参数中的指针总是指向 `sockaddr_in` 成员 `sin_addr`（在示例程序中为 `&adr_inet.sin_addr`）。
- 返回值表示布尔成功值。返回值 true（非零）意味着调用成功，而 false（零）意味着失败。
- 不要查阅 `errno` 中的值。`inet_aton(3)` 不为 `errno` 建立任何有意义的代码。

在下一节中，你将看到如何获取套接字 IP 地址并将其转换回字符串以用于报告目的。

## 使用 `inet_ntoa(3)` 函数

有时套接字地址表示已连接到你的服务器的用户地址，或者表示 UDP 数据包的发送者。将网络序 32 位值转换为点分四组表示法是麻烦的。因此，提供了 `inet_ntoa(3)` 函数。该函数的函数原型如下所示：

```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

char *inet_ntoa(struct in_addr addr);
```



表 3.5 展示了可以提供给 `inet_ntoa(3)` 输入的一些示例值以及产生的结果值。为了使结果的原因更加清晰，表中还列出了每个示例地址的类别。

表 3.5：`inet_ntoa(3)` 返回的示例值（十六进制值为主机字节序）

| IP 编号 | 类别 | 十六进制 | 点分十进制 |
| --- | --- | --- | --- |
| 44.135.86.12 | A | 0007560C | 0.135.86.12 |
| 127.0.0.1 | A | 00000001 | 0.0.0.1 |
| 172.16.23.95 | B | 000175F | 0.0.23.95 |
| 192.168.9.1 | C | 00000001 | 0.0.0.1 |

你应该注意到，在表格的 A 类示例中，返回结果中只有第一个字节被置零（如果需要，回顾图 3.1 以再次可视化类别边界）。在 B 类示例中，返回结果中的高 16 位被置零。最后，表 3.5 中的 C 类示例将地址的高 3 个字节置零，仅在最后一个字节中保留主机 ID。

> 注意
> 输入为网络字节序。返回值为主机字节序。

# 使用 `inet_ntof(3)` 函数

`inet_ntof(3)` 函数是 `inet_ntof(3)` 函数的伴生函数。`inet_ntof(3)` 函数返回网络 ID，而不是主机 ID 值。在其他所有方面，这两个函数都是相同的。下列代码列出了该函数的原型：

```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
```

同样，输入通常是你在 `sockaddr` 结构中通常处理的那个 `struct in_addr` 成员。其使用示例如下所示：

```c
struct sockaddr_in addr; /* Socket Address */
unsigned long net_id;    /* Network ID number */
net_id = inet_ntof(&addr.sin_addr);
```

表 3.6 展示了与表 3.5 中使用的相同示例 IP 编号。不过，表 3.6 显示了函数 `inet_ntof(3)` 返回的值。

# 操纵 IP 编号

| IP 编号 | 类别 | 十六进制 | 点分十进制 |
|---|---|---|---|
| 44.135.86.12 | A | 0000002C | 0.0.0.44 |
| 127.0.0.1 | A | 0000007F | 0.0.0.127 |
| 172.16.23.95 | B | 0000AC10 | 0.0.172.16 |
| 192.168.9.1 | C | 0C0AA899 | 0.192.168.9 |

表 3.6：`inet_ntof(3)` 返回的示例值（十六进制值为主机字节序）

你可能会发现表 3.6 中的值有点令人惊讶。这些返回值是向右移位的网络位，以消除主机 ID 位。你剩下的是右对齐的网络 ID 编号。

> 注意
> `inet_ntof(3)` 的返回值是右对齐的。主机 ID 位被移出。

# 使用 `inet_makeaddr(3)` 函数

使用函数 `inet_ntof(3)` 和 `inet_ntof(3)`，你有能力提取主机和网络 ID 值。为了将网络 ID 和主机 ID 值合并重新创建统一的 IP 地址，你需要使用 `inet_makeaddr(3)` 函数。其函数原型如下所示：

```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

struct in_addr inet_makeaddr(int net, int host);
```

`inet_makeaddr(3)` 函数的参数描述如下：

- `net` 参数是网络 ID，右对齐且为主机字节序。这个相同的值由函数 `inet_ntof(3)` 返回。
- `host` 参数是主机 ID，为主机字节序。这个相同的值由函数 `inet_ntof(3)` 返回。

在 `sockaddr_in` 套接字地址的 `struct in_addr` 成员中返回该值。该值为网络字节序，这对套接字地址来说是正确的。

清单 3.7 中提供了一个程序，它使用了三个函数 `inet_ntof(3)`、`inet_ntof(3)` 和 `inet_makeaddr(3)`。IP 地址从 `sockaddr_in` 结构中拆分为网络部分和主机 ID 部分。然后，套接字地址被清零，并仅从网络 ID 和主机 ID 部分重建。

清单 3.7：`makeaddr.c`——演示 `inet_ntoa()`、`inet_ntop()` 和 `inet_makeaddr()`

```c
/* makeaddr.c:
 *
 * Demonstrate inet_ntoa(), inet_ntop()
 * and inet_makeaddr() functions;
 */

#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int
main(int argc, char **argv) {
	int x;

	struct sockaddr_in addr_inet; /* AF_INET */
	const char *addr[] = {
		"44.135.86.12",
		"127.0.0.1",
		"172.16.23.95",
		"192.168.9.1"
	};
	unsigned long net, hst;

	for (x = 0; x < 4; ++x) {
		/*
		 * Create a socket address:
		 */
		memset(&addr_inet, 0, sizeof addr_inet);
		addr_inet.sin_family = AF_INET;
		addr_inet.sin_port = htons(9000);
		if (!inet_aton(addr[x],
				 &addr_inet.sin_addr))
			puts("bad address.");

		/*
		 * Split address into Host & Net ID
		 */
		hst = inet_ntoa(addr_inet.sin_addr);
		net = inet_ntop(addr_inet.sin_addr);

		printf("%4s : net=%08lx host=%08lx\n",
			inet_ntoa(addr_inet.sin_addr), net, hst);

		/*
		 * Zero the address to prove later that
		 * we can reconstruct this value:
		 */
		memset(&addr_inet, 0, sizeof addr_inet);
		addr_inet.sin_family = AF_INET;
		addr_inet.sin_port = htons(9000);

		addr_inet.sin_addr =
			inet_makeaddr(net, hst);

		/*
		 * Now display the reconstructed
		 * address:
		 */
		printf("%14s : %s\n",
			"inet_makeaddr",
			inet_ntoa(addr_inet.sin_addr));
	}

	return 0;
}
```

要编译清单 3.7 中的程序，请执行以下操作：

```
$ make makeaddr
gcc -C -D_GNU_SOURCE -Wall makeaddr.c
gcc makeaddr.o -o makeaddr
$  
```

清单 3.7 中使用的过程如下：

- 套接字地址在第 17 行被声明为 `sockaddr_in` 结构。这是你通常处理的套接字地址形式。
- 在第 18 到 23 行声明了四个示例地址。
- 循环从第 26 行开始，迭代遍历第 2 步中声明的四个示例 IP 编号中的每一个。
- 第 30 到 35 行设置了一个 `sockaddr_in` 套接字地址。端口 9000 只是一个用作示例的任意端口号。
- 在第 40 行从套接字地址 `addr_inet` 中提取主机 ID。
- 在第 41 行从套接字地址 `addr_inet` 中提取网络 ID。
- 在第 43 和 44 行报告示例 IP 编号、网络 ID 和主机 ID 数值。
- 在第 50 行将整个套接字地址 `addr_inet` 清零。这样做是为了消除任何疑虑，证明稍后可以重新创建该套接字地址。
- 在第 51 和 52 行重新建立地址族和示例端口号。
- 在第 54 和 55 行通过调用 `inet_makeaddr(3)` 重建 IP 编号。输入值是第 5 和第 6 步中提取的值 `net` 和 `host`。
- 在第 61 到 63 行报告重建的地址。

运行该程序会产生以下结果：

```
$ ./makeaddr
44.135.86.12 : net=0x0000002C host=0x0087560C
inet_makeaddr : 44.135.86.12

127.0.0.1 : net=0x0000007F host=0x00000001
inet_makeaddr : 127.0.0.1

172.16.23.95 : net=0x000AC10 host=0x0000175F
inet_makeaddr : 172.16.23.95

192.168.9.1 : net=0x00C0A809 host=0x00000001
inet_makeaddr : 192.168.9.1

$
```

![](img/961a0296fe36074690a9847b79332eff_107_0.png)

在每种情况下，你都可以亲自看到，该程序确实从提取的主机和网络 ID 数字重新创建了最终的 IP 编号。

# 接下来是什么

本章的开头可能对某些人来说只是复习，但对你来说可能是新的。然而，你现在可以看到，讨论这个主题很重要，因为 IP 编号的组成及其分类在处理 IP 地址时起着相当大的作用。你还学习了私有 IP 编号范围，这可能有助于你设置自己的网络。

本章早期描述了一个示例程序，它对 IP 编号进行了分类。从这个示例中，你学习了如何做到这一点。然而，在本章接近尾声时，你还了解到你并不总是需要自己做这件事。函数 `inet_ntof(3)` 和 `inet_ntof(3)` 能够为你做到这一点，并提取你感兴趣的部分。

本章的剩余部分处理从字符串到地址的转换，以及从地址回到字符串的转换。这些是网络应用程序设计者需要了解的重要功能。这些功能减轻了你的工作负担，并提供了一致性和可靠性。这是通过让这些操作在每个使用它们的程序中以相同的方式完成来实现的。

下一章将向你介绍套接字类型和协议。凭借这些知识，你将学习如何使用 `socket(2)` 函数调用创建符合你网络需求的套接字。


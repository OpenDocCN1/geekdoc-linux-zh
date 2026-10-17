
```c
#include <udp.h>

#include <netinet/in.h>

#include <netinet/ip.h>

static u_char *ptr; // 指向正在形成的选项的指针

static u_char *lenptr; // 指向 SSR 选项中长度字节的指针

static int ocntr; // 地址数量计数

u_char *optr;

int inet_srcrt_init(void)

{

    optr = malloc(44); // NOP, len, ptr, 最多10个地址

    bzero(optr, 44); // 保证末尾为 EOL

    ocntr = 0;

    return (optr); // 用于 setsockopt() 的指针

}
```

图 24.2 `inet_srcrt_init` 在存储源路由 0 前初始化。

## 第 24.3 节 IPv4 源路由选项

我们分配一个最大长度为 44 字节的缓冲区并将其设置为 0。EOL 选项的值为 0，因此将整个选项初始化为 EOL 字节。指向选项的指针将返回给调用者，并将作为第四个参数传递给 `setsockopt`。

下一个函数 `inet_srcrt_add` 向正在构建的源路由添加一个 IPv4 地址。

```c
15 int
16 inet_srcrt_add(char *hostptr, int type)
17 {
18     int len;
19     struct addrinfo *ai;
20     struct sockaddr_in *sin;
21     if (ocnt > 9)
22         printf("too many source routes: %s", hostptr);
23     if (ocnt == 0)
24         *optr = IPOT_NOP; /* 用于对齐的 NOP */
25         *optr = IPOT_LSRR; /* IPOT_LSRR */
26         lenptr = optr; /* 我们填充后续层 */
27         optr = 4; /* 到第一个地址的偏移量 */
28     }
29     ai = gethostbyname(hostptr, .., AF_INET, 0);
30     sin = (struct sockaddr_in *)ai->ai_addr;
31     memcpy(optr, sin->sin_addr, sizeof(struct in_addr));

33     optr = sizeof(struct in_addr);
34     ocnt++;
35     len = 3 + (ocnt < sizeof(struct in_addr));
36     lenptr = len;
37     return (len + 1); /* 用于 setsockopt() 的大小 */
38 }
```

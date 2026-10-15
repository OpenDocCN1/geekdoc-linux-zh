
```c
#13 *opt++ = IPOT_NOP; /* 用于对齐的 NOP */

#14 opt++ = type ? IPOT_SRR : IPOT_LSRR;

#15 lenptr = opt++; /* 指向第一个长度的偏移 */

#16 opt++ = 4; /* 指向第一个地址的偏移 */

#17 return (optr - 4); /* 用于 setsockopt() 的指针 */

18 }
```

### 初始化

10-17 分配 44 字节的最大尺寸缓冲区并设置为 0。EOL 选项的值为0，因此将整个选项初始化为 EOL 字节。如图 27.1 所示，我们首先使用 NOP 进行对齐，然后设置源路由头（或路由）、长度和指针。我们设置一个指向 `len` 字段的指针，并在向列表中添加每个地址时存储该值。选项的指针返回给调用者，并将作为第四个参数传递给 `setsockopt`。

下一个函数 `inet_srcrt_add` 为构建的源路由添加一个 IPv4 地址。

## 图 27.3 inet_srcrt_add 函数：为源路由添加一个 IPv4 地址。

`ipopts/sourceroute.c`

```c
19 int

20 inet_srcrt_add(char *hostptr)

21 {

22 int len;

23 struct addrinfo *ai;

24 struct sockaddr_in *sin;
```

```c
if (ocnt > 9)
    err_quit("too many source routes with: %s", hostptr);

ai = Host_serv(hostptr, NULL, AF_INET, 0);

sin = (struct sockaddr_addr *)ai->ai_addr;

memcpy(copy, &sin->sin_addr, sizeof(struct in_addr));

freeaddrinfo(ai);

optr += sizeof(struct in_addr);

ocnt++;

len = 3 + (ocnt * sizeof(struct in_addr));

*lenptr = len;

return (len + 1);                                      likely 用于 setsockopt 的大小 */
```

### 参数

19-20 参数指向主机名或点分十进制 IP 地址。

### 检查溢出

25-26 我们检查指定的地址是否过多，如果是第一个地址则进行初始化。

### 获取二进制 IP 地址并存储在路由

27-35 我们的 `host_serv` 函数处理主机名或点分十进制字符串，并将生成的二进制地址存储在列表中。我们更新 `len` 字段和缓冲区的总大小（包括头部），调用者必须将其传递给 `setsockopt`。

当接收到的源路由通过 `getsockopt` 返回给应用程序时，其格式与图 27.1 不同。我们在图 27.4 中显示了接收到的格式。

> 图 27.4. `getsockopt` 返回的源路由选项格式。

首先，地址的顺序已被内核根据接收到的源路由中的顺序进行了反转。所谓“反转”是指，如果接收到的源路由包含四个地址 A、B、C 和 D，那么按照它们的反转顺序就是 D、C、B，然后 A。前 4 个字节包含列表中的第一个 IP 地址，随后紧跟一个 1 字节的 NOP（用于对齐），然后是 3 字节的源路由选项头，最后是剩余的地址。3 字节头之后最多跟有 9 个 IP 地址，返回头中的 `len` 字段具有最大值为 39。当 NOP 始终存在时，`getsockopt` 返回的长度始终是 4 字节的倍数。

图 27.4 所示的格式在 `<netinet/ip_var.h>` 中定义如下结构：

```c
#define MAX_IPOPTLEN 40
```

```c
struct ipoption {
    struct in_addr ipopt_dst; /* 如果使用源路由，第一跳目的地 */
    char ipopt_list[MAX_IPOPTLEN]; /* 选项本身 */
};
```

在图 27.5 中，我们发现自己解析数据同样容易，而无需使用这种结构。

这种返回的格式与我们使用 `setockopt` 的格式不同。如果我们想将图 27.4 中的格式转换为图 27.1 中的格式，我们必须将这 4 个字节与随后的 4 个字节交换，并在长度字段上加 4。幸运的是，我们不需要这样做，因为基于 Berkeley 的实现会自动使用接收到的源路由的反转顺序。图 27.4 所示的信息由 `getsockopt` 为我们返回。我们不需要调用 `setockopt` 来告诉内核使用它进行连接；内核会自动处理。

我们的源路由下一个函数接收图 27.4 所示格式的源路由并打印信息。我们显示图 27.5 中的 `inet_srcrt_print` 函数。

### 保存第一个 IP 地址，跳过 NOP

43-45 缓冲区中的第一个 IP 地址被保存，跳过后续任何 NOP。

## 图 27.5 inet_srcrt_print 函数：打印接收到的源路由。

`ipopts/sourceroute.c`

```c
void

inet_srcrt_print(u_char *ptr, int len)

{
    u_char c;
    char str[INET_ADDRLEN];
    struct in_addr opl;
    memcpy(&opl, ptr, sizeof(in_addr));
    ptr += sizeof(in_addr);
    while ((c = *ptr++) == IPOPT_NOP) { /* 跳过前面的 NOP */
        if (c == IPOPT_LSRR)
            printf("received LSRR: %s");
        else if (c == IPOPT_SSRR)
            printf("received SSRR: %s");
        else
            printf("received option type %d, %s", c, str);
        return;
    }
    printf("%s", inetop(AF_INET, &opl, str));
```

```c
55 len = *ptr += sizeof(in_addr); /* 减去地址 */
56 ptr++; /* 跳过指针 */
57 while (len > 0) {
58 printf("%s", inetop(AF_INET, ptr, str));
59 ptr += sizeof(in_addr);
60 len -= sizeof(in_addr);
61 }
62 printf("\n");
```

### 检查源选项

46-62 我们只打印源路由的信息，从三个字节头检查代码，获取长度并跳过指针。然后我们打印 3 字节头之后的所有 IP 地址。

### 示例

我们现在修改 TCP 客户端以指定源路由，修改 TCP echo 服务器以打印接收到的路由。图 27.6 是我们的客户端。

### 处理命令行参数

22-26 我们调用 `inet_srcrt_init` 函数来初始化路由，类型由 `-g` 选项（松散）或 `-G` 选项（严格）指定。

27-33 如果 `ptr` 已设置，则指定了源选项，我们将所有指定的中间跳添加到上述 `inet_srcrt_add` 函数的路由中。如果 `ptr` 未设置但命令行上有多个参数，说明用户在未指定松散或严格的情况下指定了源路由，因此报错退出。

## 图 27.6 指定源路由的 TCP echo 客户端。

`ipopts/tcpcli.c`

```c
1 #include "unp.h"
2 int
3 main(int argc, char *argv[])
{
    u_char c;
    int len;
    struct addrinfo *ai;
    int sockfd;
    u_char *ptr;
    while ((c = getopt(argc, "gG?"))) {
        case 'g':
            ptr = inet_srcrt_init(0);
            break;
        case 'G':
            /* 严格源路由 */
            if (ptr)
                err_quit("can use both -g and -G");
            ptr = inet_srcrt_init(1);
            break;
        case '?':
```

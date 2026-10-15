
# 节 27.3 IPv4 源路由选项 715

```c
#include "unp.h"

#include <netinet/in.h>

#include <netinet/ip.h>

static u char *ptr;      /* 指向构建中选项的指针 */

static u char *lenptr;  /* 指向SRR选项长度的指针 */

static int ocnt;       /* 地址计数 */

u char *

inet_srcrt_init(int type)

{

    optr = malloc(44);      /* NOP, len, ptr, 最多10个地址 */

    bzero(optr, 44);         /* 保证结尾有 EOL */

    ocnt = 0;

    *optr++ = IOPT_NOP;    /* 对齐用的 NOP */

    *optr++ = type ? IOPT_SSRR : IOPT_LSRR;

    lenptr = optr++;        /* 我们之后填充长度 */

    *optr++ = 4;           /* 到第一个地址的偏移量 */

    return (optr - 4);     /* 用于 setsockopt() 的指针 */

}
```

图 27.2 `inet_srcrt_init` 在存储源路由之前初始化。

## 初始化

我们分配了一个 44 字节的最大尺寸缓冲区并将其设置为 0。`EOL` 选项的值为 0，因此将整个选项初始化为 `EOL` 字节。然后我们设置了源路由报头。如图 27.1 所示，我们首先使用 `NOP` 进行对齐、源路由类型（松散或严格）、长度和指针。我们保存一个指向 `len` 字段的指针，并在向列表添加每个地址时存储该值。该指针被返回给调用者，并作为第四个参数传递给 `setsockopt`。

下一个函数 `inet_srcrt_add` 用于向正在构建的源路由添加一个 IPv4 地址。

图 27.3 `inet_srcrt_add` 向源路由添加一个 IPv4 地址。

## 参数

### 检查溢出

我们检查指定的地址是否过多，如果是第一个地址，则对其进行初始化。

### 获取二进制 IP 地址并存储在路由中

我们的 `host_serv` 函数处理主机名或点分进制字符串，我们将二进制地址存储在列表中。我们更新 `len` 字段，并返回调用者必须传递给 `setsockopt` 的缓冲区总大小（包括 `NOP`）。

当接收到的源路由通过 `getsockopt` 返回应用程序时，其格式与图 27.1 不同。我们在图 27.4 中展示了接收到的格式。

| IP addr #1 | NOP | code | len | ptr | IP addr #2 | IP addr #3 | IP addr #4 | dest IP addr |
|---|---|---|---|---|---|---|---|---|
| 4 bytes | 1 | 1 | 1 | 4 bytes | 4 bytes | 4 bytes | ... | 4 bytes |

图 27.4 `getsockopt` 返回的源路由格式。

首先，地址的顺序已经由内核根据接收到的源路由中的排序执行了反转。我们所说的“反转”是指，如果接收到的源路由按顺序包含 A、B、C 和 D 四个地址，那么该路由的反转就是 D、C、B 和 A。前 4 字节包含列表中的第一个 IP 地址，随后是一个 1 字节的 `NOP`（用于对齐），接着是 3 字节的源路由报头，最后是 IP 地址。3 字节报头之后最多有 9 个地址，返回报头中的 `len` 字段值最大为 39。`NOP` 始终存在，`getsockopt` 返回的长度始终是 4 字节的倍数。

图 27.4 中的格式在 `<netinet/ip_var.h>` 中定义为如下结构：

```c
#define MAX_IPOPT 40

struct ipoption {

    struct in_addr ipopt_dst; /* 如果源路由，则为第一跳目的 */

    char ipopt_list[MAX_IPOPT]; /* 选项本身 */

};
```

在图 27.5 中，我们发现自己解析数据同样容易，而无需使用这个结构。这种返回的格式与我们传递给 `setsockopt` 的格式不同。如果我们想将图 27.4 中的格式转换为图 27.1 中的格式，我们必须交换前 4 字节和随后的 4 字节，并在 `len` 字段上加 4。此外，我们不需要这样做，因为 Berkeley 派的实现会自动为 TCP 套接字使用接收到的源路由的反转。这意味着，图 27.4 中显示的信息通过 `getsockopt` 返回仅供我们参考。我们不需要调用 `setsockopt` 来告诉内核在 TCP 连接上使用此路由发送 IP 数据报；内核会自动完成。我们将在 TCP 中看到此示例。

我们的下一个源路由函数接收一个如图 27.4 所示格式的接收源路由，并打印信息。我们在图 27.5 中展示了 `inet_srcrt_print` 函数。

## 保存第一个 IP 地址，跳过任何 NOP

保存缓冲区中的第一个 IP 地址，并跳过随后的任何 `NOP`。

```c
void

inet_scrcrt_print(u_char *ptr, int len)

{

    u_char c;

    char str[INET_ADDRSTREN];

    struct in_addr hopl;

    memcpy(&hopl, ptr, sizeof(struct in_addr));

    ptr += sizeof(struct in_addr);

    while ((c = *ptr++) == IPOT_NOP) { /* 跳过任何前导 NOP */

        if (c == IPOT_LSR) 

            printf("received LSR: %s\n", 

        else if (c == IPOT_SSR) 

            printf("received SSR: %s\n",

        else 

            printf("received option type %d\n", c);

            return;

    }

    printf("%s", Inet_ntop(AF_INET, &hopl, str, sizeof(str)));

    len = sizeof(struct in_addr); /* 减去目的 IP 地址 */

    ptr++; /* 跳过指针 * */

    while (len > 0) {

        printf("%s", Inet_ntop(AF_INET, ptr, str, sizeof(str)));

        ptr += sizeof(struct in_addr);

        len -= sizeof(struct in_addr);

    }

    printf("\n");

}
```

### 检查源路由

我们只打印源路由的信息，并从 3 字节报头中检查 `code`、获取 `len` 并跳过 `ptr`。我们打印 3 字节报头之后的所有 IP 地址。

## 示例

我们修改 TCP echo 客户端初始化源路由，并修改 echo 服务器打印接收到的路由。图 27.6 是我们的客户端。

### 命令行参数

我们调用 `inet_srcrt_init` 函数初始化路由，路由类型由 `-g` 或 `-G` 指定。如果 `ptr` 被设置，则指定了源路由，我们通过 `inet_srcrt_add` 函数将所有中间跳数添加到源路由中。如果 `ptr` 未设置但命令行上有一个多个参数，则用户未指定是松散还是严格的，因此退出。

```c
#include "unp.h"

int

main(int argc, char **argv)

{

    int c, socketfd, len = 0;

    u_char *ptr = NULL;

    struct addrinfo *ai;

    if (argc < 2)

        err_quit("usage: tcpcli [-g|-G] <hostname> ... <hostname>");

    optopt = 0; /* 不让 getopt() 写入 stderr */

    while ((c = getopt(argc, argv, "gG")) != -1) {

        switch (c) {

            case 'g': /* 松散路由 */

                if (ptr)

                    err_quit("can't use both -g and G");
```

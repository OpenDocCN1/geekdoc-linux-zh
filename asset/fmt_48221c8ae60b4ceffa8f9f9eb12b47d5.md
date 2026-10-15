
清单 13.1 中显示的服务器在功能上分为以下几个部分：

- 股票指数表在第 27 到 39 行中声明。定义了四个指数，带有起始值和粗糙的波动性值形式，用于模拟。

- 第 44 到 58 行的函数`initialize()`被调用一次以初始化模拟。

- 调用函数`gen_quote()`随机更改随机选择的股票指数的模拟值（第 63 到 77 行）。

- 构成服务器基础的`main()`程序包含在第 92 到 222 行中。

这个股票市场服务器的基本操作如下：

- 默认地址在第 106 和 107 行中声明。当没有提供命令行参数时，使用这些地址。

- 如果提供了两个命令行参数，则服务器地址从第二个参数获取地址（第 114 行）。

- 如果提供一个或多个命令行参数，则广播参数从参数一获取（第 118 行）。

- 形成服务器地址（第 123 到 132 行）。

- 形成广播地址（第 137 到 146 行）。

- 创建一个套接字（第 151 到 153 行）。

- 在套接字上启用`SO_BROADCAST`选项（第 158 到 165 行）。

- 绑定服务器地址（第 172 到 177 行）。

- 初始化股票指数（第 182 行）。

- 服务器循环从第 184 行开始。

服务器无限循环。你需要终止它才能结束其执行。

服务器循环使用以下步骤：

- 通过调用`gen_quote()`更新随机选择的指数（第 188 行）。

- 提取所有指数的报价并格式化到缓冲区中（第 193 到 203 行）。这创建了一个包含四行文本的字符串，对应每个股票指数。

- 使用`sendto(2)`函数发送格式化字符串（第 208 到 216 行）。此调用执行广播，因为地址`adr_bc`包含一个广播地址。

- 进行四秒钟的`sleep(3)`调用，以模拟报价更新之间合理的时间延迟。

- 循环从步骤 1 重复。

这里有几个要点值得回顾：

- 套接字必须启用`SO_BROADCAST`选项。否则，不允许从此套接字进行广播。

- `sendto(2)`调用执行了广播，因为目标地址是一个广播地址。

这两个条件都是广播的先决条件。套接字必须启用广播，并且目标地址必须是一个广播 IP 地址。

要编译此程序，使用以下命令：

```
$ make stksrv
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type -g stksrv.c
gcc -c -D_GNU_SOURCE -Wall -Wreturn-type -g mkaddr.c
gcc -g stksrv.o mkaddr.o -o stksrv
$
```

![](img/961a0296fe36074690a9847b79332eff_355_0.png)

在测试服务器之前，我们必须编译并理解客户端程序。

## 接收广播

将要介绍的客户端程序必须侦听股票市场指数程序将发出的广播。清单 13.2 说明将使用的客户端程序源代码。

## 接收广播

列表 13.2：`quotes.c`。—— 股票市场指数客户端程序

![](img/961a0296fe36074690a9847b79332eff_356_0.png)

```c
/* quotes.c:
 *
 * Get datagram stock market
 * quotes from UDP broadcast:
 */
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <time.h>
#include <signal.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

#ifndef TRUE
#define TRUE 1
#define FALSE 0
#endif

extern int mkaddr(
             void *addr,
             int *addrlen,
             char *str_addr,
             char *protocol);

/*
 * This function reports the error and
 * exits back to the shell:
 */
static void
bail(const char *on_what) {
      fputs(strerror(errno),stderr);
      fputs(": ",stderr);
      fputs(on_what,stderr);
      fputc('\n',stderr);
      exit(1);
}

int
main(int argc,char **argv) {
      int z;
      int x;
      struct sockaddr_in adr;    /* AF_INET */
      int len_inet;          /* length */
      int s;           /* socket */
      char dgram[512];       /* Recv buffer */
      static int so_reuseaddr = TRUE;
      static char
       *bc_addr = "127.255.255.255:9097";

  /*
   * Use a server address from the command
   * line, if one has been provided.
   * Otherwise, this program will default
   * to using the arbitrary address
   * 127.0.0.23.
   */
  if ( argc > 1 )
    /* Broadcast address: */
    bc_addr = argv[1];

  /*
   * Create a UDP socket to use:
   */
  s = socket(AF_INET, SOCK_DGRAM, 0);
  if ( s == -1 )
    bail("socket()");

  /*
   * Form the broadcast address:
   */
  len_inet = sizeof adr;

  z = mkaddr(&adr,
    &len_inet,
    bc_addr,
    "udp");

  if ( z == -1 )
    bail("Bad broadcast address");

  /*
   * Allow multiple listeners on the
   * broadcast address:
   */
  z = setsockopt(s,
    SOL_SOCKET,
    SO_REUSEADDR,
    &so_reuseaddr,
    sizeof so_reuseaddr);

  if (z == -1)
    bail("setsockopt(SO_REUSEADDR)");

  /*
   * Bind our socket to the broadcast address:
   */
  z = bind(s,
    (struct sockaddr *)&adr,
    len_inet);

  if (z == -1)
    bail("bind(2)");

  for (;;) {
    /*
     * Wait for a broadcast message:
     */
    z = recvfrom(s,       /* Socket */
       dgram,       /* Receiving buffer */
       sizeof dgram, /* Max rcv buf size */
       0,       /* Flags: no options */
       (struct sockaddr *)&adr, /* Addr */
       &x);       /* Addr len, in & out */

    if (z < 0)
      bail("recvfrom(2)"); /* else err */

    fwrite(dgram,z,1,stdout);
    putchar('\n');

    fflush(stdout);
  }

  return 0;
}
```

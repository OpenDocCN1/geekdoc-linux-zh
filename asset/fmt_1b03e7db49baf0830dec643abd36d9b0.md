
```c
void
str_cli(FILE *fp, int sockfd) {

    char sendline[MAXLINE];

    struct args args;

    struct result result;

    while (fgets(sendline, MAXLINE, fp) != NULL) {

        if (sscanf(sendline, "%d%d", &args.arg1, &args.arg2) != 2) {

            printf("input: %s\n", sendline);

            continue;

        }

        write(sockfd, &args, sizeof(args));

        if (Readn(sockfd, &result, sizeof(result)) == 0) {

            err_quit("str_cli: server terminated prematurely");

        }

        printf("%d\n", result.sum);

    }

}
```

> 图 5.19 `str_cli` 函数，它向服务器发送两个二进制整数。

`sscanf` 将参数从文本转换为二进制格式，我们调用 `write` 将结构体发送到服务器。
我们调用 `read` 读取回复，并使用 `printf` 返回结果。

> 图 5.20 显示了我们的 `str_echo` 函数。

```c
#include "unp.h"
#include "sum.h"

void
str_echo(int sockfd) {
    size_t n;
    struct args args;
    struct result result;
    for ( ; ) {
        if ((n = Readn(sockfd, &args, sizeof(args))) == 0) {
            return; /* 连接由另一端关闭 */
        }
        result.sum = args.arg1 + args.arg2;
        write(sockfd, &result, sizeof(result));
    }
}
```

> 图 5.20 `str_echo` 函数，它计算两个二进制整数之和。

## TCP 客户端/服务器示例

9-14 我们通过调用 `read` 读取参数，计算并存储和，然后调用 `write` 将结构体发回。

如果我们在两台架构相同的机器上运行客户端和服务器（例如 SPARC 机器），一切运行正常。此处是客户端的交互过程：

```
solaris % tcpcli19 12.106.32.254
11 22
33
-11 -44
-55
我们输入这些
这是服务器的回复
```

当客户端和服务器位于两台架构不同的机器上时（例如服务器位于大端序 SPARC 系统 `freebsd` 上，而客户端位于小端序 Intel 系统 `linux` 上），程序就无法正常工作。

```
linux % tcpcli19 206.168.112.96
1 2
3
-22 -77
-16777314
我们输入这些
它工作正常
然后我们输入这些
但它无法正常工作了
```

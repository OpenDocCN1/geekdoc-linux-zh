
| 函数 | 参数 | 描述 |
|---|---|---|
| / | 不适用 | 将栈顶的上一个数字除以栈顶数字。整数结果将替换栈顶的这两个数字。 |
| % | 不适用 | 将栈顶的两个数字替换为栈顶数字除以上一个数字的模运算结果（余数）。 |
| = | 不适用 | 栈顶结果被弹出栈并返回给客户端。 |
| dump | 不适用 | 整个栈被转储回客户端。栈保持不变。 |

列表 11.1 展示了一个简单计算过程。然后在退出服务器之前，测试了 `dump` 和 `=` 函数。

![](img/961a0296fe36074690a9847b79332eff_289_0.png)

```text
$ telnet localhost 9090
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
#:3
0:
#:4
1:
#:7
2:
dump
2:7
1:4
0:3
E:end of stack dump
+
1:
dump
1:11
0:3
E:end of stack dump
*
0:
dump
0:33
E:end of stack dump
=
0:33
dump
E:end of stack dump
```

```text
`-]
telnet> c
Connection closed.
$
:`
```

该会话演示了如何计算以下内容：
3 * (4 + 7)

在列表 11.1 中执行的步骤如下：

1.  三个值 3、4 和 7 首先被压入栈中。
2.  使用 `dump` 操作转储栈。
3.  执行 `+` 操作，导致计算 4 + 7，并将其结果 11 放在栈顶以替代输入值。
4.  再次使用 `dump` 转储栈。由此可以看出，值 3 和 11 仍保留在栈中。
5.  输入 `*` 时，计算 3 * 11 的乘法。结果 33 替代了栈上的输入值。
6.  再次执行 `dump` 操作以显示栈内容。它显示栈上的单个结果 33。
7.  `=` 操作将此最后一个值从栈中弹出。
8.  此时 `dump` 操作显示空栈。
9.  使用 CTRL+1，然后输入字符 `c` 并回车，关闭 telnet 会话。

服务器支持的一元函数显示在表 11.2 中。

| 函数 | 参数 | 描述 |
|---|---|---|
| abs | 不适用 | 栈顶值被替换为该数字的绝对值。 |
| neg | 不适用 | 栈顶值被替换为该数字的相反数。 |
| sqrt | 不适用 | 栈顶值被替换为该数字的整数平方根。 |

请注意，一元函数只需要栈上存在一个数字。表 11.3 列出了一些 RPN 服务器支持的更高级的函数。

### 表 11.3：高级 RPN 服务器函数

| 函数 | 参数 | 描述 |
| :--- | :--- | :--- |
| gcd | 不适用 | 计算栈顶两个数字之间的最大公因数。结果替换栈顶的两个数字。 |
| seed | 不适用 | 使用栈顶值作为随机数种子值。没有结果被压入栈中。 |
| random | 不适用 | 使用栈顶值作为要生成的随机数的最大值 + 1。随机结果替换栈上的输入值。 |
| tprime | 不适用 | 测试栈顶值是否为素数。栈顶倒数第二个数字表示要应用的测试次数。典型值为 25。结果替换栈上的两个输入值。结果 1 表示该数字可能是素数，而 0 表示该数字不是素数。 |
| genprime | 不适用 | 生成一个素数，使用栈顶值作为“最大随机数 + 1”值（参见 `random`）。栈上倒数第二个数字表示要执行的测试次数（通常为 25）。生成的结果替换顶部的两个值。 |
| swap | 不适用 | 交换栈顶的两个值。用于交换两个数字时很有用。 |
| dup | 不适用 | 复制栈顶的值。 |

使用 `seed` 和 `random` 函数需要稍作解释。`seed` 函数允许您以可预测的方式为随机数生成器设置种子。如果您希望重现一组随机数以进行后续测试，这一点很重要。例如：

![](img/961a0296fe36074690a9847b79332eff_291_0.png)

```text
#:1000
0:
seed
0:
#:3000
0:
random
0:
dump
0:560
```

此序列使用值 1000 为随机数生成器设置种子。稍后，3000 被输入到函数 `random`，产生随机数 560。值 3000 作为 `random` 函数的最大值 + 1。以此作为输入值，生成的随机数可能在 0 到 2999 之间。

`genprime` 函数的作用方式类似。以如下为例：

```text
#:25
0:
#:9999999999999999999999999999999999
1:
```
输出：
```text
genprime
0:
dump
0: 731694666996633312605231309328347
E: end of stack dump
```

此示例展示了如何生成一个大素数。推入的值 25 导致生成的数字被测试 25 次以查看它是否为素数。如果您需要更可靠地保证该数字是素数，必须使用更大的测试值。函数 `tprime` 的作用方式相同，只是它产生零或一的测试结果。一表示该数字被测试为可能是素数。

> **注意**
>
> 素数测试是通过 GMP 库函数 `mp2_probab_prime_p()` 实现的。该函数实现了基于 Donald E. Knuth 的研究的“概率素性测试”，见 *The Art of Computer Programming*，第 2 卷，*Seminumerical Algorithms*，第 2 版，Addison-Wesley，1981。
>
> 函数的结果表明该数字是素数的概率很高。返回假阳性指示的概率为 $(1/4)^r$，其中 $r$ 表示要执行的测试次数。文档指出 $r$ 的值 25 是一个合理的数字。

## 使用 fork(2) 服务多个客户端

第 10 章中开发的服务器在本节中进行了修改，通过 `fork(2)` 系统调用处理多个客户端。列表 11.2 显示了修改后的 `rpsrv.c` 模块的列表。所有其他源模块保持与前一章中出现的一样。

```c
/* Listing 11.2: rpsrv.c—The fork(2) Modified RPN Server */

/* rpsrv.c:
 *
 * Example RPN Server:
 */
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <errno.h>
#include <string.h>
#include <time.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <netdb.h>
#include <sys/wait.h>
#include <signal.h>

#ifndef SHUT_RDWR
#define SHUT_RDWR 3
#endif

extern int mkaddr(void *addr,
                  int *addr_len,
                  char *input_address,
                  char *protocol);

extern void rpn_process(FILE *tx,
                        char *buf);

/*
 * Process Terminated Child processes:
 */
static void
sigchld_handler(int signo) {
    pid_t PID;
    int status;

    do {
        PID = waitpid(-1, &status, WNOHANG);
    } while (PID != -1);

    /* Re-instate handler */
    signal(SIGCHLD, sigchld_handler);
}

/*
 * This function reports the error and
 * exits back to the shell:
 */
static void
bail(const char *on_what) {
    if (errno != 0) {
        fputs(strerror(errno), stderr);
        fputs(": ", stderr);
    }
    fputs(on_what, stderr);
    fputc('\n', stderr);
    exit(1);
}

int
main(int argc, char **argv) {
    int z;
    char *srvr_addr = "127.0.0.1:9090";
    struct sockaddr_in adr_srvr; /* AF_INET */
    struct sockaddr_in adr_clnt; /* AF_INET */
    int len_inet;
    int s = -1;  /* Socket */
    int c = -1;  /* Client socket */
    FILE *rx = NULL;  /* Read stream */
    FILE *tx = NULL;  /* Write stream */
    char buf[4096];  /* I/O Buffer */
    pid_t PID;  /* Process ID */

    /*
     * Set signal handler for SIGCHLD:
     */
    signal(SIGCHLD, sigchld_handler);

    /*
     * Use a server address from the command
     * line, otherwise default to 127.0.0.1:
     */
    if (argc >= 2)
        srvr_addr = argv[1];

    len_inet = sizeof adr_srvr;
    z = mkaddr(&adr_srvr, &len_inet,
               srvr_addr, "tcp");

    if (z < 0 || !adr_srvr.sin_port) {
        fprintf(stderr, "Invalid server "
                "address, or no port number "
                "was specified.\n");
        exit(1);
    }

    /*
     * Create a TCP/IP socket to use:
     */
    // continues
```


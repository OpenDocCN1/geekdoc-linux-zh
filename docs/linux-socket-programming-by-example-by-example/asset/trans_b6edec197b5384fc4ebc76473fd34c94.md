
# 解决报价服务问题

![](img/961a0296fe36074690a9847b79332eff_492_0.png)

*图 18.1：Netscape 获取到 RHAT 股票报价后的屏幕截图，网址为* `http://finance.yahoo.com.`

从这里，你有三个选择：

- 将鼠标移到“下载电子表格格式”链接上，并记下状态行上显示的 URL（Netscape 4.7 在那里显示链接 URL）。

- 从菜单项 视图->页面源代码 中选择。在 HTML 代码中寻找类似 `<a href="/d/quotes.csv?ts=RHAT&f=s!1d1tclc1oghwg&f=.csv">Download Spreadsheet Format</a>` 的链接（通过寻找 *Download Spreadsheet Format* 来定位它）。

- 使用 Netscape 获取此信息的最佳方式是右键点击“下载电子表格格式”链接。从弹出的菜单中，选择“复制链接位置”项。这将把链接引用复制到你的剪贴板。然后，你可以稍后将这些信息粘贴到一个文件中。

## 第 18 章：一个实际的联网项目

凭借这些信息，你将拥有所需的一切。按照以下步骤使用 telnet 测试该功能（请记住在主机名后提供 80）：

```
$ telnet finance.yahoo.com 80
Trying 204.71.201.75...
Connected to finance.yahoo.com.
Escape character is '^]'.
GET /dq/quotes.csv?s=RHAT&f=ss11d1tc1of9hq&a=.csv
"RHAT",168.9375,'11/24/1999','4:00PM',0,147.5625,175.5,145.6875,3661700
Connection closed by foreign host.
$
```

![](img/961a0296fe36074690a9847b79332eff_493_0.png)

在你连接之后，发出 GET 命令，并附带一个看起来奇怪的 pathname 以及按下 Enter 键（你可能需要按两次 Enter）。如果成功，你将获得一行电子表格数据作为回报！用另一个符号替换 RHAT 将获得不同的数据。

如果你没有遇到好运，请检查你的标点符号和拼写。在这里，准确性至关重要。如果可能，请使用屏幕上的剪切和粘贴。如果这没有帮助，那么你需要研究 finance.yahoo.com 目前是如何做的（你甚至可能需要从 yahoo.com 主页开始）。按照之前概述的步骤操作，以便能够找出所需的新主机名和 pathname。

以下是获取报价过程的摘要：

1. 连接到端口 80 的 finance.yahoo.com（该主机名可能会在未来某个日期更改）。
2. 发出带有所示魔法 pathname 的 GET 请求（单词 GET 应为大写）。
3. 一行电子表格格式的数据在同一套接字上作为响应返回。
4. 套接字关闭。

这就是全部了！当你稍后审查源代码列表时，请记住这些步骤。

接下来的章节将展示并描述组成服务器和客户端程序的模块。不幸的是，空间不允许列出完整的源代码。但是，完整的源代码和 make 文件可在 http://www.quecorp.com/series/by_example/ 获取。

表 18.1 列出了你需要的所有源文件。本章中将会列出并描述其中一些更有趣的文件。

### 表 18.1：报价服务器和客户端的源模块

| 源文件 | 描述 |
|---|---|
| Makefile | 项目 make 文件。 |
| bcast.c | 实现执行向局域网广播报价的函数。 |
| connect.c | 实现连接到远程互联网报价服务器的函数。 |
| csparse.c | 解析返回的报价数据的解析器... |
| getick.c | 从远程互联网报价服务器获取报价信息。 |
| load.c | 从文件 tickers.rc 加载股票市场代码。 |
| misc.c | 小型杂项函数。 |
| mkaddr.c | 互联网地址便利函数。 |
| mktwatch.c | 市场监控客户端程序。此程序接收本地广播信息并显示它。 |
| msgf.c | 将服务器消息记录到 syslog 日志记录的模块。 |
| qserve.c | 实现本地报价服务器程序的模块。 |
| quotes.h | 所有源模块的公共头文件。 |
| tickers.rc | 需要查询的代码列表。修改此文件以更改为你感兴趣的代码。 |

## 检查报价服务器程序

开始检查代码的逻辑位置是 qserve.c 源模块。此模块构成了报价服务器本身的主程序。它负责获取股票行情并广播到局域网。清单 18.1 显示了 qserve.c 的源代码列表。

### 清单 18.1：qserve.c—报价服务器模块

```c
/* qserve.c:
 *
 * Stock Quote Concentrator Program:
 */
#include "quotes.h"

static char *command = NULL;

/* Remote Quote Server Address */
static char *cmdopt_a = DFLT_SERVER;

/* Quote Re-Broadcast Address */
static char *cmdopt_b = DFLT_BCAST;

/* Ticker Table: */
static TickReq tickers[MAX_TICKERS];
static int ntick = 0;

/* Return server usage information: */
static void
usage(void) {
    printf("Usage: %s [-h] -a address:port\n"
           "where:\n"
           "\t-t\tRequests usage info,\n"
           "\t-a address:port\tSpecify "
           "the server\n"
           "\t\taddress and port number.\n"
           "\t-b bcast:port\tSpecify "
           "the broadcast\n"
           "\t\taddress and port number.\n",
           command);
}

/* Server Main Program: */
int
main(int argc, char **argv) {
    int rc = 0; /* Return Code */
    int optch;  /* Option Char. */
    int z;      /* Status Code */
    int x;      /* Index */
    int s;      /* Broadcast socket */
    time_t tn = 0; /* Time Next */
    time_t tzz;   /* Sleep Time */
    time_t tm = 20; /* Seconds */
    time_t td;    /* Time + Date */
    struct sockaddr_in bc_addr; /* bc addr */
    socklen_t bc_len; /* bc addr len. */
    const int True = TRUE; /* Const. TRUE */
    static char cmdopts[] = "ha:b:";

    /* Process command line options: */
    command = Basename(argv[0]);

    while ( (optch = getopt(argc, argv, cmdopts)) != -1 )
        switch ( optch ) {
        case 'h' :               /* -h for help */
            usage();
            return rc;

        case 'a' :               /* -a quote_server */
            cmdopt_a = optarg;
            break;

        case 'b' :   /* -b broadcast_addr */
            cmdopt_b = optarg;
            break;

        default :
            /* Option error */
            rc = 1;
        }

        /*
         * Check for option errors:
         */
        if ( rc ) {
            usage();
            return rc;
        }

        /*
         * Form the broadcast server
         * address:
         */
        bc_len = sizeof bc_addr;   /* Max len */
        z = mkaddr(
                &bc_addr,        /* Returned addr. */
                &bc_len,        /* Returned len. */
                cmdopt_b,       /* Input address */
                "udp" );        /* UDP protocol */

        if ( z == -1 ) {
            msgf("e", "%s: -b %s", 
                 strerror(errno),
                 cmdopt_b);
            return 1;
        }

        /*
         * Create a UDP socket to use:
         */
        s = socket(AF_INET, SOCK_DGRAM, 0);

        if ( s == -1 ) {
            msgf('e', "s: socket(AF_INET, "
                 "SOCK_DGRAM,0)",
                 strerror(errno));
            return 1;
        }

        /*
         * Allow broadcasts on socket s:
         */
        z = setsockopt(s,
                 SOL_SOCKET,
                 SO_BROADCAST,
                 &True,
                 sizeof True);

        if ( z == -1 ) {
            msgf('e', "s: setsockopt(SO_BROADCAST)",
                 strerror(errno));
            return 1;
        }

        /*
         * Load tickers from tickers.rc:
         */
        if ( load(&tickers[0], &ntick, MAX_TICKERS) )
            goto errxit;

        /*
         * Now monitor the remote quote server:
         */
        for (;;) {
            tn = 0;                /* Refresh tn */
            time(&td);            /* Current time */

            /*
             * Loop for all tickers:
             */
            for ( x=0; x<ntick; ++x ) {
                /*
                 * Get quote for ticker x
                 */
            }
        }
    }
}
```


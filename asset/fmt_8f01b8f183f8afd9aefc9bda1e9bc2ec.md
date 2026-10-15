
### 用服务器地址填充套接字地址结构

9-12 `IPv4` 套接字地址结构被服务器的 IP 地址和端口号填充。这将传递给 `dg_cli`，指定向何发送数据报。

13-14 创建一个 UDP 套接字并调用函数 `dg_cli`。

## 8.6 UDP Echo 客户端：`dg_cli` 函数

图 8.8 显示了 `dg_cli`，它执行了大部分的客户端处理。

图 8.8 `dg_cli` 函数：客户端处理循环。

`lib/dg_cli.c`

```c
1 #include "unp.h"

2

3 void

4 dg_cli(FILE *fp, int sockfd, const SA *pservaddr, socklen_t servlen)

5 {

6     int n;

7     char sendline[MAXLINE], recvline[MAXLINE + 1];

8     while (fgets(sendline, MAXLINE, fp) != NULL) {

9         sendto(sockfd, sendline, strlen(sendline), 0, pservaddr, servlen);

10         n = recvfrom(recvline, MAXLINE, 0, NULL, NULL);

11         recvline[n] = 0; /* 字节结束符 */

12         fputs(recvline, stdout);

13     }

14 }
```

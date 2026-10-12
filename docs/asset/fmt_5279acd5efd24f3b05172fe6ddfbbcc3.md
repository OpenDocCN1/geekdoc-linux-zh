
```c
1:  /* af_inet.c:
2:   *
3:   * Establishing a Specific AF_INET
4:   * Socket Addresses:
5:   */
6:
7:  #include <stdio.h>
8:  #include <unistd.h>
9:  #include <errno.h>
10: #include <string.h>
11: #include <sys/types.h>
12: #include <sys/stat.h>
13: #include <sys/socket.h>
14: #include <netinet/in.h>
15:
16: /*
17:  * This function reports the error and
18:  * exits back to the shell:
19:  */
20: static void
21: bail(const char *on_what) {
22:     perror(on_what);
23:     exit(1);
24: }
25:
26: int
27: main(int argc,char **argv,char **envp) {
28:     int z;                /* Status return code */
29:     int sock_inet;        /* Socket */
30:     struct sockaddr_in adr_inet; /* AF_INET */
31:     int len_inet;         /* length */
32:     const unsigned char IPno[] = {
33:         127, 0, 0, 23    /* Local loopback */
34:     };
35:
36:     /* Create an IPv4 Internet Socket */
37:     sock_inet = socket(AF_INET,SOCK_STREAM,0);
38:
39:     if ( sock_inet == -1 )
40:         bail("socket()");
41:
42:     /* Create an AF_INET address */
43:     memset(&adr_inet,0,sizeof adr_inet);
44:
45:       adr_inet.sin_family = AF_INET;
46:       adr_inet.sin_port = htons(9000);
47:       memcpy(&adr_inet.sin_addr.s_addr,IPno,4);
48:       len_inet = sizeof adr_inet;
49:
50:       /* Now bind the address to the socket */
51:       z = bind(sock_inet,
52:                (struct sockaddr *)&adr_inet,
53:                len_inet);
54:
55:       if ( z == -1 )
56:           bail("bind()" );
57:
58:       /* Display all of our bound sockets */
59:       system("netstat -pa --tcp 2>/dev/null | `sed -n '1,/Proto:/af_inet/p'");
60:
61:       close(sock_inet);
62:       return 0;
63:    }
```

此程序中使用的步骤与列表 `2.3` 和 `2.5` 中显示的其他步骤几乎相同。然而，第 `43` 到 `48` 行需要一些解释：

- `1.` 第 `30` 行使用名称 `adr_inet` 定义了 `sockaddr_in` 结构体。此外，套接字地址长度在第 `31` 行定义为整数 `len_inet`。
- `2.` 在第 `32` 和 `33` 行中，定义了一个无符号字符数组 `IPno[4]`。在这里，单独的字节拼出了一个特定的 IP 地址 `127.0.0.23`。
- `3.` 第 `43` 行像往常一样将 `adr_inet` 清零。注意，这再次是可选的。
- `4.` 第 `45` 行将地址族建立为 `AF_INET`。
- `5.` 此示例选择在第 `46` 行建立 TCP/IP 端口号 `9000`。注意第 `46` 行中使用了转换函数 `htons(3)`。
- `6.` 字符数组 `IPno[4]` 被复制到第 `47` 行的位置 `adr_inet.sin_addr.s_addr`。由于字节在步骤 `2` 中已定义为网络序，因此这里不需要字节序转换。您会记得，网络字节序中最高有效字节在前。
- `7.` 地址结构的大小像以前一样计算（第 `48` 行）。

您可能已经注意到 Internet 地址具有固定长度。如果您查看图 `2.3`，这一点显而易见。然而，您会记得 `AF_LOCAL` 地址的长度是可变长度（参见图 `2.2`）。对于 `AF_INET` 地址，您只需提供套接字结构体 `sockaddr_in` 的大小即可。用 C 语言术语来说，这就是

```c
sizeof(struct sockaddr_in)
```

现在，您应该已经具备了构建 Internet IPv4 地址的能力。为了拓宽您在套接字寻址方面的知识，接下来的章节将向您展示如何指定其他一些地址族。

## 指定 X.25 地址

套接字接口允许程序员在 Linux 下使用其他协议，且几乎不需要付出努力。代码中唯一的主要不同之处在于套接字的寻址方式。您已经看到了 `AF_LOCAL` 和 `AF_INET` 地址所需的初始化。`X.25` 地址的创建非常相似。

用于定义 `X.25` 协议地址的结构体是 `sockaddr_x25` 结构体。定义该结构体的包含语句如下：

```c
#include <linux/x25.h>
```

列表 `2.10` 显示了 `AF_X25` 地址族的套接字地址结构体。

![](img/961a0296fe36074690a9847b79332eff_72_0.png)

**列表 2.10：X.25 套接字地址结构体**

```c
struct sockaddr_x25 {
    sa_family_t sx25_family; /* Must be AF_X25 */
    x25_address sx25_addr; /* X.121 Address */
};

typedef struct {
    char x25_addr[16];
} x25_address;
```

您会注意到，同样地，成员 `sx25_family` 占据了通用套接字结构的前两个字节。对于此地址，它必须具有值 `AF_X25`。

**提示**

> 有关 `X.25` 套接字地址的信息可以在 `x25(4)` 手册页中找到。

`X.25` 网络地址（由 `X.121` 标准定义此地址）由一系列十进制数字组成。程序 `af_x25.c` 已提供，以向您展示如何建立 `X.25` 地址并让 `netstat(1)` 显示它。列表 `2.11` 显示了程序列表。

**示例**

**列表 2.11：** `af_x25.c`—建立 `X.25` 协议地址

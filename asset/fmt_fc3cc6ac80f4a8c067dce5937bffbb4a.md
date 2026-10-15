
```c
6 void
7 send_dns_query(void)
8 {
9     size_t nbytes;
10    char *ptr;
11    buf = malloc(sizeof(struct udphdr)) + 100;
12    ptr = buf + sizeof(struct udphdr);      /* 为 IP/UDP 头部留出空间 */

13    *(uint16_t *)ptr = htons(12344);      /* identification */
14    ptr += 2;
15    *(uint16_t *)ptr = htons(0x0100);   /* flags; 递归 desired */
16    ptr += 2;
17    *(uint16_t *)ptr = htons(1);       /* questions */
18    ptr += 2;
19    *(uint16_t *)ptr = 0;            /* # answer RRs */
20    ptr += 2;
21    *(uint16_t *)ptr = 0;            /* # authority RRs */
22    ptr += 2;
23    *(uint16_t *)ptr = 0;            /* # additional RRs */
24    ptr += 2;

25    memcpy(ptr, "\001a0144-root-servers\003net000", 20);
26    ptr += 2;
27    *(uint16_t *)ptr = htons(1);      /* query type = A */
28    ptr += 2;
29    *(uint16_t *)ptr = htons(1);      /* query class = 1 (IP addr) */
30    ptr += 2;

31    nbytes = (ptr - buf) - sizeof(struct udphdr);
```
```c
udp_write(buf, nbytes);
if (verbose)
    printf(":%d bytes of data\n", nbytes);
```

# 分配缓冲区并初始化指针

11-12 我们使用 `malloc` 分配 `buf`，留有存放 20 字节 IP 头部、8 字节 UDP 头部和 100 字节用户数据的空间。`ptr` 指用户数据的第一个字节。

# 构建 DNS 查询

13-24 要理解此函数构建的 UDP 数据报细节，需要了解 DNS 消息格式。这可以在 TCP IP 的第 14.3 节中找到。我们将标识标签（identification）设置为 1234，标志（flags）设置为 0，问题数量设置为 1，并将回答资源记录 (Rs) 的数量、权威 RRs 的数量以及附加 RRs 的数量设置为 0。25-30 我们将标识标签设置为 1234，标志设置为 0，问题数量设置为 1，并将回答资源记录 (Rs) 的数量、权威 RRs 的数量以及附加 RRs 的数量设置为 0。31-32 `nbytes = (ptr - buf) - sizeof(struct udphdr);` 32-45 当计算 UDP 校验和时，它包含了 UDP 头部和数据，还包含了 IP 头部的字段。这些 IP 头部的字段构成了伪头部（pseudheader）。伪头部的引入确保了如果校验和正确，则数据包已发送到正确的主机。这些语句初始化了构成伪头部的 IP 头部字段。代码虽然有些晦涩，但在第 23.6 节中会有解释。

# 初始化指针

24-ip 指向 IP 头部开头，ui 指向相同位置，udphdr

# 清零头部

27 我们显式地将头部区域置零，以避免校验缓冲区中的残留数据。之前的版本代码显式地将结构体的所有元素置零；但该结构体在不同系统间有所不同。这是构建头部时的典型移植性问题。

# 更新长度

28-ui_len 是 UDP 长度：用户数据的字节数加上 UDP 头部的大小（8 字节）。user_len（UDP 头部之后的用户数据）增加 28（20 字节 IP 头部和 8 字节 UDP 头部）以反映 IP 数据包的总大小。

# 填充 UDP 头部并计算校验和

32-45 当计算 UDP 校验和时，它包含了 UDP 头部和数据，还包含了 IP 头部的字段。这些 IP 头部的字段构成了伪头部。伪头部的引入确保了如果校验和正确，则数据包已发送到正确的主机。这些语句初始化了构成伪头部的 IP 头部字段。代码虽然有些晦涩，但在第 23.6 节中会有解释。

# 声明套接字描述符

2 我们声明一个全局变量来持有描述符。

# 创建原始套接字并开启 IP_HDR

7-13 我们创建一个原始套接字并开启 `IP_INCL`。此选项允许我们写入自己的头部。

# 图 29.13 open_output 函数：准备原始套接字。

```c
udpcksum/udpwrite.c

int rawfd;
void
open_output(void);
5 {
  int on = 1;
  /*
   * 需要原始套接字。进程必须具有超级用户权限才能创建此套接字。
   * 还要设置 IP_INCL 以便写入自己的头部。
   */
11
   rawfd = socket(dest->sa_family, SOCK_RAW, 0);
12
   setsockopt(rawfd, IPPROTO_IP, IP_HDRINCL, &on, sizeof(on));
13 }
```

图 14 显示了函数 `udp_write`，它构建了 IP 和 UDP 头部。

我们注意到，Solaris 2.x（对于 x < 6）在带有 `IP_HDRINCL` 套接字选项的原始套字上，TCP 段和 UDP 数据报的校验和存在一个 Bug。内核会计算校验和，我们必须将 `ip_sum` 字段设置为 UDP 长度。

## 填充 IP 头部

46-59 由于我们使用了 `IP_HDRINCL` 套接字选项，我们必须填充 IP 头部中的大部分字段。（第 28.3 节讨论了设置此套接字选项时向原始套接字写入的内容）。我们将标识设置为 0 (`ip_id`)，这告诉 IP 设置此 IP 头部校验和。`sendto` 会写入 IP 头部。

注意，我们根据所使用的操作系统，以主机字节序或网络字节序设置 `ip_len` 字段。这是使用原始套接字时的可移植性问题。

下一个函数是图 29.15 中的 `udp_read`，它是在图 29.10 中调用的。

## 29.14 udp_write 函数：构建 UDP 和 IP 头部并将 IP 图形写入原始套接字。

`udpchecksum/udpwrite.c`


最后，我们来看一个新的函数 `sctp_print_addresses`，它将以 `sctp_getaddrs` 和 `sctp_getladdrs` 返回的形式打印地址列表。

### 图 23.12 地址列表。

```c
#include "unp.h"

void sctp_print_addresses(struct sockaddr_storage *addrs, int num)
{
    struct sockaddr_storage *ss;
    int i, salen;

    ss = addrs;
    for (i = 0; i < num; i++) {
        printf("%s\n", Sock_ntop((SA *) ss, salen));
#ifdef HAVE_SOCKADDR_SA_LEN
        salen = (ss->ss_family);
#else
        switch (ss->ss_family) {
            case AF_INET:
                salen = sizeof(struct sockaddr_in);
                break;
#ifdef IPv6
            case AF_INET6:
                salen = sizeof(struct sockaddr_in6);
                break;
            default:
                err_quit("sctp_print_addresses: unknown AF");
                break;
        }
#endif
        ss = (struct sockaddr_storage *) ((char *) ss + salen);
    }
}
```

#### 处理每个地址

7-8 该函数根据调用者指定的地址数量遍历每个地址。

#### 打印地址

9 我们使用 `sock_ntop` 函数打印地址。请记住，该函数会打印系统支持的任何套接字地址结构格式。

#### 确定地址大小

10-26 地址列表是一个紧凑列表（packed list），而不是 `sockaddr_storage` 结构的简单数组。这是因为 `sockaddr_storage` 结构很大，在内核和用户空间之间来回传递地址时使用它太浪费资源了。在 `sockaddr` 结构包含自身长度的系统中，这是轻而易举的：只需从当前的 `sockaddr_storage` 结构中提取长度即可。在其他系统中，我们根据地址族选择长度，如果地址族未知，则带错误错误退出。

#### 移动地址指针

27 该函数现在将地址的大小加到基指针上，以便在地址列表中向前移动。

### 运行代码

我们如下所示对服务器运行了修改后的客户端：

```
FreeBSD-lap: ./tcpclient01 10.1.1.5
[0]Hi
有 2 个远程地址，它们是：
10.1.1.5:9877
127.0.0.1:9877
有 2 个本地地址，它们是：
10.1.1.5:1025
127.0.0.1:1025
From str:0 seq:0(assoc:c99e2680):[0]Hi
Ctrl-B
FreeBSD-lap:
```

# 23.8 查找关联 IP 地址

在 23.7 节中对客户端所做的最近更改中，客户端关联通知（association notification）来触发其地址的检索。这种通知非常方便，因为它在 `sac_assoc_id` 中保存了关联标识符。但如果应用程序没有跟踪关联标识符而只有对端的地址，它如何找到关联标识符呢？在图 23.13 中，我们展示了一个将对端地址转换为关联 ID 的简单函数。服务器将在后的 23.10 节中使用此函数。

#### 初始化

7-8 我们的第一个函数初始化了它的 `sctp_paddrparams` 结构。

#### 复制地址

9 使用传递的长度将地址复制到 `sctp_paddrparams` 结构中。

#### 调用套接字选项

10 该函数现在使用 `SCTP_PEER_ADDR_PARAMS` 套接字选项请求对端地址参数。注意，我们使用的是 `sctp_opt_info`而不是 `getsockopt`，因为 `SCTP_PEER_ADDR_PARAMS` 套接字选项需要将参数拷贝进出内核。这将返回当前的心跳间隔、在 SCTP 实现认为对端地址失败之前的最大重传次数，以及最重要的关联 ID。注意，我们没有返回该值，因为如果调用失败，我们将返回 0。

### 图 23.13 将地址转换为关联 ID。

`sctp/sctp_addr_to_assoc.c`

```
1 #include "unp.h"
2 sctp_assoc_t
3 sctp_addr_to_assoc(int sock_fd, struct sockaddr *sa, socklen_t salen)
4 {
5     struct sctp_paddrparams sp;
6     int size;
7
 size = sizeof(struct sctp_paddrparams);
8 bzero(&sp, size);
9 memcpy(&sp.pp_address, sa, salen);
10 sctp_opt_info(sock_fd, 0, SCTP_PEER_ADDR_PARAMS, &sp, &size);
11 return (sp.sp_assoc_id);
12 ```
```

`!!` 该函数返回关联 ID。注意，如果调用失败，我们将返回 0。`sctp_paddrparams` 结构用于告知调用者 ID。

# 23.9 心跳与地址失败

SCTP 提供了一种类似于 TCP 留存存（keep-alive）的心跳机制。在 23.8 节中看到的 `sctp_paddrparams` 结构允许应用程序控制心跳。在 SCTP 中，心跳是默认开启的。如果没有干预，`sctp_paddrparams` 结构中的 `pp_interval` 字段设置为 `SCTP_NO_HB(0)` 则禁用心跳。如果设置为 `SCTP_ISSUE_HB(xffffffff)` 则请求即时心跳。其他值设置心跳间隔。该值是心跳之间的间隔。在图 23.14 中，我们展示了一个设置心跳间隔的小函数。使用 `SCTP_PEER_ADDR_PARAMS` 套接字选项可以设置心跳超时，在目标变为不可达之前。`sctp_paddrparams` 结构用于设置心跳。

### 图 23.14 心跳控制工具。

`sctp/sctp_modify_hb.c`

```
1 #include "unp.h"

2 int heartbeat_action(int sock_fd, struct sockaddr *sa, socklen_t salen, int value)

3 {

4     struct sctp_paddrparams sp;

5     int size;

6

7 size = sizeof(struct sctp_paddrparams);

8 bzero(&sp, size);

9 memcpy(&sp.pp_address, sa, salen);

10 if (value == SCTP_NO_HB(0))

11     sp.spp_interval = 0;

12 else if (value == SCTP_ISSUE_HB(xffffffff))

13     sctp_opt_info(sock_fd, 0, SCTP_PEER_ADDR_PARAMS, &sp, &size);

14 else

15     sp.spp_interval = value;

16 sctp_opt_info(sock_fd, 0, SCTP_PEER_ADDR_PARAMS, &sp, &size);

17 return 0;

18 ```
```

#### 设置地址

使用传递的长度将地址复制到 `sctp_paddrparams` 结构中。

#### 调用套接字选项

该函数现在使用 `SCTP_PEER_ADDR_PARAMS` 套接字选项请求对端地址参数。注意，我们使用的是 `sctp_opt_info`而不是 `getsockopt`，因为 `SCTP_PEER_ADDR_PARAMS` 套接字选项需要将参数拷贝进出内核。这将返回当前的心跳间隔、在 SCTP 实现认为对端地址失败之前的最大重传次数，以及最重要的关联 ID。注意，我们没有返回该值，因为如果调用失败，我们将返回 0。

#### 清零参数

我们清空 `sctp_paddrparams` 结构，以确保用户或内核未设置的字段没有垃圾数据。

#### 执行操作

应用程序使用 `sctp_paddrparams` 结构设置心跳间隔。

# 23.10 剥离关联

我们一直在关注 SCTP 提供的一对多接口。这种接口与经典的对一风格相比有以下几个优势：

- 只需要维护一个文件描述符。
- 它允许我们构建一个简单的服务器。
- 无需跟踪状态。

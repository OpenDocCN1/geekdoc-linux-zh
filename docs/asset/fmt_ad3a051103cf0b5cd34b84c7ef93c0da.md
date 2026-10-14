
服务器应用程序是根据服务器的端口号（有时也包括 IP 地址）在系统中识别的。因此，服务器应用程序通过某种方式请求内核，它需要通过特定端口（某些情况下为 IP 地址）标识自己。应用程序通过调用 `bind()` 系统调用来实现这一点。在 `bind()` 返回应用程序后，我们还没有作为服务器准备好。我们只是在内核中注册了自己，但无法服务任何客户端请求。此时，我们需要对套接字进行一些基本配置，这意味着我们需要告诉内核，如果服务器在任何时刻无法处理许多请求，内核应该在该套接字的待处理队列中保留多少连接请求。这是通过调用 `listen()` 系统调用实现的。在 `listen()` 返回应用程序后，我们还没有准备好服务任何客户端请求，因为服务器应用程序需要请求内核现在开始接收客户端请求。为此，该服务器调用 `accept()` 系统调用。通过这种方式，内核初始化了一些特定的数据结构，并实际上将应用程序的服务注册到系统中。`accept()` 系统调用会永久阻塞，直到收到来自客户端的新连接请求。一旦接收到连接，`accept()` 系统调用将返回与新连接关联的新文件描述符。

服务器使用 `accept()` 系统调用返回的文件描述符与客户端通信。我们现在将看到当内核调用这些系统调用时内核会做什么。

## 4.1.2 服务端操作

图 4.1 显示了实现 TCP 服务器程序的系统调用序列。它还对每个系统调用所提供的功能进行了简要描述。

### 4.2 BIND

如所述，`socket()` 系统调用仅在内核中为套接字创建空间。此时，该套接字没有身份，也无法执行任何操作。`bind()` 系统调用为套接字创建一个身份，是创建服务器应用程序的下一步。每个打开的套接字在系统中都需要唯一标识。因为我们有套接字地址的概念。`bind()` 将此套接字地址作为参数之一，内核将此地址与套接字关联。表示此套接字的 C 语言结构是 `struct sockaddr`（见图 4.2）。

- `sa_family`: 这存储了我们之前讨论过的与套接字关联的协议族号。
- `s_data[]`: 此数组包含非常特定于协议的数据。在 `PF_INET` 协议族的情况下，此数组包含 [端口号，IP 地址 (`struct in_addr`)]；

由于我们一直在处理 IP 协议，表示 IP 协议（`PF_INET` 族）套接字地址的 C 结构是 `struct sockaddr_in`（见图 4.3）。套接字地址由三者的组合定义：

- `sin_family`: 这是一个地址族（IP 协议为 `PF_INET`）。
- `s_port`: 这是一个 16 位数字，用于区分同一协议族的不同套接字。
- `s_addr`: 这是一个表示 IP 地址的 32 位数字。在服务器应用程序中，这通常设置为 `INADDR_ANY`，这意味着如果服务器有多个接口（物理/虚拟），它可以接受来自其中任何一个接口的连接。服务器应用程序可以限制来自任何

```c
#include <linux/socket.h>
struct sockaddr {
    unsigned short sa_family;   /* 地址族，AF_*** */
    char sa_data[14];           /* 14 字节的协议地址 */
};
```

图 4.2. 表示套接字地址的 C 结构。

## BIND

```c
#include <linux/in.h>

struct sockaddr_in {
  sa_family_t      sin_family;    /* 地址族 */
  unsigned short int sin_port;     /* 端口号 */
  struct in_addr    sin_addr;      /* Internet 地址 */

  /* _pad                       填充到 'struct sockaddr' 的大小 */
  unsigned char     _pad[SOCK_SIZE - sizeof(unsigned short int)] = 
                                sizeof(unsigned short int) - sizeof(struct in_addr);
};
```

图 4.3. IP 的套接字地址。

`sockaddr_in` 结构允许服务器通过指定绑定不同接口（具有不同 IP 地址）的 IP 地址来接受来自任何接口的连接。

## 4.2.1 与套接字相关的数据结构

- `sa_family`: 这存储了我们之前讨论过的与套接字关联的协议族号。
- `s_data[]`: 此数组包含非常特定于协议的数据。在 `PF_INET` 协议族的情况下，此数组包含 [端口号，IP 地址 (`struct in_addr`)]；
- `sin_family`: 这是一个地址族（IP 协议为 `PF_INET`）。
- `s_port`: 这是一个 16 位数字，用于区分同一协议族的不同套接字。
- `s_addr`: 这是一个表示 IP 地址的 32 位数字。在服务器应用程序中，这通常设置为 `INADDR_ANY`，这意味着如果服务器有多个接口（物理/虚拟），它可以接受来自其中任何一个接口的连接。

### 4.2.2 哈希桶 (Hash Buckets)

| 结构 | 描述 |
| :--- | :--- |
| `tcp_ehash` | 所有具有完整身份（已建立）的套接字列表 |
| `tcp_bhash` | 包含所有端口号信息的实体哈希（已绑定） |
| `tcp_listening_hash` | 所有处于 TCP_LISTEN 状态的套接字 |

### 4.2.3 Listen_hash

| 结构 | 描述 |
| :--- | :--- |
| `tcp_listening_hash` | 已建立状态套接字的哈希表 |

### 4.2.4 Bhash

| 结构 | 描述 |
| :--- | :--- |
| `tcp_bhash` | TIME_WAIT 状态套接字的哈希表 |

### 4.2.5 Listen_hash

| 结构 | 描述 |
| :--- | :--- |
| `tcp_bhash` | 基于绑定的套接字哈希表 |

## 内核实现的 TCP 连接建立

长度为 'n' 的 `tcp_ehash` 哈希表分为两部分。前半部分（n/2）哈希所有不在 TIME_WAIT 状态的套接字。后半部分（n/2）哈希所有处于 TIME_WAIT 状态的套接字。

图 4.4.-状态为 >=_ESTABLISHED 和 <_CLOSE 的套接字的哈希链。

### 4.2.6 tcp_hashinfo

该结构管理 TCP 绑定哈希桶。`tcp_hashinfo` 的成员如下：

```c
struct tcp_ehash_bucket *_tcp_ehash; // 所有具有完整身份的套接字列表。具有完整身份意味着套接字状态 1. >= TCP_ESTABLISHED 2. <_CLOSE
struct tcp_bind_hashbucket *_tcp_bhash; // 包含所有已绑定端口信息的实体哈希桶
int _tcp_ehash_size; // tcp_ehash 表的大小。
int _tcp_bhash_size; // tcp_bhash 表的大小。
struct sock *_tcp_listening_hash[TCP_LHTABLE_SIZE]; // 所有处于 TCP_LISTEN 状态的套接字的哈希表。套接字根据本地端口号在表中进行哈希。
```

## TCP 连接建立的内核实现

### tcp_bhash

`tcp_bhash[0]` 受自旋锁 '`lock`' 保护的冲突哈希链

![](img/b3f231108facab5be0138b2cfd3f681a_153_0.png)

`tcp_bhash[n]` 受自旋锁 '`lock`' 保护的冲突哈希链

![](img/b3f231108facab5be0138b2cfd3f681a_153_1.png)

| 字段 | 类型 | 描述 |
| :--- | :--- | :--- |
| `tb->next` | `struct tcp_bind_bucket *tb` |  |
| `tb->pprev` | `struct tcp_bind_bucket *tb` |  |
| `sk->bind_next` | `struct socket *sk` |  |
| `sk->bind_pprev` | `struct socket *sk` |  |

哈希表中的每个元素 (`struct tcp_bind_bucket`) 都设置了 `fastreuse` (`tb->fastreuse`) 标志，当 `owners(tb->owners)` 列表中的所有 socket 都设置了 `reuse(sk->reuse)` 标志且它们不是监听套字 (`sk->state != TCP_LISTEN`) 时。

**图 4.6.** 系统级哈希表，链接了所有绑定到其中一个端口的 socket。

`rwlock_t __tcp_lhash_lock`: 此锁保护 `__tcp_lhash_users` 以及 `__tcp_each` 表。

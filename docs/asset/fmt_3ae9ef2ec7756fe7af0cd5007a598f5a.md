
`atomic_t` `__tcp_lhash_users`：该变量用于同步 `__tcp_listening_hash` 的读/写者。每当进程想要获取 `tcp_listen_hash` 列表的读/写锁时，该成员就会加 1。当我们释放锁时，它会减 1；如果值降为 0，我们将唤醒所有等待获取锁的进程。

`wait_queue_head_t` `__tcp_lhash_wait`：这是 `tcp_listening_hash` 读/写者的等待队列。

`pinlock_t` `__tcp_portalloc_lock`：此锁用于同步对全局变量 `tcp_port_rover` 和 `tcp_bhash` 哈希表的访问。当我们请求本地端口来绑定 socket 时，应该持有此锁。

## 4.2.7 tcp_bind_hashbucket (见图 4.6)

这描述了哈希桶并由两个成员组成：

- `spinlock_t` `lock`：用于保护冲突哈希链的锁。
- `tcp_bind_bucket` * `chain`：绑定哈希桶的冲突哈希链的元素。

### 4.2.8 tcp_bind_bucket

此结构保留了关于端口号的使用信息以及端口号的使用方式。这些信息足以足够告知新的绑定 socket 是否可以绑定到已使用的特定端口号上。该数据结构还跟踪了所有与端口号相关的 socket。

`unsigned short` `port`：这是与 `tcp_bind_bucket` 关联的端口号。每当 socket 想要绑定到某个未使用的端口时，我们都会分配一个新的 `tcp_bind_bucket` 结构，分配涉及的端口号，并在 `tcp_bind_hashbucket` 中对其进行哈希处理。

`signed short` `fastreuse`：此标志表示已占用的端口号是否可以被新 socket 复用。每当有新 socket 请求为其分配端口号时，我们会检查该端口号是否被其他 socket 占用。因此，我们会检查 `tcp_bind_hashbucket` 中与该端口号关联的条目。现在，如果我们请求绑定具有该哈希条目的端口号的 socket，我们会检查 `fastreuse` 标志。如果该标志被设置，我们确定可以将 socket 绑定到关联的端口并将其添加到 `owners` 列表中。

简而言之，如果 `fastreuse` 标志被设置，我们就拥有了 `owners` 列表中的所有 socket，如下：

- 1. 这些 socket 绑定到同一个 TCP 端口，但在不同的网络接口上。我们可以让服务器应用程序监听在同一个端口，但在不同接口上配置了不同的 IP 地址。
- 2. 或者所有 socket 都绑定到同一个复用集且不是监听套字，意味着对于 `owners` 列表中的所有 socket 都满足以下条件：

```
sk->reuse && sk->state != TCP_LISTEN
```

- 3. 或者所有 socket 都使用相同的接口绑定到同一个端口，但所有 socket 的 `recv_saddr` 都不同。

`sys_bind(int fd,struct sockaddr *umyaddr, int addrlen)`

图 4.7. 内核中 bind 系统调用的入口点。

`struct tcp_bind_bucket` * `next`：这是 `tcp-hash-bucket` 链中的下一个节点，其关联的端口号哈希到相同的值。

`struct sock` * `owners`：这是使用相同端口号的 socket 列表。它们通过 `sock` 结构中的以下成员链接：

- 1. `sk->bind_next`
- 2. `sk->bind_pprev`
- 3. `sk->prev`

`struct tcp_bind_bucket` ** `next_pprev`：这是 `tcp_bind_bucket` 的前驱，它包含了绑定哈希桶地址。

### 4.2.9 bind()

内核中，`bind()` 系统调用的入口点接受以下参数：

- socket 的文件描述符 (`fd`)
- socket 的地址 (`struct sockaddr`)

由于 `socket()` 已经将文件描述符与 socket 关联，当调用 `bind` 系统调用时，会调用 `sys_bind`。

### 4.2.10 sys_bind()

`sys_bind()` 是一个函数，接收三个参数：

- `fd`：文件描述符
- `umaddr`：涉及的地址 (`struct sockaddr`)
- `addrlen`：地址长度

首先，通过 `socket()` 返回的文件描述符获取绑定 socket 的地址。

### 4.2.11 get()

`get()` 描述了 socket 的地址。

### 4.2.12 fget()

`fget()` 描述了 socket 的文件描述符。

## 绑定 (BIND)

`sk->rcv_saddr`

`sk->saddr`

`sk->rcv_saddr`。这是一个用于哈希查找的源地址，而 `sk->saddr` 用于传输（IP 头部部的源地址）。这些初始化为套接地址中指定的 IP 地址 (`addr->sin_addr.addr`)。当套接字的 IP 地址为组播或广播时，我们将 `sk->saddr` 设置为 0（这意味着在这种情况下使用发送设备）。

下一步是确定我们是否被允许绑定到指定的端口（该端口已被另一个套接字占用）。调用特定协议的 `sk->prot->get_port()`。这是来自 `tcp_prot` 的 `tcp_v4_get_port()`（特定于 `SOCK_STREAM` 的协议操作set）。

- 1. > `TCP_ESTABLISHED`
- 2. < `TCP_CLOSE`

## 4.2.14 tcp_v4_get_port()

`cp_port_rover`

`tcp_bhash`

`cp_port_rover`：这是另一个记录分配给套接字的最后一个端口号的变量。

`cp_bhash`：这是一个全局哈希桶，包含所有分配的端口号及相关信息。这是一个宏，用于访问全局变量 `tcp_hashinfo`（类型为 `struct tcp_hashinfo`）的成员 `tcp_hashinfo->tcp_bhash`。

从 `tcp_port_rover` 开始，我们检查 `sysctl_local_port_range[1]` 中存储的最大本地端口范围内的所有空闲端口。

`rover = tcp_port_rover;`

我们从 `tcp_bhash` 哈希表访问每个端口号对应的哈希链头（参见 cs 4.1）。

在访问冲突哈希链之前，我们需要持有链锁 (`head->lock`)。

`spin_lock(&head->lock);`

# 134 # TCP 连接建立的内核实现

```c
net/ipv4/tcp_ipv4.c
220      head = &tcp_bhash[tcp_bhash(rover)];
```

cs 4.1. `tcp_v4_get_port()`。

现在我们使用链元素的 `next` 成员（`struct tcp_bind_bucket`）遍历冲突哈希链的每个元素。对于每个元素，我们尝试将当前端口号与哈希链元素的端口号进行匹配。

```c
if (tb->port == rover)
```

如果我们发现当前哈希冲突链中没有任何元素 (`tb`) 对应选定的端口号 (`rover`)，我们就移动到下一个端口号 (`++rover`) 并重新开始。否则，我们退出循环并释放全局锁 `tcp_portalloc_lock`。我们到达这里是因为以下两种情况之一：

- 1. 我们已经耗尽了所有端口号（全部被占用）
- 2. 或者我们找到了未使用的端口号。

在一种情况下，我们返回错误；而在后一种情况下，我们需要在 `tcp_bhash` 哈希表中为新端口号分配创建一个条目。我们将分配的端口号存储在全局变量 `tcp_port_rover` 中，并将 `tb`（冲突链列表元素）初始化为 NULL，因为我们需要创建一个新的条目层。

如果应用程序指定了我们想要绑定的套接字端口号，我们从 `tcp_bhash[]` 哈希表中获取与该端口号对应的冲突哈希链元素。我们遍历冲突哈希链的每个元素，并匹配每个元素的端口号与目标端口号。如果我们能够找到匹配的条目，我们就知道该端口已被占用。尽管如此，我们并不会放弃，因为如果满足某些条件，我们可以重用这些端口。如果我们到达这里，说明：

- 1. 要么我们获得了一个可用的空闲端口号
- 2. 或者获得了未被占用的请求端口号
- 3. 或者获取了已占用的请求端口号。

对于情况 1 和 2，我们需要在 `tcp_bhash` 表中创建一个新的哈希条目。我们分配一个新的 `struct tcp_bind_hashbucket`，并初始化分配结构的所有字段。我们将当前哈希链元素链接到分配的结构以及 `tcp_bind_bucket` 结构中的 `head` 和 `pprev` 成员。现在，需要初始化元素的元素的 `fastreuse` 成员。我们之前已经详细讨论过这个标志，现在我们查看如何初始化。在以下情况下，我们设置此标志 (`tb->fastreuse`)：

- 1. 为当前套接字设置了重用标志 (`sk->reuse == 1`)
- 2. 且当前套接字不处于监听状态 (`sk->state != TCP_LISTEN`)

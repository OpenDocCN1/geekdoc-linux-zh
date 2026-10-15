
...（大于）第一个 SYN 数据包的序列号，仅向调用函数指示需要发送 RST。同样，对 TCP 头部标志进行检查。如果它们不是 ACK 而是 RST 或 SYN，我们就会做出适当的决策。最后，我们已经通过了所有测试，且 ACK 是正确的，因此我们需要处理连接请求。我们调用特定于返回协议的 `rvn_syn_socket()` 函数。如前所述，这是 `struct tcp_func` 的一部分，在 `v4_init_socket()` 到 `ipv4_specific` 时，在 `socket()` 时通过 `of_hash` 插入。此函数 `of_specific_syn_recv_socket()` 在情况下指向 `tcp_v4_syn_recv_socket()`。`tcp_v4_recv_socket()` 为连接请求创建一个新套字，因为三次握手在两个连接上已完成，我们已经识别了它们的身份。如果 accept 队列未满，则创建新套字。状态：通过调用 `tcp_acceptq_is_full()` 检查 accept 队列。在 accept 队列满的情况下，连接请求仍在 SYN 队列中，以便稍后再次收到此连接的最终 ACK，且如果 accept 未满，我们可以接受连接队列，因为套字队列未满，我们继续初始化新套字。大部分属性继承自套字，其余特定于 tcp 的字段来自 `kernel/ip` 头部。我们调用 `tcp_v4_hash()` 在 `tcp_ehash` 表上对新创建的套字进行哈希（见图 4.4）。我们返回到 `check_recv()`，在该处从 SYN 队列中取消链接并添加到接受队列。因此处于 SYN_RECV 状态。从新套字指针返回到 `tcp_v4_hand_recv()`。从 `tcp_v4_do_rcv()`，我们调用 `child_process()` 对新创建的套字进行更多处理。在情况下对套字没有用户（`child->lock_users == 0`）时，`child_process()` 调用 `tcp_rcv_state_process()`。在 `tcp_rcv_state_process()` 中，我们对 TCP 标志进行相同的检查，并通过调用 `tcp_fast_parse_options()` 从 TCP 头部选项中提取选项，初始化套字的 `tcp_opt_structure(sk->tpinfo_of_tcp)`。

最后将套字状态更改为 TCP_ESTABLISHED。我们通过调用 `tcp_data_queue()` 将 `sk_buff` 放入套字接收队列，以便进程可以接收到数据的通知。我们返回到 `tcp_child_process()`。我们在持有套字锁且下半部分的情况下完成了套字的整个处理，因为下半部分在处理过程中可能会改变进程的状态。内核处理连接请求的完整流程如图 4.19 所示。

## 4.4.3 处理新连接请求的流量控制

图 4.19a 和 4.19 显示了内核中 TCP 连接请求处理实现的流量控制。在这里我们展示了实现连接处理的主要程序，将在 4.4.1 和 4.4.2 节中讨论。

## 4.5 ACCEPT

正如我们从之前的课程中学到的，`listen()` 系统调用让 TCP 套字接受连接，但该套字尚未完全功能化。当 TCP 两个端完成三次握手后，监听套字会接受连接并将其放入 accept 队列。accept 队列中的套字处于已建立状态。现在服务器应用程序必须拾取

![](img/b3f231108facab5be0138b2cfd3f681a_182_0.png)

图 19a. 处理连接的代码流。

## TCP 连接建立的内核实现

进一步处理 SYN_RECV 套字，`sk->state = TCP_SYN_RCV`：

![](img/b3f231108facab5be0138b2cfd3f681a_183_0.png)

逐个处理 accept 队列中的已建立连接请求，并为每个套字提供唯一的身份，以便该套字可以作为一个独立通道与其对端开始通信。每个连接请求的 `sock` 结构与 BSD 套字关联，并映射在进程的文件表中。执行此操作的应用调用了 `accept()` 系统调用。服务器应用程序发出 `accept()` 以从 accept 队列中开始一个开放连接请求，图 4.1。`accept()` 系统调用向应用程序返回一个新套字描述符，服务器使用该描述符与对端或连接起始者进行通信。在这里我们讨论当应用程序调用 `accept()` 时内核内部发生了什么，内核内部使用以下参数调用 `sys.accept()`：

```
sys_accept(int fd, struct sockaddr *upeer, int *upeer_addrlen)
```

accept 的内核接口。

- `fd`: 监听套字的文件描述符。
- `upeer`: 连接远端的套字地址（`struct sockaddr *`），需要由内核填充并发送回应用程序。
- `upeer_addrlen`: 套字地址的长度。

`sys_accept()`。它通过调用 `fd_lookup()` 使用作为 `accept()` 参数传递的套字文件描述符 (`fd`) 来识别与父套字（监听套字）关联的ds 套字。工作原理如下：

它获取当前进程的 `files_structure` 结构，该结构维护了当前进程所有打开文件的计数；这是 `current->files.max_fds`，`files->max_fds` 表示在任何时刻分配给当前进程打开文件的作为文件描述符的最大数量。它对监听器文件描述符进行合理性检查，确保它没有超过 `->max_fds`。如果 `fd` 远低于 `->max_fds`，我们得到文件数组的第 id 个元素 `fd[id]`，这里是监听套字文件描述符的文件结构。通过文件表锁 `current->files->fd_lock` 访问文件表 `current`。与套字描述符关联的 BSD 套字可以从刚获取的文件结构中的 `dentry->inode` 获得。我们还需要确保 inode 与套字关联。这可以通过检查 inode 的 `i_sock` 来实现，`inode->i_sock`。如果 inode 被设置，则 inode 表示套字。现在套字是该 inode 的一部分，并可以从 `inode->i_sock` 获取。文件、inode 和套字之间的链接如图 4.2 所示。

因此，我们调用了 `sys_socket()` 并获得了与监听套字关联的结构。我们需要为新请求创建一个新套字，并以与处理监听套字相同的方式将套字关联（见图 4.20）。通过调用 `sock_alloc()` 为连接分配新的套字结构。该函数为连接分配一个新的套字结构。调用 `tcp_v4_hash()` 在 `tcp_ehash` 表上对新创建的套字进行哈希（见图 4.4）。我们返回到 `check_recv()`，在该处请求从 SYN 队列中取消链接并添加到接受队列。因此处于 SYN_RECV 状态。从新套字指针返回到 `tcp_v4_hand_recv()`。从 `tcp_v4_do_rcv()`，我们调用 `child_process()` 对新创建的套字进行更多处理。在情况下对套字没有用户（`child->lock_users == 0`）时，`child_process()` 调用 `tcp_rcv_state_process()`。在 `tcp_rcv_state_process()` 中，我们对 TCP 标志进行相同的检查，并通过调用 `tcp_fast_parse_options()` 从 TCP 头部选项中提取选项，初始化套字的 `tcp_opt_structure(sk->tpinfo_of_tcp)`。

最后将套字状态更改为 TCP_ESTABLISHED。我们通过调用 `tcp_data_queue()` 将 `sk_buff` 放入套字接收队列，以便进程可以被通知数据的接收。我们返回到 `tcp_child_process()`。我们在持有套字锁且下半部分的情况下完成了套字的整个处理，因为下半部分在处理过程中可能会改变进程的状态。内核处理连接请求的完整流程如图 4.19 所示。

## 4.4.3 处理新连接请求的流量控制

图 4.19a 和 4.19 显示了内核中 TCP 连接请求处理实现的流量控制。在这里我们展示了实现连接处理的主要程序，将在 4.4.1 和 4.4.2 节中讨论。

## 4.5 ACCEPT

正如我们从之前的课程中学到的，`listen()` 系统调用让 TCP 套字接受连接，但该套字尚未完全功能化。当 TCP 两个端完成三次握手后，监听套字会接受连接并将其放入 accept 队列。accept 队列中的套字处于已建立状态。现在服务器应用程序必须拾取

![](img/b3f231108facab5be0138b2cfd3f681a_182_0.png)

图 19a. 处理连接的代码流。

## TCP 连接建立的内核实现

进一步处理 SYN_RECV 套字，`sk->state = TCP_SYN_RCV`：

![](img/b3f231108facab5be0138b2cfd3f681a_183_0.png)

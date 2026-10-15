
此时，我们有三个连接，现在我们为 `cli[2]` 调用 `t_accept`。但现在第一个客户端 `cli[0]` 已经发送 RST 终止了连接。一旦 `t_accept` 调用失败并返回错误 `TLOOK$`，但这次 `t_look` 返回的是 `T_DISCONNECT`。我们现在必须调用 `t_recvdis` 来接收断开连接。记得该函数填充的 `t_disc` 结构中有一个条目是被中止连接的序列标识符（第 28.10 节）。我们必须使用它来搜索我们的 `cli` 结构数组，寻找 `t_call` 结构序列匹配的条目。然后我们将条目“向上”移动，用 `cli[1]` 覆盖 `cli[0]`，用 `cli[2]` 覆盖 `cli[1]`。我们还递减了 `ncli`，并得到了图 30.10 所示的数据结构。

| connfd | t_call() |  |

|---|---|---|

| `cli[0]` | count | 第二个连接 |

| tcallp | | |

| connfd | | |

| `cli[1]` | count | 第三个连接 |

| tcallp | | |

| connfd | | |

| | | `ncli = 2` |

图 30.10 第一个连接被中止后的数据结构。

## 30.8 xti_accept 函数（复习）

我们（再次）调用 `t_accept`，假设这次它成功了。然后我们从数组中移除 `cli[1]` 条目，将 `ncli` 递减为变为 1，并将第三个连接返回给 `xti_accept` 的调用者。记住，此示例中目前描述的所有内容（从第一次调用 `t_listen` 开始）都发生在我们的 `xti_accept` 函数中。现在是该函数第一次向调用者返回已连接的描述符。

下一次调用 `xti_accept` 时，`ncli` 将为 1，并为 `cli[0]` 调用 `t_accept`。假设它成功，则将第二个连接返回给调用者。

我们现在展示 `xti_accept` 函数的代码，其前半部分在 30.11 中。

### 图 30.11 xti_accept 函数：第一部分。

#### 声明静态变量

计数器 `ncli`、另一个中止连接的计数器 `ndisconn` 以及指向我们的 `cli` 结构数组的指针被声明为 `static`。

#### 第一次调用时的初始化

当我们第一次分配 `cli` 结构数组时，数组中的条目数量为常量 `LISTENING` 或同名环境变量的值。这与调用 `t_bind` 时使用的 `tcp_listen` 值相同。对于数组中的每个元素，我们随后调用 `t_alloc` 来分配一个 `t_call` 结构，并将返回的指针存储在 `cli` 结构中。

在线程环境中，这一个 `cli` 数组副本及其 `n` 计数器必须受到保护，以允许多个线程同时调用 `xti_accept`。

该函数的后半部分如图 30.12 所示。

### 等待连接

如果我们的数组为空，我们必须调用 `t_listen` 并等待连接。这次 `t_listen` 的调用是监听服务器花费大部分时间的地方。当 `t_listen` 返回时，客户端的协议地址和连接标识符已保存在 `t_listen` 中。我们调用 `t_open` 创建一个新的端点，连接将在此被接受，并将此端点绑定到任何本地地址。

### 调用 t_accept；成功时返回

我们调用 `t_accept` 来接受由 `cli[ncli-1]` 指定的连接，如果成功，我们把此连接描述符返回给调用者。如果调用者想要使用读写，我们调用 `xti_rdwr` 函数，并可选地返回客户端的协议地址。

### 处理待处理连接

如果 `t_accept` 返回 `TLOOK` 且 `t_look` 返回 `T_LISTEN`，则另一个连接正在挂起，我们必须调用 `t_listen` 来接收有关此新连接的信息。我们注意这次调用不会阻塞，因为端点有一个待处理的 `T_LISTEN` 事件。我们调用 `t_open` 和 `t_bind` 将信息保存到数组条目 `cli[ncli]` 中。

### 处理待处理连接的断开

如果 `t_accept` 返回 `TLOOK` 且 `t_look` 返回 `T_DISCONNECT`，则 `t_listen` 返回的连接之一已被客户端中止。我们调用 `t_rdovis` 获取有关中止连接的信息（即其序列），然后搜索匹配的条目。当我们找到该条目时，计算出被中止条目之后的条目数量 (`n`)，并调用 `memove` 剩余条目。我们调用 `memove` 而不是 `memmove`，因为前者可以处理重叠字段，而我们在这种场景中遇到了这种情况（见练习 30.3）。

我们使用这个新版本的 `xti_accept` 测试图 30.6，它按预期工作。我们还想看 `t_accept` 多频繁因为额外的待处理连接而返回。为了看到这一点，我们写了一个简单的函数打印 `cli` 结构计数、`ndisconn` 计数器（稍后描述），然后从服务器中调用该函数（图 30.6）。图 30.7 显示了在 Unix 2.1 和 Solaris 2.5 上的结果。我们将子进程数量从 1 改变到 4，确保总共有 600 个连接。

```
for ( ; ; ) {
    if (ncli == 0) { /* 等待连接 */
        t_listen(listenfd, cli[ncli].tcallp); /* 在此处阻塞 */
        ncli--confd = T_open(xti_serv_dev, O_RDWR, NULL);
        T_bind(cli[ncli].confd, NULL, NULL);
        cli[ncli].count++;
    }
    ncli++;
    if (t_accept(listenfd, cli[ncli] - 1).confd) == 0) {
        ncli--; /* 成功 */
        if (rdwr)
            xti_rdwr(cli[ncli].confd);
    else
        if (cliaddr) { /* 返回客户端地址 */
            n = min(cliaddr->max_len, cli[ncli].tcallp->addr.len);
            memcpy(cliaddr->buf, cli[ncli].tcallp->addr.buf, n);
            cliaddr->len = n;
        }
        return (cli[ncli].confd);
    } else if (event == T_DISCONNECT) {
    if (select(listenfd) == T_LISTEN) {
        T_listen(listenfd, cli[ncli].tcallp); /* 不会阻塞 */
        cli[ncli].confd = T_open(xti_serv_dev, O_RDWR, NULL);
        T_bind(cli[ncli].confd, NULL, NULL);
        cli[ncli].count++;
    }
    ncli--;
} else if (event == T_DISCONNECT) {
    T_recvdis(listenfd, &tdiscon);
    for (i = 0; i < n; i++) {
        if (cli[i].tcallp->sequence == tdiscon.sequence) {
            T_close(cli[i].confd);
            tdisconn++;
            ncli--;
            if (n - i > 0)
                memmove(&cli[i], &cli[i + 1], n * sizeof(struct cli));
            break;
        } else
    err_quit("unexpected t_look error %d", event);
} else
    xti_err("unexpected t_accept error");
```

图 30.12 xti_accept 函数：后半部分。

| 服务器计数器 | 1 | 2 | 3 | 4 |

|---|---|---|---|---|

| `cli[0].count` | 600 | 309 | 95 | 102 |

| `cli[1].count` | | 291 | 286 | 121 |

| `cli[2].count` | | | 219 | 208 |

| Total | | 600 | 600 | 600 |

**图 30.1** `t_accept` 返回 `T_LISTEN` 的计数器。

只有两个连接，每个建立 300 个连接，且连续同时建立，`t_accept` 有一半的时间返回 `T_LISTEN`。

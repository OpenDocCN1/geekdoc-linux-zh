
在识别出发生 LRU 竞争的子锁和特定池后，你可能需要增加 LRU 旋锁的数量（`db_block_lru_latches`）或重新配置分配给每个缓冲区池的旋锁数量。

在 Oracle8 中，如果你只有一个缓冲区池配置了多个数据库写入器（`db_writer_processes`），缓冲区缓存将通过 LRU 旋锁在数据库写入器之间划分；每个 LRU 旋锁管理一个 LRU 列表。每个 LRU 列表由数据库块组成。在这种情况下，确保每个 DBWR 进程接收到等量分布的缓冲区对于平衡 DBWR 进程之间的工作负载非常重要。这避免了 DBWR 接收到大型 LRU 列表进行处理而其他接收列表非常小的情况。如果你配置了多个缓冲区池和多个数据库写入器，每个池的 LRU 旋锁数量应该是数据库写入器数量的倍数。在多个缓冲区池的情况下，每个缓冲区池可能有不同的块使用率。`recycle` 缓冲区池中的块通常被频繁修改，而 `keep` 池中的块可能很少修改。这意味着 `recycle` 缓冲区池的写操作比 `keep` 缓冲区池多。因此，为了实现最佳负载均衡，每个 DBWR 进程每个池应接收相同数量的 LRU 列表。在使用多个缓冲区池时，每个缓冲区池维护一个连续的 LRU 旋锁范围。根据可用处理器数量、数据库写入器数量和缓冲区池配置优化配置 LRU 旋锁数量。这有助于负载在数据库写入器之间均匀分布，从而最大化数据库 I/O 吞吐量。

## 5.9.4 大池 (LARGE POOL)

Oracle8 提供了在多线程服务器 (MTS) 环境下配置一个单独内存池以用于大内存分配的能力。为 MTS 会话分配的内存会减少用于共享 SQL 缓存的共享池内存。这可能会导致额外的解析和加载，因为 SQL 语句可能会为了给 MTS 会话内存分配留空间而被从缓存中老化出。为 MTS 会话内存的 I/O 缓冲区配置单独池可以减少对共享池内存的竞争。大池还可以在备份期间使用。`init.ora` 参数 `large_pool_size` 和 `large_pool_min_alloc` 分别指定大池的大小以及从大池分配内存时的最小分配大小。

你还可以通过检查 `v$sgstat` 视图的 `POOL` 列来确定对象位于哪个池中。大池不作为缓存管理，对象不会从大内存中被老化出。

## 5.10 优化归档

（注：原文此部分存在大量重复的无效文本，已根据要求保留核心逻辑并停止重复）

## 5.12 调优 TCP/IP

你可以在后等待驱动程序（post-wait driver）和信号量之间进行选择。在 Sequent 上，后等待驱动程序相对于信号量的性能提升大约为 5%。在 Solaris 上，Oracle 使用信号量是因为它们具有出色的扩展性和高性能。

## 5.12 调优 TCP/IP

SQL*Net V2 和 Net8 使用的默认数据包大小为会话数据单元（SDU） 2 KB。在大多数平台上，TCP/IP 栈和底层网络层使用的数据包大小为 1 KB。SDU 应该等于或底层 TCP/IP 数据包大小的倍数。如果数据包大小小于 SDU，可能需要额外的网络开销，因为每个 SDU 数据包会被拆分成更小的数据包。某些平台允许你增大 OS 的 TCP/IP 数据包大小。将 OS 数据包大小增大到 2 KB 可以让 SQL*Net 数据包和 OS TCP/IP 数据包保持相同。

## 5.12.1 会话数据单元 (SDU)

Oracle 网络层将数据放在缓冲区中，并在缓冲区满或请求数据时发送缓冲区。会话数据单元（SDU）是用于跨网络发送数据的缓冲区。通过将 SDU 单元大小从默认的 2 KB 进行调整，可能可以通过减少网络往返次数来提高性能。只有在传输大量数据、使用对延迟至关重要的广域网（WAN）或数据包大小保持一致的情况下，才应该修改 SDU 大小。传输数据单元（TDU）是用于传输数据到底层协议适配器的块。TDU 和 SDU 可以设置为不同的大小；但在大多数情况下，这样做没有太大用处。

在调整 SDU 和 TDU 的大小之前，你应该通过查询 `v$sysstat` 视图来检查网络流量。

```sql
SQL> select name,
      value
from v$sysstat where name like '%Net@'
```

| NAME | VALUE |
|---|---|
| 通过 SQL*Net 发送到客户端的字节 | 208985960 |
| 通过 SQL*Net 从客户端接收的字节 | 310259198 |
| 往客户端的 SQL*Net 往返 | 4749102 |
| 通过 SQL*Net 发送到 dlink 的字节 | 12122 |
| 通过 SQL*Net 从 dlink 接收的字节 | 78615 |
| 往 dlink 的 SQL*Net 往返 | 81 |

此查询报告了 SQL*Net/Net8 流量的字节数以及往返次数。这些信息可以帮助根据网络流量更有效地查询 SDU 和 TDU 缓冲区。你还应该查询 `v$system_event` 视图来确定用户是否正在等待网络事件。

```sql
SQL> select event,
total_waits,
time_waited,
average_wait
from v$system_event
where event like '%Net8*'
```

| EVENT | TOTAL_TIME_WAITED | AVERAGE_WAIT |
|---|---|---|
| SQL*Net message to client | 4776784 | 1191 | .000249313 |
| SQL*Net message to dblink | 82 | 0 | 0 |
| SQL*Net more data to client | 650918 | 4621 | .007099205 |
| SQL*Net message from client | 4775666 | 105374930 | 22.0649702 |
| SQL*Net more data from client | 938 | 17327 | 18.427214 |
| SQL*Net more data from dblink | 81 | 184 | 2.27160494 |
| SQL*Net more data from dblink | 30 | 6 | .2 |
| SQL*Net break/reset to client | 5794 | 18150 | 3.12355091 |
| SQL*Net break/reset to dblink | 2 | 1 | .5 |

在确定网络流量以及以及用户正在经历事件等待后，你可以通过修改客户端和服务器上的 `tnsnames.ora` 和 `listener` 文件来调整 SDU 和 TDU 的大小。指示较大的 SDU/TDU 单元是否有益处的主要事件是 SQL*Net more data 事件。当由于数据无法放入数据包大小而需要多次往返来交付数据时，就会触发 SQL*Net more data 事件。如果等待信息显示在 SQL*Net more data 事件上花费了大量时间，那么增大 SDU/TDU 大可能会有助于性能提高到数据库块的若干倍。除了查看网络统计和事件外，你还应该彻底测试应用程序，以确定 SDU/TDU 的最佳设置。

TNSNAMES.ORA:

```
sales=(DESCRIPTION:
(SDU=8192) ***** session data unit buffer size
(TDU=8192) ***** transport data unit size
(ADDRESS=(PROTOCOL=tcp)
(PORT=1521)
(HOST=myhost))
(CONNECT_DATA=(SID=prods)))
```

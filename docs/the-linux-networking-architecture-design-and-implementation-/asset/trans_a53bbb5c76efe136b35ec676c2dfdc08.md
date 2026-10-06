

## 16.3 实现

rt_check_expire() 会根据配置变量 `ip_rt_gc_interval` 和 `ip_rt_gc_timeout`（默认在处理完数组的五分之一后）在执行若干步后中断工作，最晚在 jiffies 计数器值变化时中断。下次调用将从数组中的相同位置继续处理。

```
rt_garbage_collect() net/ipv4/route.c
```

rt_garbage_collect() 删除缓存条目的的方法与 rt_check_expire() 类似，但有以下不同点：

- rt_garbage_collect() 不再检查固定数量的数组元素来查找旧条目，而是针对要删除的条目数量设置一个特定目标。一旦达到该目标就会停止（时间同样被限制在两次 jiffies 变化之间的间隔内）。

- rt_may_expire() 的第二个阈值也是特定动态的；在每次遍历该条目后，它都会减半，直到达到目标。

- 要删除的条目数量是在 rt_garbage_collect() 开始时根据上一次调用的数量计算的。该计算试图找到一个平衡状态，即删除的条目数量与创建的数量大致相等。

rt_garbage_collect() 是一个非常消耗资源的函数，因此在配置变量 `ip_rt_gc_min_interval` 中定义了两次调用之间的最小间隔，除非空间极度缺乏。在这种情况下，该函数将立即返回。

RT Netlink 接口 路由缓存条目可以通过 RT netlink 接口读取。相应的消息由 `ip_rt_dump()` 创建，该函数在请求缓存条目时由 `inet_dump_fib()`（见上文）调用。

此外，你还可以通过 RT netlink 接口使用 `ip route` 命令来模拟形成过程。具体而言，此过程会调用 `ip_input()` 或 `ip_route_output()` 并返回结果，其副作用是在路由缓存中创建一个条目。相应的 RT netlink 消息由 net/ipv4/route.c. 中的 `inet_rtm_getroute()` 处理，该函数注册在 net/ipv4/devinet.c. 的 `inet_rtlink_table[]` 表中。

Proc 文件系统 某些配置变量（包括控制缓存垃圾回收行为的变量）映射到 `/proc/sys/net/ipv4/route` 目录下的文件。对于缺失的 `ip_rt_prefix`，文件名与变量对应。唯一的例外是 `flush` 文件，访问它时会删除路由缓存。

这些文件由 net/ipv4/route.c 中的控制结构 `ctl_table ipv4_route_table[]` 定义，处理 `flush` 文件访问的函数 `ipv4_sysctl_rtcache_flush()` 也注册在该处。net/sysctl_net_ipv4.c 中的 `ctl_table` 结构 `ipv4_table[]` 包含了对 `ipv4_route_table[]` 的引用。该结构嵌入在通过 net/sysctl.c 中的 `net_table[]` 跨越的核心 `sysctl()` 树以及 kernel/net/sysctl.c 中的 `root_table[]` 中。

文件 `/proc/net/rt_cache` 允许你读取整个路由缓存的内容。内容由 net/ipv4/route.c 中的函数 `rt_cache_get_info()` 格式化，该函数在 `ip_route_init()` 初始化路由时通过 `proc_net_create()` 注册。

## 16.4 转发过程

第 14.2.1 节讨论了如何将转发查询嵌入入数据包的处理中：`ip_rc_finish()` 调 `ip_route_input()` 来查找一个 `dst_entry` 结构以确定数据包的后续路由。第 14.2.2 节讨论了出站数据包：它们的路由决策在 `ip_route_output()` 中做出，该函数由例如 `ip_queue_xmit()` 调用。

## ip_route_input()

net/ipv4/route.c

对于每个到达网络接口的数据包，都会调用函数 `ip_route_input()`。参数包括一个指向 socket-buffer 结构的指针、目的地址和源地址、TOS 值，以及指向接收网络接口的 `net_device` 结构指针。

首先，对地址和 TOS 值调用 `rt_hash_code()` 以计算在路由缓存哈希表中的索引。如果必要，将遍历链中最小的锚定元素，以找到与地址、输入接口、TOS 值和转发标志（如果存在）匹配的缓存条目。如果搜索成功，则将该条目的指针作为 `dst` 放入 `sk_buff` 结构中，任务完成。

如果没有找到匹配的缓存条目，则由以下两个函数之一负责进一步处理：

如果目的地址是组播地址，则调用 `ip_route_input_mc()`。另一个前提条件是输入接口要么属于一个组播组，要么配置了组播路由。如果不是如此，则数据包可能会被丢弃。`ip_route_input_mc()` 函数将在本章后关于 IP 组播的章节（第 17.4 节）中讨论。这里的做法与下文描述的本地目的地址处理相似，不同之处数据包始终被交付到本地机器，而不是引起 FIB 查询。

`ip_route_input_slow()` 用于处理“普通”目的地址，接下来将描述。

这两个函数接受的参数与 `ip_route_input()` 相同。

后四个参数也可以从前几个参数推导出来。然而，由于它们是单独传递的，`ip_route_input()` 不需要了解它们在 socket-buffer 结构中的表示形式……尽管套接字缓冲区结构仍被完全视为一个封装“黑盒”，但至少只访问了少数专门用于路由的数据元素。

## 16.3 实现

```
ip_route_input_slow()
```

首先，用传递的参数填充 `rt_key` 结构。然而，在使用它运行 FIB 查询之前，会检查无效值——组播源地址，以及移动带有空前缀的网络前缀。此类数据包会被丢弃，如果配置了 `CONFIG_IP_ROUTE_VERBOSE` 详细消息，它们将记录在系统日志中。在有限广播的意义上，显式允许例外使用 `0.0.0.0` 作为源和目的地址，因为这有时用于自动网络配置。

接下来，通过 `fib_lookup()` 开始 FIB 查询。如果没有找到匹配的条目，`ip_route_input_slow()` 也会停止处理并返回错误代码，这随后会导致 `ip_rcv_finish()`（由 `ip_route_input_slow()` 调用）丢弃数据包。

如果第 16.1.6 节提到的路由 NAT 处于激活状态，下一步将根据所用路由信息处理源地址（如果是 NAT，则处理目的地址）。然而，新地址仅添加到 `rt_key` 结构中；旧地址在调用参数中保留以供其他操作使用。目的地址发生转换后，必须再次调用 `fib_lookup()` 来查找常规路由条目（不允许进行其他转换）。

除外，FIB 查询的结果还会显示目的地址是否为本地地址，这意味着数据包针对本地系统。这种情况在后续处理中会被单独处理。

本地目的：一旦通过调用 `fib_validate_source()` 了源地址，就会创建一个新的缓存条目。函数指针 `output()` 将获得 `ip_rt_bug()` 值，因为数据包不允许离开系统。接下来，`input()` 指针设置为 `ip_local_deliver()`，以便将包交付到本地机器。由于没有路由器，缓存条目的 `rt_gateway` 地址设置为目的地址。

广播地址（例如上述作为源和目的的 `0.0.0.0` 以及通常的有限广播 `255.255.255.255`）在起始地址验证处被检测到并作为本地目的地址处理。然而，对于 `0.0.0.0` 地址不会调用 `fib_validate_source()`。

非本地目的地址：只有在输入接口的转发功能开启时，才需要处理非本地目的地址，因此首先检查此项。

如果找到的路由条目描述了多个输出路由，则调用 `fib_select_multipath()` 选择其中之一。随后，通过函数 `fib_validate_source()` 检查源地址，该函数在这种情况下也可以考虑找到输出网络接口。

```
ip_forward()` 和 `ip_output()` 被设置在新缓存条目的 `input()` 和 `output()` 函数指针中。函数 `rt_set_nexthop()` 执行
```


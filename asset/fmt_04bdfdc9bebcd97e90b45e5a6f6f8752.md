
```
# ls -1 -la /sys/bus/ccw/group/drivers/qeth/0.0.c200/
drwxr-xr-x 6 root 0 Sep 28 07:59 .
drwxr-xr-x 6 root 0 Sep 28 08:01 ..
-rw-r--r-- 1 root 4096 root Sep 28 07:59 add_hlen
drwxr-xr-x 2 root 0 Sep 28 07:59 blkt
-rw-r--r-- 1 root 4096 root Sep 28 07:59 broadcast_mode
-rw-r--r-- 1 root 4096 root Sep 28 07:59 buffer_count
l lwx-xr-x 1 root 0 Sep 28 07:59 bus -> ../../bus/ccwgroup
l-rw-xr-x 1 root 4096 root Sep 28 07:59 canonical_macaddr
-rw-r--r-- 1 root 4096 root Sep 28 07:59 card_type
l lwx-xr-x 1 root 0 Sep 28 07:59 cdev0 -> /.../../devices/sys/ccw0/0.0.0009/0.0.c200
l lwx-xr-x 1 root 0 Sep 28 07:59 cdev1 -> /.../../devices/ccw0/0.0.000a/0.0.c201
l lwx-xr-x 1 root 0 Sep 28 07:59 cdev2 -> /.../../devices/ccw0/0.0.000b/0.0.c202
-rw-r--r-- 1 root 4096 root Sep 28 07:59 checkingsum
-rw-r--r-- 1 root 4096 root Sep 28 07:59 chipid
lrw-rwx 1 root 0 Sep 28 07:59 driver -> ../../../bus/cgroup/drivers/qeth
--rw-r---- 1 root 4096 Sep 28 07:59 fake_broadcast
--rw-r---- 1 root 4096 Sep 28 07:59 fake_ll
--rw-r---- 1 root 4096 Sep 28 07:59 if_name
drwxr-xr-x 2 root 0 Sep 28 07:59 ipa_takeover
--rw-r---- 1 root 4096 Sep 28 07:59 large_size
--rw-r---- 1 root 4096 Sep 28 07:59 layer2
lrw-r-wx 1 root 0 Sep 28 07:59 net:eth0 -> ../../../class/eth0
--rw-r---- 1 root 4096 Sep 28 07:59 online
--rw-r---- 1 root 4096 Sep 28 07:59 performance_stats
--rw-r---- 1 root 4096 Sep 28 07:59 portname
--rw-r---- 1 root 4096 Sep 28 07:59 perino
--rw-r---- 1 root 4096 Sep 28 07:59 priority_queueing
-w-xr-xr-x 1 root 4096 Sep 28 07:59 recover
--rw-r---- 1 root 4096 Sep 28 07:59 route4
--rw-r---- 1 root 4096 Sep 28 07:59 route6
drwxr-xr-x 2 root 0 Sep 28 07:59 rxip
--rw-r---- 1 root 4096 Sep 28 07:59 state
-w-xr-xr-x 1 root 4096 Sep 28 07:59 uevent
-w-xr-xr-x 1 root 4096 Sep 28 07:59 ungroup
drwxr-xr-x 2 root 0 Sep 28 07:59 vipa
```

表 11-2 显示了 `sysfs` 系统上的所有可用参数。这些参数可以通过 `sysfs` 文件进行动态更新。参数分为三类：

-   显示（Display）：获取有关 OSA 配置的信息
-   配置（Configuration）：配置 OSA 上的其他功能
-   性能（Performance）：调优 OSA 适配器

| 文件 | 类别 | 描述 |
| :--- | :--- | :--- |
| `add_hlen` | Performance | 在每个数据包前面预留额外的头部空间。 |
| `broadcast_mode` | Configuration | 用于令牌环广播。 |
| `buffer_count` | Performance | 你可以为入站流量分配 8 到 128 个缓冲区。 |
| `canonical_macaddr` | Configuration | 用于令牌环网络。 |
| `card_type` | Configuration | |
| `checksumming` | Performance | 卸载校验和。 |
| `chipid` | Configuration | 显示通道 ID。 |
| `fake_broadcast` | Configuration | 伪广播。 |
| `fake_ll` | Configuration | |
| `if_name` | Configuration | |
| `ipa_takeover` | Configuration | |
| `large_size` | Configuration | |
| `layer2` | Configuration | |
| `online` | Configuration | |
| `performance_stats` | Performance | |
| `portname` | Configuration | |
| `perino` | Configuration | |
| `priority_queueing` | Configuration | |
| `recover` | Configuration | |
| `route4` | Configuration | |
| `route6` | Configuration | |
| `rxip` | Configuration | |
| `state` | Configuration | 显示状态。 |
| `uevent` | Configuration | |
| `ungroup` | Configuration | |
| `vippa` | Configuration | |

图 11-9 显示了我们在场景中执行的操作。我们测试了软件和硬件校验和。如你所见，当由 OSA 适配器执行校验和时，CPU 的使用率较低。在案例中，我们使用了 OSA Express 1000BASE-T。如果你使用 OSA Express 2 卡，差异会更加显著。

![](img/a8398552a9cf58d3f3798c1dedb947c2_196_0.png)

图 11-9 硬件软件校验和

## OSA 参数：`large_send`

与校验和类似，你可以将 TCP 分段从 Linux 网络栈卸载到 OSA-Express 2。对于具有大量出站包的接口，大发送（large send）可以提高性能。可以使用 `echo` 命令使用不同的值修改 `large_send` 参数：

-   No：不提供大发送。由 Linux TCP/IP 栈执行分段。
-   TSO：网络适配器执行分段。
-   EDDP：`qeth` 驱动程序执行分段。

## OSA 参数：`priority_queuing`

ODIO 模式下的 OSA-Express CHPID 在主存储中有四个输出队列。该参数赋予这些队列不同的优先级。队列化对于高流量情况非常重要。你可以通过 `cat` 命令检查 `priority_queuing`。示例 11-8 显示了在 `0.0.c200` 设备中设置的优先级队列。

示例 11-8 显示与 `0.0.c200` 设备相关的优先级队列

```
# cat /sys/bus/ccgroup/drivers/qeth/0.0.c200/priority_queuing
always queue 2
```

可以使用此值修改该参数：

-   `prio_queuing_prec`：根据每个数据包 IP 头部优先例字段的两个最高有效位来确定队列分配。
-   `prio_queuing_tos`：根据某些应用程序为数据包分配的 IP 服务类型（ToS）选择队列（自动管理队列）。
-   `no_prio_queuing`：默认值。所有数据包均使用队列 2。
-   `no_prio_queuing:0`：所有数据包均使用队列 0。
-   `no_prio_queuing:1`：所有数据包均使用队列 1。

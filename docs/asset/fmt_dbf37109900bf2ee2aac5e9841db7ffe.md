
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

- 显示（Display）：获取有关 `OSA` 配置的信息
- 配置（Configuration）：配置 `OSA` 上的其他功能
- 性能（Performance）：调优 `OSA` 适配器

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
| `vipa` | Configuration | |

*(注：由于原文提供的表格文本中部分行描述缺失，翻译严格遵循了提供的文本结构)*

通过 I/O 子通道接口显示状态。

通过新的 `sysfs` 文件系统，所有关于驱动的信息都收集在 `/sys/bus/ccw/group/drivers/qeth`。

你可以通过此 `sysfs` 方法交互来修改、添加或查询参数。示例 11-1 显示了与我们环境中使用的 `0.0.c200` 相关的文件系统结构。

示例 11-1 显示与驱动相关的 `sysfs` 文件的命令

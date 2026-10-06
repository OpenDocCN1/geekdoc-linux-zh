
当网桥初始化时，网桥定时器也会初始化。该定时器是一个 `timer_list` 类型（参见第 2.7.1 节）：它每秒调用一次 `br_tick()` 函数。该函数用于控制网桥实例的所有定时器函数和生成树协议。这意味着每个网桥实例仅使用一个系统定时器。所有内部定时进程都通过此定时器运行。更多信息请见后文子节“定时器处理”。

### 处理 BPDU
一旦接收到 BPDU，`br bridge_frame()` 函数中的 `br_handle_pdu()` 就会被调用。当拓扑变更包（TCN）到达时，由 `br_received_tcn_bpdu()` 负责后续的所有处理。当配置包（Config BPDU）到达时，数据包内容被复制到 `br_config_bpdu` 结构中，并将某些字段转换为内部表示。例如，时间值存储在 jiffies 而非 ticks 中。随后，BPDU 将由 `br_received_config_bpdu()` 函数处理。

### 生成树算法的步骤
生成树算法的具体步骤已在第 12.2.4 节中描述。如该节所述，生成树机制会在当前配置接收到任何信息的每条配置消息运行时运行。

新配置消息是否包含比当前存储更好的信息，是由策略实施的决策，例如根端口的选择和指定端口的命名。请注意，这些操作通常涉及较少的比较。

```
br_received_config_bpdu() net/bridge/br_stp.c
```

该函数最初调用 `br_is_root_bridge()` 来检查自身是否为根网桥。注意，如前所述，网桥并没有局域网互联的全局视图。可能有其他网桥将自己分类为根网桥。这种情况随着生成树算法步骤的运行逐渐改变，最终一个网桥将成为唯一的根网桥。

当新配置优于当前信息（调用 `br_supersedes_port_info()` 的结果）时，会发生以下情况：

- 首先，调用 `br_record_config_information()` 会导致配置 BPDU 的数据写入 `net_bridge_port` 结构中。
- 接着，调用 `br_configuration_update()` 函数。它选择根端口和指定端口。此操作可能会导致网桥及其端口的信息结构发生变化。
- 随后，`br_port_state_selection()` 识别端口状态。如果网桥在存储新信息之前是根网桥，但现在不再是，则停止 hello 定时器。如果还发现了拓扑结构的变化，则停止 `topology_change_timer`，启动 `tcn_timer` 并发送拓扑变更消息（`br_transmit_tcn()`）。

## 12.4 实现

如果输入端口被标记为根端口，则配置 BPDU 的超时值被添加到 `net_bridge` 结构中，并生成配置 BPDU（通过 `br_config_bpdu_generation()`）。此外，如果配置 BPDU 中设置了 `topology_change_ack` 标志，则调用函数 `br_topology_change_acknowledged()`。

相比之下，如果响应配置 BPDU 时没有发生变化，只要输入端口为指定端口，则调用 `br_reply()`。这意味着将发送一条带有本地存储值的配置消息。

```
br_supersedes_port_info net/bridge/br_stp.c
```

此函数检查所存储的 `net_bridge_port` 结构是否响应接收到的配置 BPDU 发生变化（即新的配置 BPDU 是否包含“更好”的信息）。这发生在以下两种情况：

- 根网桥的 ID 比结构中当前存储的根网桥 ID 小。
- 两个 ID 相等，但 BPDU 中的路径代价（path cost）更小。
- 路径代价相等，但发送网桥的 ID 比自身的 ID 小。
- 网桥 ID 匹配，但发送网桥的端口 ID 比输入端口 ID 小。

上述列表中的两点通常是决定性的，但如果两个本地网络通过并行网桥连接，则端口 ID 也可能起作用。

```
br_record_config_information() net/bridge/br_stp.c
```

如果配置消息优于当前存储的信息，则调用此函数。根网桥 ID 和通过根网桥的路径代价（RPC）分别作为指定根和代价存储在 `net_bridge_port` 结构中。发送配置消息的网桥及其输出端口作为指定网桥和端口。

消息年龄定时器（message-age timer）从配置消息的值开始，以便检测组件潜在的故障。

```
br_record_config_timeout_values() net/bridge/br_stp.c
```

调用此函数会清除从配置消息中复制的定时器过期值。

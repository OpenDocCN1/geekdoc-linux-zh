
系统中的 IPoIB 接口通常被称为 `ib0`、`ib1` 等（每个 InfiniBand 端口一个接口）。最好通过在服务器和计算节点的配置文件中写入地址来静态分配地址。在 IPoIB 上使用 DHCP 协议是可能的，但出于可靠性考虑，不建议使用它。

链路层地址（以太网网络中称为 MAC 地址或硬件地址）对于 IPoIB 长度为 20 字节。这就是为什么某些工具（特别是广泛使用的 `ifconfig` 工具，其以太网 MAC 地址长度固定为 6 字节）无法正常工作，并显示 IPoIB 的链路层地址。建议替换 `ifconfig` 的 `ip` 工具没有这个缺点。

链路层地址包含端口的 GUID、队列对编号（`QPN`，类比 InfiniBand 的 TCP 端口号）以及指示可以使用 InfiniBand 传输层协议进行 IP 传输的标志。

## 查看和管理 InfiniBand 网络的工具

本节提供了 OFED 工具包中一些工具的输出示例，并对输出信息进行了解释。这些信息将帮助你理解 InfiniBand 网络中发生了什么，并诊断其运行中的某些错误。

`ibstat` 命令显示安装在运行主机上的 InfiniBand 适配器上所有端口的状态。

```
CA 'mlx5_0'
CA type: MT4113
Number of ports: 2
Firmware version: 1.5.4.0
```

（注：由于原文中 `ibstat` 块内容不完整，此处仅根据用户提供的文本进行呈现。）


- 7. 现在你将看到准备好创建网络的窗口。从那里，点击“完成”在 KVM 主机上创建新的网络适配器。

在 `localhost` 连接详细信息窗口中，你将看到两个网络适配器。其中一个允许你通过 NAT 连接到外部网络，另一个仅为你提供私有网络。在虚拟主机上，此网络适配器被称为虚拟桥接适配器。

## 理解 KVM 网络

如果你使用 `ip link show` 命令，就可以看到此适配器（参见列表 9.2）。因为默认 KVM 安装已经创建了一个虚拟桥接，因此此虚拟桥接适配器将被称为 `virbr1`。

### 列表 9.2：虚拟网络适配器显示为 virbr1

```
[root]# ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 16436 qdisc noqueue state UNKNOWN
   link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: p61: <BROCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN
   qlen 1000
   link/ether b8:ac:6f:9c:35:28 brd ff:ff:ff:ff:ff:ff
3: wlan0: <NOCARRIER,BROCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN
   qlen 1000
   link/ether a0:88:b4:20:ce:24 brd ff:ff:ff:ff:ff:ff
4: virbr0: <BROCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc queue state UNKNOWN
   link/ether 52:54:00:71:43 brd ff:ff:ff:ff:ff:ff
5: virbr0-nic: <BROCAST,MULTICAST,UP> mtu 1500 qdisc noop state DOWN qlen 500
   link/ether 52:54:00:71:43 brd ff:ff:ff:ff:ff:ff
10: vnet0: <BROCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN qlen 500
    link/ether 54:00:15:a6:b4:b8 brd ff:ff:ff:ff:ff:ff
11: virbr1: <BROCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UNKNOWN
    link/ether 52:54:00:71:43 brd ff:ff:ff:ff:ff:ff
12: virbr1-nic: <BROCAST,MULTICAST,UP> mtu 1500 qdisc noop state DOWN qlen 500
    link/ether 52:54:00:71:43 brd ff
```

在这项强制性练习中，你将学习如何为你的 KVM 环境切换网络配置。首先，你将在主机上设置一个隔离的虚拟网络，然后你将把虚拟机中的网卡连接到这个隔离网络。如果一切顺利，在本次练习结束时，你将能够从你的虚拟机 ping 通主机计算机。

- 以 `root` 身份登录 KVM 主机。启动“虚拟机管理器”，选择“编辑” > “连接详细信息”。从那里开始，点击“虚拟网络”选项卡以显示配置正确的虚拟网络。你应该使用默认网络。

![](img/3a7e027360b64bc83d5cf9a2db902251_293_0.png)

- 点击“虚拟网络”选项卡左下角的 `+` 号。这将启动“创建虚拟网络”向导。从该向导的第一个界面，点击“下一步”。

- 为虚拟网络输入一个有意义的名称（例如 `privatenet`），并点击“下一步”继续。

## 练习 9.7（续）

![](img/3a7e027360b64bc83d5cf9a2db902251_294_0.png)

- 4. 现在，你需要选择一个将在此私有网络使用的网络。默认情况下，会自动从私有地址范围选择一个 IP 网络地址。如果此地址范围与你站点已使用的地址不冲突，直接接受并点击“下一步”。如果冲突，请在点击“下一步”之前选择另一个地址。

![](img/3a7e027360b64bc83d5cf9a2db902251_294_1.png)

- 5. 默认，使用 DHCP 为此网络中的虚拟机分配网络。DHCP 服务器可以使用选定的默认 IP 地址范围内的地址。接受此默认建议，并点击“下一步”继续。

## 练习 9.7（续）

![](img/3a7e027360b64bc83d5cf9a2db902251_295_0.png)

- 6. 在下一个窗口中，你将选择如何连接到物理网络。在本次练习中，你正在设置隔离网络，因此点击“隔离虚拟网络”，然后点击“下一步”继续。

![](img/3a7e027360b64bc83d5cf9a2db902251_295_1.png)

- 7. 现在你将看到准备好创建网络的窗口。从那里，点击“完成”在 KVM 主机上创建新的网络适配器。

第 9 章 · 使用 KVM 虚拟化

练习 9.7

### 更改虚拟机网络设置

在这项强制性练习中，你将学习如何为你的 KVM 环境切换网络配置。首先，你将在主机上设置一个隔离的虚拟网络，然后你将把虚拟机中的网卡连接到这个隔离网络。如果一切顺利，在本次练习结束时，你将能够从你的虚拟机 ping 通主机计算机。

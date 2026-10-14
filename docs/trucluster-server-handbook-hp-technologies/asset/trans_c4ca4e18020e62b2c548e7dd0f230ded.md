

## 11.2.5 输入集群互连 IP 地址

在第 10 章中，子网 10.0.0 被用作集群成员之间节点间通信的专用网络。默认情况下，10.0.0 子网加上成员 ID 会作为新成员的默认集群互连 IP 地址。为了保持一致性，并且由于它是 RFC 1918（私有且不可路由）保留地址，使用这个默认值作为虚拟集群互连 IP 地址是一个不错的选择。

```
The virtual cluster interconnect IP address '10.0.0.2' was created by replacing the last byte of the virtual cluster interconnect network address '10.0.0.0' with the previously chosen member ID '2'.
To use this default value, press Return at the prompt.

The virtual cluster interconnect IP address is the IP address associated with the virtual cluster interconnect IP name. (192.168.168.1 is an example of an IP address.)

Enter the IP address for the virtual cluster interconnect [10.0.0.2]: 10.0.0.2
Checking virtual cluster interconnect IP address: 10.0.0.2

You entered '10.0.0.2' as the IP address for the virtual cluster interconnect.
Is this address correct? [yes]: yes
```

## 11.2.6 输入集群互连类型²

从 TruCluster Server 5.1A 版开始，`clu_add_member` 命令与 `clu_create` 命令一样，让我们可以选择使用以太网 LAN 或 Memory Channel 作为集群互连。³ 在添加新成员的这一步，系统会提示我们选择集群互连类型。

为了便于说明，我们提供了两个示例，展示选择集群互连类型时应该是什么样子。第一个示例使用 Memory Channel，第二个示例使用以太网 LAN。

- 使用 Memory Channel 非常简单。我们只需选择 `mc0` 作为物理集群互连设备，确认选择，然后就完成了。

```
Device 'mc0' is the default physical cluster interconnect interface device
To use this default value, press Return at the prompt.
```

² `clu_add_member` 的这一部分在 TruCluster Server 5.0A 版和 TruCluster Server 5.1 版中不存在。

³ TruCluster Server 5.0A 版和 TruCluster Server 5.1 版仅支持 Memory Channel 作为集群互连。

```
The physical cluster interconnect interface device is the name of the physical device(s) which will be used for low level cluster node communications. Examples of the physical cluster interconnect interface device name are: tu0, es0, and nr0.

Enter the physical cluster interconnect device name(s) [mc0]: mc0
Checking physical cluster interconnect interface device name(s): mc0

You entered 'mc0' as your physical cluster interconnect interface device name(s). Is this correct? [yes]: yes
```

- 添加新集群成员时，使用以太网 LAN 作为物理集群互连比使用 Memory Channel 更复杂。首先，系统会提示我们输入物理集群互连设备。在我们的示例中，我们使用千兆以太网 LAN 卡 —— `alt0`。

```
The physical cluster interconnect interface device is the name of the physical device(s) which will be used for low level cluster node communications. Examples of the physical cluster interconnect interface device name are: tu0, ee0, and nr0.

Enter the physical cluster interconnect device name(s) []:alt0
Would you like to enter another Ethernet device? [yes]:no
Checking physical cluster interconnect interface device name(s): alt0

You entered 'alt0' as your physical cluster interconnect interface device name(s). Is this correct? [yes]:yes
```

然后系统会提示我们指定这些接口是否应配置在 NetRAIN 虚拟接口中。有关 NetRAIN 的更多信息，请参阅第 9 章。在我们的示例中，我们选择不为 NetRAIN 接口设备名称输入任何内容，因为我们只有一个以太网设备用于集群互连。

```
Enter a NetRAIN interface device name []:
```

现在软件已经知道物理集群互连设备是什么了，我们还需要物理集群 IP 名称和地址。如第 4 章和第 10 章所述，该名称由单词 `member` 加上成员 ID 和 `-icstcp0` 构成。系统会自动为我们创建该名称。

将成员 ID 附加到默认私有子网 10.1.1.0 上，就创建了默认的物理集群 IP 地址。在我们的示例中，该 IP 地址将是 10.1.1.0.2。同样，我们接受这个默认值。



`"Non-Ethernet protocols, along with information on how to set up routers to communicate beyond your LAN, are described in Chapter 17."` => `"非以太网协议以及有关如何设置路由器以在局域网之外进行通信的信息在第十七章中有所描述。"`

`"In addition to Ethernet, you need to configure TCP/IP."` => `"除了以太网外，您还需要配置 TCP/IP。"`

`"Transport Control Protocol/Internet Protocol (TCP/IP) is the standard that defines the protocols and addressing scheme (using names and numbers) that allow computers to operate over the entire world."` => `"传输控制协议/互联网协议（TCP/IP）是定义允许计算机在全球范围内运行的协议和地址方案（使用名称和数字）的标准。"`

`"TCP/IP is a transport protocol. This means that it provides end-to-end connection service between host computers."` => `"TCP/IP 是一种传输协议。这意味着它提供主机计算机之间的端到端连接服务。"`

`"The actual physical network can be carried by a variety of network service providers, which can rely on Ethernet, telephone lines, direct connections, or other media to physically carry messages."` => `"实际的物理网络可以由多种网络服务提供商携带，这些提供商可以依赖以太网、电话线、直接连接或其他介质来传输消息。"`

`"Different ways of arranging and connecting your computers in a LAN are discussed in the next section."` => `"不同的计算机在局域网中的排列和连接方式在下一节中进行讨论。"`

下一个标题：`"## Choosing a network topology and equipment"` => `"## 选择网络拓扑和设备"`

段落：`"Even with a simple LAN, you need to make some decisions about network topology (how computers are connected)."` => `"即使是简单的局域网，您也需要决定网络拓扑（计算机的连接方式）。"`

`"You also need to make some decisions about network equipment (network interface cards, wires, hubs, and so on)."` => `"您还需要决定网络设备（网络接口卡、线缆、集线器等）。"`

`### LAN Topologies` => `"### 局域网拓扑"`

列表项：

- *星形拓扑* — 在这种安排中，每台计算机包含网络接口卡（`NIC`），通过电缆连接到中央集线器。布线称为双绞线电缆，类似于用于将电话插入墙壁插孔的线缆。其他设备（如打印机和传真机）也可以在星形拓扑中连接到集线器。图 16-1 是星形拓扑的示例。

- `Bus topology` — 与使用集线器不同，总线拓扑通常被描述为从一端到另一端的链条。使用的布线是同轴电缆或细以太网电缆。一个“T”连接器连接到每台计算机的 `NIC`，然后连接到链条中的相邻计算机。链条两端的 T 连接器被终止。图 16-2 是总线拓扑的示例。

- `Ring topology` — 与星形和总线拓扑相比，环形拓扑不太流行。在环形拓扑中，计算机连接到一条环形线路上，计算机从中取并传递令牌以发送网络信息。此类拓扑通常使用 `IBM` 的令牌环形协议。

> 注意 一个既不是真正的拓扑的拓扑，也在本章中描述。您可以将两台计算机直接连接，使它们能够在不使用 `NIC` 的情况下共享任何服务。

`"For our purposes, we will focus on star and bus topologies."` => `"为了我们的目的，我们将专注于星形和总线拓扑。"`

`"Common to both topologies is the protocol used to send data over those wires — the Ethernet protocol."` => `"两种拓扑共同使用的数据传输协议是以太网协议。"`

`"Star topology is the more common among small office and home networks, for several reasons."` => `"星形拓扑在小型办公室和家庭网络中更为常见，原因有几点。"`

`"It's easy to add and remove computers without disrupting other computers on the network."` => `"轻松添加和移除计算机而不干扰网络中其他计算机。"`

`"The star cabling (twisted-pair) is more flexible, less expensive, and generally easier to handle than bus cabling (coaxial)."` => `"星形布线（双绞线）比总线布线（同轴）更灵活、更便宜，也更容易处理。"`

`"Also, many inexpensive NICs do not have the BNC connectors needed for the bus topology."` => `"此外，许多廉价 NIC 不具备总线拓扑所需的 BNC 连接器。"`

`"I have used bus topology (coaxial cables and BNC connectors) when I had old 10 Mbps NICs hanging around and only a couple of computers to connect."` => `"当我手头有旧的 10 Mbps NIC 且只有少量计算机需要连接时，我使用了总线拓扑（同轴电缆和 BNC 连接器）。"`

`"If you are starting a new installation, I recommend star topology."` => `"如果您正在进行新安装，我推荐使用星形拓扑。"`

`"The equipment is easier to deal with and more readily available."` => `"设备更易处理且更易获得。"`

`"Also, coaxial cables offer no easy way to upgrade to 100 Mbps technology."` => `"同轴电缆没有提供轻松升级到 100 Mbps 技术的方法。"`

`"Bus topology does some advantages over star topology, however."` => `"总线拓扑相对于星形拓扑有一些优势，不过。"`

`"Although the cabling is more expensive, cost savings can occur because no hub is needed."` => `"尽管布线成本更高，但可以通过不需要集线器而节省成本。"`

`"The coaxial cables are also considered extremely reliable."` => `"同轴电缆也被认为极其可靠。"`

`"Both topologies have different limitations on the number of machines that can be connected and the distances between them."` => `"这两种拓扑对可连接的机器数量和它们之间的距离有不同的限制。"`

`"Star topology's limit is 1024 nodes on the network; the total length of a bus network cannot be more than 185 meters."` => `"星形拓扑的节点限制为 1024 个；总线网络的总长度不能超过 185 米。"`

`"For a star topology, each computer must be no more than 100 meters from the hub (or a repeater if one is used)."` => `"在星形拓扑中，每台计算机距离集线器（或中继器）最多不超过 100 米。"`

`### LAN Equipment` => `"### LAN 设备"`

列表项：

- 网络接口卡 (`NIC`) — 通常，这些卡片会插入每台计算机的插槽中。对于以太网网络，卡片可以以 `10 Mbps` 或 `100 Mbps` 的速度传输数据。`Linux` 还支持新型千兆（`1000 Mbps`）`NIC` 卡。

段落：`"If you are looking to upgrade your network in the near future but still have a lot of computers around that run at 10 Mbps, you might want to consider buying new NICs that run at both 10 Mbps and 100 Mbps."` => `"如果您计划不久的将来升级网络，但仍有许多运行在 10 Mbps 的计算机，您可能需要考虑购买既能以 10 Mbps 又以 100 Mbps 运行的新 NIC。"`

`"When you switch over to 100 Mbps, you will have fewer cards to replace."` => `"当您切换到 100 Mbps 时，需要更换的卡片将更少。"`

`"Gigabit (or 1000 Mbps) NICs are quite a bit more expensive."` => `"千兆（1000 Mbps）NIC 卡价格要高得多。"`

- 对于星形拓扑，布线称为双绞线，如上文所述。电缆两端均为 `RJ-45` 插头，类似于电话线使用的插头。以太网电缆可为 `10Base-T`（`10 Mbps` 速度）、`100Base-TX`（`100 Mbps` 速度）或 `1000Base-T`（`1` 千兆）形式。它们的一端插入计算机的 `NIC`，另一端插入集线器。


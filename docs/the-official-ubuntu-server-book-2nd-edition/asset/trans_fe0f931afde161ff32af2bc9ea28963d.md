

$ /sbin/ifconfig
...
vmnet1   Link encap:Ethernet  HWaddr 00:50:56:c0:00:01
          inet addr:192.168.170.1  Bcast:192.168.170.255
          Mask:255.255.255.0
          inet6 addr: fe80::250:56ff:fec0:1/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

vmnet8   Link encap:Ethernet  HWaddr 00:50:56:c0:00:08
          inet addr:172.16.45.1  Bcast:172.16.45.255
          Mask:255.255.255.0
          inet6 addr: fe80::250:56ff:fec0:8/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

有了这些接口，你就可以通过 SSH 或主机上的其他网络工具连接到同一网络上创建的任何虚拟机。

## VMware Web 管理

过去 VMware 曾提供可用于管理 VMware 的本地应用程序，但从 VMware Server 2.0 开始，所有虚拟机管理都通过 Web 界面完成。该界面默认在 8222 端口监听 HTTP，在 8333 端口监听 HTTPS，因此打开 Web 浏览器并浏览到你的 VMware Server。如果服务器的主机名为 vmhost.example.org，你将浏览到 http://vmhost.example.org:8222 或 https://vmhost.example.org:8333，但在任何情况下你都会被重定向到 HTTPS 会话。一旦接受自签名证书并加载页面，你将被提示输入用户名和密码，因此使用你在 VMware 配置工具中指定用于管理的用户的凭据。登录后，你将看到如图 9-4 所示的默认 VMware 管理页面。

在默认管理页面上，你可以看到机器的 CPU 和内存使用情况以及 VMware Server 使用的所有数据存储。The

## 图 9-4 默认 VMware 管理页面

![](img/304f637afcecc491b152ee8ac5afadee_374_0.png)

界面相当直观；使用主窗格中的标签在不同显示之间切换。

> 注意 如果你需要有关如何导航 Web 管理工具的额外帮助，请点击页面顶部沿线的 Help 链接。这将打开一个新窗口，其中包含 VMware Server、Web 界面以及运行和调优虚拟机的文档的完整文档。

## 创建新的虚拟机

要创建新的虚拟机，请点击页面顶部的 Virtual Machine 按钮并选择 Create Virtual Machine。这将启动一个向导，会询问你有关主机的一系列问题，例如其名称、你将在其上安装的操作系统类型，以及分配多少 RAM 和存储空间。当然，所有这些选项都将根据你想要创建的虚拟机类型而有所不同，但相对简单地浏览菜单并做出选择。

当你到达 Network Adapter 部分时，你将能够在之前设置的桥接、NAT 和仅主机网络之间进行选择。你在这里的选择很大程度上取决于你是否希望将此虚拟机与 rest of the network 隔离。如果希望虚拟机看起来像网络上的任何其他机器，请选择 Bridged。如果希望它可以访问 rest of the network 但希望它位于自己的私有网络上，请选择 NAT。如果希望它完全隔离，请选择 Host-only。

当你到达 CD/DVD 驱动器部分时，你将能够选择是让此虚拟机访问服务器上的物理 CD-ROM 驱动器还是系统上的 ISO。ISO 选项很方便，因为你可以将多个安装和救援 CD 的 ISO 存储在服务器上并通过几次点击从中启动。我在 /var/lib/vmware/Virtual Machines 下创建了一个名为 isos 的目录，用来存储我想要使用的所有 ISO。你也可以添加虚拟软盘驱动器和 USB 控制器，如果需要的话。

完成向导后，你的主机将与你创建的任何其他虚拟机一起显示在左侧窗格中。点击它即可看到类似图 9-5 的屏幕，显示虚拟机的 Summary 屏幕。从此屏幕你可以监视虚拟机的 CPU 和 RAM 使用情况，查看其当前配置的硬件，并添加个人备注。

屏幕顶部你会看到形如标准停止、暂停和播放图标的快捷图标，以及一个重置电源的图标。停止按钮将切断虚拟机的电源，就像你按住服务器上的电源按钮或将其从墙上拔掉一样。播放按钮将开机机器，暂停按钮将暂停其

## 存储设置

创建新磁盘时，请注意你拥有的一些选项。如果担心空间问题，你可以告诉 VMware 根据需要增长磁盘文件，因此即使你设置了 20Gb 磁盘，如果磁盘仅使用 20%，它只会占用那么多存储空间。这节省了空间，但可能会损害磁盘性能。创建磁盘时，你必须在性能和存储之间做出决定。你还可以选择将 VMware 磁盘保存为最大 2Gb 的文件。除非你计划将虚拟机移动到文件系统最大文件大小限制为 2Gb 的系统，否则请保持此选项未选中。


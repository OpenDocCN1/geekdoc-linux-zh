
```
$ lspci
0000:00.00 RAM memory: Intel Corporation Host Bridge (rev a2)
0000:00.01 RAM memory: Intel Corporation Memory Controller 0 (rev a2)
0000:00.02 RAM memory: Intel Corporation Memory Controller 1 (rev a2)
0000:00.03 RAM memory: Intel Corporation Memory Controller 5 (rev a2)
0000:00.04 RAM memory: Intel Corporation Memory Controller 4 (rev a2)
0000:00.05 RAM memory: Intel Corporation Host Bridge (rev a2)
0000:00.06 RAM memory: Intel Corporation Memory Controller 3 (rev a2)
0000:00.07 RAM memory: Intel Corporation Memory Controller 2 (rev a2)
0000:01.02 PCI bridge: Intel Corporation PCI Bridge (rev a1)
0000:03.00 PCI bridge: Intel Corporation PCI Bridge (rev a1)
0000:04.00 PCI bridge: Intel Corporation PCI Bridge (rev a1)
0000:05.00 VGA controller: Intel Corporation Express Bridge
0000:09.00 Host bridge: Intel Corporation Host Bridge (rev a2)
0000:0a.00 ISA bridge: Intel Corporation PCI Bridge (rev a2)
0000:0a.01 USB bus: Intel Corporation Bus (rev a2)
0000:0b.00 USB controller: Intel Corporation USB Controller (rev a2)
0000:0b.01 USB controller: Intel Corporation USB Controller (rev a2)
0000:0d.00 IDE interface: Intel Corporation IDE (rev a1)
0000:0e.00 IDE interface: Intel Corporation SATA Controller
0000:0f.00 IDE interface: Intel Corporation SATA Controller
0000:10.00 PCI bridge: Intel Corporation PCI Bridge (rev a2)
0000:10.a3 Audio: Intel Corporation High Definition Audio (rev a2)
0000:14.00 Bridge: Intel Corporation Ethernet Controller (rev a1)
0000:18.00 Host bridge: Hypertransport Technology Configuration
0000:18.01 Host bridge: [Ath64/Opteron] Address Map
0000:18.02 Host bridge: [Ath64/Opteron] DRAM Controller
0000:18.03 Host bridge: [Ath64/Opteron] Miscellaneous Controller
0000:04.05 FireWire (IEEE 1394): LSI, Inc. IEEE 1394 Host Controller
0000:04.08 SCSI storage controller: LSI Logic / Symbios Logic 3c598
0000:04.09. Ethernet controller: 3Com Corporation 3c596 100BaseTX [Vortex]
```

虽然此输出看起来很丑，但很容易扫描以确定你的新卡是否被检测到。如果是，你应该运行与 PCI 卡提供的功能或设备类型相关的配置工具。

# 图形化查看和调试设备

Ubuntu 系统提供了一个名为“设备管理器”的优秀图形实用程序，允许你从系统的视角浏览、导航并探索系统硬件。该工具默认未安装，但你可以使用你喜欢的包管理软件（如第 19 章所讨论）在 Ubuntu 系统上安装 `gnome-device-manager` 包。如果已安装，在 Ubuntu 系统上选择应用程序 -> 系统 -> 设备管理器来启动此工具，它将显示图 20-21 所示的初始对话框。

图 20-21

Ubuntu 的设备管理器

![](img/1a233c34336fbf5a85d6eb785e401709_799_0.png)

# 第 20 章：添加硬件和连接外设备

显示设备管理器后，你可以使用左侧的面板滚动或钻取，以检查系统提供的任何基本设备或连接到其任何接口的设备。当你选择不同的设备时，设备管理器右侧面板会显示相应的标签页。右侧面板通常提供一个通用的设备信息标签页和一个“高级”标签页，后者提供了有关所选设备或接口的更多细节。

此实用程序提供的信息对于确定你的系统硬件正在被识别（或是否被识别）非常有用，这可以帮助你在尝试解决新硬件问题时知道从何处开始。对于我们许多人来说，看到系统如何识别、组织和使用硬件也仅仅是一件很有趣的事。

## 总结

本章解释了如何向系统添加各种类型的硬件，从你只想临时使用的可移动存储设备，到更永久连接的设备，如打印机、新的内置硬盘和扫描仪。

下一章将探索如何保护你的 Ubuntu 系统。虽然 Linux 通常对泛滥互联网（以及大多数 Windows 系统）的大多数类型病毒、木马和间谍软件具有免疫，但 Linux 系统的网络安全性对于任何可能直接连接到互联网的计算机系统来说都是至关重要的。有数百本专门介绍网络和计算机安全的书籍，但下一章将对关键概念和关注点提供基础解释，阐明你可能想要保护系统的一些基本方法，并重点介绍你可能想要进一步研究的领域。

# 第 21 章

## 网络配置与安全

几乎从 20 世纪 70 年代家庭计算开始开始，个人电脑就开始与其他类型的计算机系统接触。在互联网服务提供商（ISP）出现之前，在互联网存在之前，家用计算机爱好者使用调制解调器访问公告板系统（BS）、远程大型主机或小型计算机，以及如 CompuServe 和 AOL 等古老的内容提供商，使用各种终端仿真程序进行相互通信、传输文件等。早期的存储和转发机制（如 Unix-to-Unix Calling Program (UOCP) 和 FidoNet）为在缓慢的计算机系统网络中传播文件和其他信息提供了很好的方法，这些网络之所以被称为网络，是因为它们知道彼此的电话号码。

ARPANET 转换为互联网及其随后的商业化诞生了 ISP（商业互联网服务提供商）的概念，为家用计算机直接访问互联网提供了机制，尽管是通过那些笨拙的对点解决方案，这些解决方案仍然依赖于调制解调器，因此提供的上网浏览速度仅（据称）被保证大于零。无论如何，ISP 的出现结束了 PC 的孤立，使其成为互联网的真正参与者，即使速度很慢。

随着 ISP 的出现并成为许多家用计算机用户的基础实用程序，网络和 PC 硬件成本持续下降，接近了通常与烤面包机和冰箱相关的商品级价格。越来越多的家用计算机用户（即使在同一栋房屋内）引入了家庭计算机网络的概念，这些网络通常是独立的，或者通过调制解调器作为 ISP 的 9,600 或 56-KB 网关，将特定系统连接到互联网。

## 本章内容

- 用于网络配置的图形化工具
- 传统的网络配置文件
- 测试网络接口
- 安装防火墙

# 第二部分：面向桌面用户的 Ubuntu

宽带以太网、更廉价的有线硬件以及无线网络的爆炸式增长，让许多家用计算机用户使这成为了现实。家用计算机系统现在可能拥有真实的 IP 地址和连接互联网的功能性连接速度，并且通常是家庭计算机网络的成员，使用网络地址翻译 (`NAT`) 等机制共享这些互联网连接。如果你是网络领域的新手，本章的第一节提供了基本网络概念和术语的概述。

更好的网络和网络访问是有代价的。无处不在的网络让成千上万的“随机人士通过真实的 IP 服务器或其他网络进程访问你的计算机系统。他们大多数人并不在乎，有些仅仅是好奇，而另一些则是完全的恶意的。最后这些人通过某种方式主动尝试入侵计算机，给所有人脸抹了黑脸。我不反对那些仅仅对外部世界感到好奇的黑客——探索一直以来是人类生存状况的基本组成部分。真正的黑客是电子版的《国家地理学会》或《星际迷航》，在那个地方没有人涉足过。然而，那些闯入系统以破坏或利用它们的人是“破解者”（crackers），他们给所有人脸抹了黑脸。

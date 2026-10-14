
这台 VAIO 确实有 USB 接口，但不支持从 USB 启动。我唯一的选择就是拆开它。幸运的是，我在网上找到了一篇拆卸指南。这一发现非常幸运，因为这类旧 VAIO 结构非常紧凑，没有带照片的指南我很可能会损坏它。值得一提的是，网上有很多针对各种笔记本型号的类似教程。

拆开电脑后，我考虑用 DSL 商店的笔记本 IDE 紧凑型闪存适配器替换硬盘。但这台电脑只有

如果你从未在静音电脑上工作过，你真的不知道那会是多么惬意。你听到的唯一噪音就是你想听到的声音（例如一些音乐或电台直播）。我听过许多电脑用户说，一旦改用静音电脑，他们就再也无法忍受嘈杂的电脑了。

市面上有静音电脑，一些高端机型的售价高达数千美元。还有一些基于 Mini-ITX 的小型机专门为静音而设计，但这些电脑也往往非常昂贵（基础配置常常超过 800 美元）。这些电脑之所以定价昂贵，是因为它们是按特殊订单限量生产的。要让静音 PC 价格亲民，就需要大规模生产，但这是一个过于小众的市场，难以实现。

## 瘦客户机作为静音 PC

瘦客户机数量很多，而且许多价格实惠。它们通常没有活动部件，因此很安静，而是依靠被动散热来降低 CPU 温度。

专为瘦客户机设计的电脑也可以非常小巧、颇具吸引力。许多较新的瘦客户机都提供板载存储能力，例如 IDE 闪存、内置紧凑型闪存读卡器，或可安装笔记本尺寸硬盘的插槽。许多较新的瘦客户机还可以通过 USB 启动。

瘦客户机的价格通常低于 300 美元。在 eBay 等网站上，二手的几乎白送，不过它们通常是较老的型号，性能往往不足。

我们在 DSL 商店中最畅销的两款机型是 eBox III（又称 Damn Small Machine，DSM）和来自台湾的基于 Mini-ITX 的瘦客户机，我们称之为 Bargain BareBones。两者都面向瘦客户机市场，因此价格实惠，但它们也非常适合运行 DSL。图 12-4 展示了 eBox III 的一个例子。

DSM 采用板载内存，也就是固定为 256MB。这个容量确实不足以流畅运行某个知名操作系统，但运行 DSL 绰绰有余。DSM 出厂时就可以直接从 USB 闪存盘启动，因此如果你愿意，完全可以不用 IDE 硬盘。

如果你更喜欢 IDE 启动，确实有几个选择。你可以选择专为 DSM 制造的 IDE DOM（模块化磁盘）。此外，DSM 还预留了笔记本尺寸硬盘的位置。因此，你可以使用传统硬盘，也可以选择将传统 CF 卡安装到 IDE CF 适配器上。主板搭载 Via 700MHz Nano 处理器，这对 DSL 来说同样绰绰有余。图 12-5 展示我们的 BareBones 机器，旁边是一个更典型尺寸的 Mini-ITX 机箱。

FIGURE 12-4 The eBox III, a very compact machine with room for a hard drive.

![](img/af53325d7f38f1cdafca9f44568e4ab8_276_0.png)

FIGURE 12-5 Compare the size of the BareBones to a typical Mini-ITX case.

![](img/af53325d7f38f1cdafca9f44568e4ab8_276_1.png)

The Bargain BareBones is an example of a Mini-ITX-based thin client. Again, the design is very small, much more compact than a typical Mini-ITX computer. The BareBones was never intended to be a standalone workstation, and it has no provision for a hard drive or a media drive. Although the unit comes without RAM, it accepts 184-pin DIMM socket DDR RAM up to 1GB.

Unlike the DSM, the BareBones cannot take a hard drive, but there is room for an IDE DOM; at the DSL store, we have 1GB units available. The DOM is not needed if you are content with booting via USB.

Personally, I use one of each of these thin client computers. I have the DSM in my home office and the BareBones at work. Each of them has an IDE DOM, but I do not use them for booting. Instead, I only use them for occasional backup when I have important documents I want to save on them in one place.

I go back and forth between the two units using a single bootable pen drive that I use as my portable office. This way, regardless of where I am, I have my desktop the way I like it and I can continue working from the point at which I last stopped. DSL’s auto configuration automatically sets the ramdisk according to the available RAM.

Other than this adjustment, I have the same system, same files, same everything on both thin clients. It is a nice way to work. Unlike the traditional use of these computers as thin clients, I am not dependent on any network for my files or applications, and I have all my work with me on the pen drive.

If you are not the mobile type, you may want to consider running DSL from an IDE drive, whether it is a hard drive (DSM), IDE CF conversion (DSM), or disk on module (DSM or Bargain BareBones). The units are self-contained with this approach. The fact that most of the newer thin clients can boot from USB makes installing to an IDE drive easy. Simply boot up DSL via USB and perform a Frugal install (see Chapter 8).

## Green Machines

In general, alternative hardware is often environmentally friendly, whether it is a diskless homemade PC, a Mini-ITX system, a discarded laptop, or a thin client converted to run as a desktop PC. You can feel good about using less energy than with a conventional computer. In addition, when working with used equipment, you are keeping usable systems out of landfills. By using Damn Small Linux, you are contributing to a healthier planet. Now about that SUV…..

## SUMMARY

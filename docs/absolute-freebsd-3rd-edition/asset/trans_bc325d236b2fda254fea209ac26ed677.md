

## 包含与排除

FreeBSD 的内核配置有两个有趣的功能，可以使内核维护变得更容易：`no` 选项和 `include` 功能。

`include` 功能允许你将单独的文件引入内核配置中。例如，如果你的内核配置可以描述为“带有几个额外小功能的 GENERIC”，你可以使用 `include` 语句包含 GENERIC 内核配置：

```
include GENERIC
```

因此，如果你想构建一个具有 GENERIC 所有功能但也支持 VIA 3d 芯片 DRM 功能特性的内核，你可以创建一个完全由以下内容组成的有效内核配置：

```
ident VIADRM
include GENERIC
options drm
options viadrm
```

你可能会认为这实际上比将 GENERIC 复制到新文件并进行编辑要麻烦，你是对的。那么，为什么要费心这样做呢？最大的原因是，当你升级 FreeBSD 时，GENERIC 配置可能会发生变化。FreeBSD 12.1 中的 GENERIC 与 12.0 中的略有不同。你的新配置对这两个版本都有效，并且在两种情况下都可以合法地描述为“GENERIC 加上我的选项”。

这在包含条目时效果很好，但不太适合从内核中移除事物。与其手动为每个新的 FreeBSD 版本重新创建内核，你可以使用 `include` 语句，但使用 `nodevice` 和 `nooptions` 关键字来排除不需要的条目。使用 `nodevice` 移除不需要的设备驱动程序，而 `nooptions` 则禁用不需要的选项。

看看 -current 机器上的 GENERIC-NODEBUG 内核配置。它与 GENERIC 配置相同，但禁用了所有的调试功能。

```
include GENERIC

ident   GENERIC-NODEBUG

nooptions       INVARIANTS
nooptions       INVARIANT_SUPPORT
nooptions       WITNESS
nooptions       WITNESS_SKIPSPIN
nooptions       BUF_TRACKING
nooptions       DEADLKRES
nooptions       FULL_BUF_TRACKING
```

我们首先包含 GENERIC 内核配置。然而，该内核将自身标识为 GENERIC-NODEBUG。接下来的七个 `nooptions` 语句关闭了 FreeBSD-current 的标准调试选项。开发人员使用 GENERIC-NODEBUG 内核来查看内核调试器是否会导致问题。如果带有调试功能的内核发生恐慌（panic），而没有调试功能的内核不恐慌，调试代码突然就显得可疑了。

## 跳过模块

如果你费心构建了一个自定义内核，你可能确切知道你的主机需要哪些内核模块。如果你永远不使用它们，为什么要构建这些数十个内核模块呢？你可以使用 MODULES_OVERRIDE 选项关闭模块的构建。将 MODULES_OVERRIDE 设置为你想要构建和安装的模块列表。

```
# make MODULES_OVERRIDE='' kernel
```

也许你想要构建大多数模块，但你有理由讨厌某个特定模块。使用 WITHOUT_MODULES 将其排除在构建之外。在这里，我将 vmm 排除在构建之外，因为我不希望即使有一点点在 VirtualBox 上运行 bhyve(8) 的诱惑。从这里到运行十几层虚拟化并纳闷为什么我的笔记本电脑很慢，只是一小步而已。

```
# make KERNCONF=VBOX WITHOUT_MODULES=vmm kernel
```

有选择地构建模块，结合自定义内核，可以让你把自己锁定在真正极小的盒子里。只有当你发现自己缺少一个从未想到需要的功能时，你才会明白那些盒子有多小。如果你必须构建内核，请慷慨地保留功能。

现在你的本地机器已经按照你想要的方式精确调整好了，让我们来看看互联网的其他部分。

# 7. 网络

![](img/f11aeb3fa2ed406688e13ccb43ed9dab_227_0.png)

FreeBSD 以其网络性能而闻名。TCP/IP 网络协议套件最初是在 BSD 上开发的，而 BSD 反过来包含了第一个主要的 TCP/IP 实现。尽管在 1980 年代，竞争性的网络协议被认为更具吸引力，但 BSD TCP/IP 堆栈的广泛可用性、灵活性和宽松许可证使其成为*事实上的*标准。这不仅仅是一个历史趣闻；如今，Facebook 正在积极寻找能够使 Linux 网络性能与 FreeBSD 相匹配的工程师。该项目预计需要数年时间。

如今许多系统管理员对网络基础有一些模糊的了解，但并不真正理解它是如何整体运作的。然而，优秀的系统管理员理解网络。了解 IP 地址真正是什么，子网掩码如何工作，以及端口号与协议号有何不同，是掌握你职业的必要步骤。我们将在本章中涵盖这些问题。首先，你必须理解网络层。

虽然本章对 TCP/IP 提供了一个不错的概述，但它不会涵盖许多细节、陷阱和注意事项。如果你需要更多地了解 TCP/IP，请阅读一本关于该主题的书籍。要获得概述，可以查看我的书*Networking for Systems Administrators*（Tilted Windmill Press, 2015 年）。最终你需要深入研究网络；可以直接阅读 Charles M. Kozierok 的*The TCP/IP Guide*（No Starch Press, 2005 年）。

## 网络层

主要互联网协议是 TCP/IP（传输控制协议运行在互联网协议之上）。TCP 是一种传输协议，而 IP 是一种网络协议，但它们紧密交织在一起，通常被视为一个单一实体。我们将了解网络如何工作，然后讨论 IP 版本 4 和 6，并进一步讨论 TCP 和 UDP。

网络的每一层都在网络处理过程中执行特定的任务，并且只与其上方和下方的层进行交互。学习 TCP/IP 的人常常在听到所有这些层简化了网络处理过程时会发笑，但这确实是事实。现在需要记住的重要事情是，每一层只与其直接上方的层和直接下方的层进行通信。

经典的开放式系统互连（OSI）网络协议堆栈有七层，详尽完整，几乎涵盖了任何网络协议和任何应用程序的任何情况。然而，互联网只是其中一种情况，而这不是一本关于通用网络或网络应用的书籍。我们将讨论限制在 TCP/IP 网络上，例如互联网和几乎所有企业网络，因此我们只需要考虑网络堆栈的四层。

## 物理层

在最底层，我们有物理层：网络卡片以及离开它的导线、光纤或无线电波。该层包括物理交换机；集线器或基站；连接该设备到路由器的电缆；以及从你的办公室延伸到电话公司的光纤。电话公司交换机是物理层的一部分，洲际光纤电缆也是如此。如果它可以被绊倒、掉落或被链锯切断，它就是物理层的一部分。从这一点开始


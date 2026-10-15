

双启动确实具有一定的优势。虽然你的计算机单独运行 Linux 时性能从未受到阻碍，除非你运行 VMware，VMware 中的访客操作系统总是运行得比完全控制计算机资源时慢一些。

此外，由于访客操作系统无法完全访问你的 PC 硬件，在 VMware 会话中可能存在某些设备无法正常使用或完全无法使用，而如果直接启动到该操作系统则可以正常工作。（硬件兼容性在第 2 章“理解 VMware 的工作原理”中有进一步讨论。）表 1.1 提供了 VMware 与双启动环境功能和缺点的快速比较。

表 1.1 VMware 与双启动的比较

| 方法 | 优点 | 缺点 |
|---|---|---|
| VMware | 同时运行多个操作系统<br>易于安装/配置 | 额外费用<br>访客操作系统部分变慢 |
| 双启动 | 无额外成本<br>完全、原生的硬件支持 | 配置困难<br>切换不便 |

> 有关双启动的更多信息，以及其他各种主题，请访问 Linux 文档项目 http://www.linuxdoc.org。

## VMware 与 DOS 和 Windows 模拟器

VMware 绝不是第一个尝试将 Windows 兼容性带到 Linux 的产品，尽管它在虚拟机方法上是独一无二的。

## 模拟，就像美酒一样...

最古老、也是最著名的 Windows 模拟器之一是 Wine。实际上，“模拟器”并不是 Wine 的准确术语（Wine 是一个缩写，有多种含义，其中之一是“Wine Is Not an Emulator”，即 Wine 不是模拟器）。

## Bochs：完整 PC 模拟

Bochs 被设计为高度可移植，已成功在各种不同的计算机架构和操作系统上编译运行。这是因为 Bochs 是一个真正的模拟器，而不是虚拟机。

还记得区别吗？Bochs 基于 Intel 386/486/Pentium CPU 模拟，即使在基于 Pentium 的 Linux PC 上使用 Bochs 也会运行。这使得 Bochs 在所有受支持平台上都是一个一致的产品，但也意味着它比 VMware 等真正的虚拟机慢得多。它的配置文件也 ridiculously 杂乱无章，让 DOSEMU 看起来都很容易管理。图 1.6 显示了一个 Bochs 会话示例。

Bochs 最近被 MandrakeSoft 收购并作为开源发布，MandrakeSoft 是 Linux-Mandrake 发行版的出版商。Bochs 的原始作者 Kevin Lawton 现在正忙于 Plex86，这是一个开源虚拟机项目。

> 要了解更多关于 Bochs 的信息，请访问 http://www.bochs.com。

仅 VMware 易于使用的配置界面就足以让它在这些替代方案中胜出。VMware 也是获得与 Windows 95/98、Windows NT 和 Windows 2000 完全兼容的唯一方法。虽然每种都有其用途——甚至可能随着时间的推移在你的模拟策略中找到一席之地——但 VMware 提供了在 Linux 下运行 MS-DOS 和 Microsoft Windows 应用程序的最快和最灵活的方式。

同样重要的是要记住，VMware 不仅仅是为 Windows 应用程序提供模拟环境。使用 VMware，你可以运行另一个完整的 Linux 或 FreeBSD 会话，并且 VMware 的程序员继续努力扩展可在虚拟机中运行的操作系统范围。虽然 Bochs 对其他操作系统的支持正在缓慢增长，但 VMware 提供了最广泛的保证兼容性范围。

![](img/b2b6702758c230ce537468351fc8af15_36_0.png)

图 1.6 Bochs PC 模拟器，正在加载 WebSpyder Web 浏览器。

## 结论

你现在应该对模拟器和虚拟机背后的技术有了基本的了解，并且已经看到了 VMware 让你的 Linux PC 扩展其覆盖范围和软件兼容性的潜力。

第 2 章更详细地描述了 VMware 的内部工作原理，并解释了 VMware 与各种 PC 硬件和软件配置的兼容程度。



```
# kernel /vmlinuz-version ro root=/dev/sda2
# initrd /initrd-version.img
#
# default=0
# timeout=10
default=0
timeout=10
splashimage (hd0,0)/grub/splash.xpm.gz
title Red Hat Linux (2.4.7-10)
  root (hd0,0)
  kernel /vmlinuz-2.4.7-10 ro root=/dev/sda2
  initrd /initrd-2.4.7-10.img
title Windows 2000
  root (hd0,3)
  makeactive
  chainloader +1
```

关于 GRUB 的一个重要点是其磁盘引用记法。根引用 (hd0,0) 表示它位于 0 号硬盘的 0 号分区。如果我们想从 1 号硬盘的 3 号分区启动，那就是 (hd1,3)。

default 参数指定默认应启动哪个操作系统；零表示列出的第一个操作系统（Red Hat Linux）。timeout 变量指定 GRUB 在启动前显示其菜单的时间长度（以秒为单位，而不是 LILO 中令人困惑的十分之一秒），而 splashimage 表示要使用的背景图形的名称。

每个可启动的操作系统随后都用标题和根分区指示符指定（同样是磁盘、分区）。对于 Unix 系统，你在 kernel 行上指定内核信息（注意 ro 表示磁盘应以只读方式挂载，就像在 LILO 中所做的那样）。

非 Unix 操作系统（例如 Windows 2000）的配置则大不相同，因为本质上没有内核。相反，GRUB 使用所谓的 chainloader，它告诉 GRUB 让开，让指定磁盘和分区上的引导加载程序接管。

- 2. 你不需要做任何事情来安装新配置，但因为你不想在启动时遇到配置文件的格式错误，明智的做法是显式安装新的 GRUB 配置，通过运行 grub-install：

```
# /sbin/grub-install /dev/sda
Installation finished. No error reported.
This is the contents of the device map /boot/grub/device.map.
Check if this is correct or not. If any of the lines is incorrect,
fix it and re-run the script 'grub-install'.

(fd0)   /dev/fd0
(hd0)   /dev/sda
```

与 LILO 不同，如果安装程序发现配置有问题，它不会使系统处于无法使用状态，因此你不必对在测试模式下运行感到偏执。

- 3. 现在启动时你将可以选择两个操作系统，并且你还将拥有一个吸引人的启动屏幕，如图 11.1 所示。

图 11.1
GRUB 启动屏幕，包含两个操作系统。

![](img/5ced0c78d748bd190e9027e5549a3622_242_0.png)

通过查阅 GRUB info 页面可以获得更多关于 GRUB 的信息。输入 info grub 即可继续。

## 其他 Unix 系统的其他解决方案

虽然双启动以及让不同的操作系统各自生活在自己的分区世界中对许多人很有吸引力，但如果你愿意牺牲次要操作系统的 10–30% 性能，还有另一种替代方案。

Windows 和 Mac OS 都支持虚拟机，前者通过在受保护空间中对引导加载程序进行一些巧妙的模拟，后者通过在 Apple 平台上对 Intel 硬件架构进行仿真。

本书的范围超出了对这些进行太多讨论，但值得用几张快速截图向你展示如何创建一个虚拟 Unix 操作系统用于实验和练习，而不必担心会损害正在运行的生产系统。

## 任务 11.4：了解虚拟机

在 Intel 平台上运行虚拟机的最流行解决方案是 VMware，来自 VMware Corporation（www.vmware.com）。安装此程序后，你可以创建虚拟 Unix 操作环境，甚至可以为测试安装多个 Windows 操作系统。性能大约是原生加载的 80–90%，因此并不完全一样快。值得注意的是，你也可以在 Linux 系统上安装 VMware，从而在 Linux 中运行 Windows。

在 Macintosh 上，Connectix Corporation（www.connectix.com）的 Virtual PC 提供了类似的功能，尽管由于需要仿真 Intel 硬件架构（包括 CPU）而性能损失更高。在非常快的 Mac OS X 系统上，Virtual PC 运行起来像一台稍显迟缓的 PC。

- 1. 当你在 PC 上安装了 VMware 后，你可以安装几个不同的操作系统，并通过简单地点击相应的图标来启动你选择的那个。图 11.2 显示了在 VMware 中运行 Red Hat Linux 7.2 的 Windows 2000 系统。

图 11.2
VMware 让你在操作系统内部运行另一个操作系统。

![](img/5ced0c78d748bd190e9027e5549a3622_243_0.png)

你也可以以全屏模式运行虚拟机，消除所有 Windows 杂乱（或者，如果你在 Linux 中运行 VMware，你可以隐藏所有 Linux 内容，看起来就像直接运行 Windows 一样）。

- 2. Macintosh 上的 Virtual PC 在功能上非常相似。图 11.3 显示了 Macintosh 屏幕，其中 Virtual PC 再次运行 Red Hat Linux 7.2。尽管太小而无法看到，Windows 98 SE 和 Windows 2000 是此 Macintosh 设置上可用的其他操作系统。

图 11.3
Virtual PC 让你在 Mac OS X 上运行多个操作系统。

![](img/5ced0c78d748bd190e9027e5549a3622_244_0.png)

与 VMware 一样，Virtual PC 也允许你运行全屏模式，这略微提高了性能并消除了任何分散注意力的 Macintosh 视觉杂乱。

软件测试人员多年来一直使用 VMware 等产品来访问 Windows 和 Unix 的许多不同版本，这也是学习 Unix 系统管理的一种非常好的方式，其安全性远高于直接在物理机器上操作。最坏的情况下，如果你完全搞乱以至于无法启动，只需删除虚拟机映像并构建一个新的即可。更好的是，它允许在原生操作系统与虚拟或仿真操作系统之间轻松复制粘贴。

## 摘要

本小时重点介绍了多操作系统启动配置，从使用 Unix 工具对硬盘进行分区开始，然后深入研究了最流行的引导加载程序 LILO 和 GRUB。最后，我们讨论了在另一个操作系统的环境中运行一个操作系统的不同可用选项。

## 问答

Q 修改引导加载程序配置不是很危险吗？

A 当然是。事实上，在本章制作期间，test lilo.conf 文件中的一个多余字符给我带来了无尽的痛苦，至少浪费了八个小时。再次提醒，要小心谨慎地处理这些配置文件，并确保将原始启动参数集的备份作为其中一个选项。并且始终确保你有启动磁盘，以防万一....

Q 如果 VMware 这么酷，为什么还要双启动？

A VMware 和其他虚拟机系统提供了一种非常巧妙的方法在安全环境中运行操作系统，但它不是原生安装，而且你肯定不希望在虚拟机中运行 Web 服务器。网络和外设交互方面也有一些细微差别，在宏观上可能无关紧要，但在你管理用于开发设备驱动程序或其他低级解决方案的机器时可能会变得重要。

Q 那么，你的系统上安装了多少个操作系统？

A 我只说，在我的 Titanium Powerbook 上，它原生启动到 Mac OS X，然后使用 Virtual PC 我可以切换到全屏模式运行 Linux、Solaris、Windows 2000 和 Windows 98。当有人从我身后看过来时，这肯定会让人困惑！

![](img/5ced0c78d748bd190e9027e5549a3622_245_0.png)

## 练习

## 测验

- 1. LILO 代表什么？GRUB 代表什么？
- 2. 启动顺序是 BIOS、PRAM，然后是什么？
- 3. 想要设置双启动系统的系统管理员面临的最大挑战是什么？
- 4. 在 lilo.conf 文件中，使用 timeout 参数时需要注意什么？
- 5. GRUB 开发者修复了 LILO 中的什么关键设计错误，帮助成千上万的系统管理员避免了噩梦？


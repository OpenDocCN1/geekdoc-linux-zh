

Win4Lin 是由 NeTraverse 开发的 Wine 的商业替代方案。Win4Lin 声称比 Wine 更稳定，并支持一些微软应用程序。然而，它需要对内核进行修改，而 Wine 则不需要。Win4Lin 可以从 win4lin.com 获取。

# 双启动，以及为什么你不应该这样做

如果你曾经在一台曾作为 Windows 机器的电脑上安装过 Linux，那么你无疑被提供过设置双启动配置的选项。此类配置的功能确实如此：你可以在 Linux 下挂载 Windows 分区，并从 Windows 访问 Linux 文件系统。请阅读第 85 页有关设置双启动配置的详细信息。

但等一下！如果你正在进行实际工作并需要同时访问 Windows 和 UNIX，在生产系统的背景下，请对双启动作为可能的解决方案持非常怀疑的态度。双启动设置在最坏的情况下代表了墨菲定律：它们似乎总是启动到错误的操作系统，而且即使是微小的任务都需要多次重启。随着泛虚拟化的普及和廉价硬件的出现，通常没有理由让自己忍受这种折罪。

# Microsoft Office 替代方案

几年前，太阳公司（Sun）以 OpenOffice 的名称发布了 StarOffice（类似于 Microsoft Office 的应用程序套件）的开源版本。OpenOffice.org 包含了电子表格、文字处理器、演示文稿包以及类似于 Microsoft Access 的数据库应用程序。这些工具可以读写由其微软对应产品生成的文件。你可以从 openoffice.org 下载该套件。

OpenOffice.org 适用于所有主流平台，包括 Windows、Linux、Solaris、Mac OS 和大多数版本的 Unix。如果你正在寻找一个带有商业支持合同的软件包，你也可以购买太阳公司的 StarOffice，它本质上是带有支持和更佳拼写检查的盒装版 OpenOffice。

Google 在应用方面通过 Google Apps 提议来与之竞争。除了其强大的 Gmail 和 Google 日历服务外，Google 还包含了文字处理和电子表格。这些免费产品包含了协作功能，允许多个用户从多个位置同时编辑文档。由于 Google 的所有应用都运行在网页浏览器中，因此它们可以在几乎任何操作系统上使用。你可以以各种格式导出和导入内容，包括 Microsoft Office 的格式。

# 30.4 在 Windows 中使用命令行工具

许多 UNIX 人在 Windows 系统上工作时，最最想念的是他们喜爱的命令行终端。不仅仅是任何老旧的应用程序或被称为 DOS 框的丑产物，而是一个支持窗口缩放、颜色、鼠标控制以及花哨的 xterm 转义序列的正规 xterm。

# Windows 对电子邮件和网络标准的兼容性

尽管 Windows 没有独立的（即 X 的）原生 xterm 端口，但一个名为 rxvt 的整洁小程序非常接近这一点。它是 Cygwin 系统的一部分，可以从 cygwin.com 下载。如果你使用 Cygwin 的 X 服务器，你就可以使用真正的 xterm。

Cygwin 由 GNU 通用公共许可协议（GPL）分发，包含了大量的常用 UNIX 命令补集，以及一个在 Windows 下实现 POSIX API 的可移植库。由于Cygwin 对 UNIX 和 Windows 命令行及文件系统规范的协调是经过深思熟虑的，并成功将许多 UNIX Shell 的舒适感带到了家，通过Cygwin，在 Windows 下运行 UNIX 软件变得简单。更多详细信息请参阅 cygwin.com。

MKS Toolkit 是 Cygwin 的商业替代方案。更多信息请访问 MKS 的网站 mksoftware.com。

现在有越来越多的 UNIX 软件在 Windows Windows上原生运行，包括 Apache、Perl、Bind、PHP、MySQL、Vim、Emacs、Gimp、midrange 和 Python。在尝试用类似 Cygwin 工具强制让应用程序在 Windows 上运行之前，先确认是否有原生实现版本。

# 30.5 Windows 对电子邮件和网络标准的兼容性

在一个理想的世界里，每个人都使用开放标准进行通信，快乐无处不在。但这不是一个理想的世界，许多人指责 Windows 是私有协议的堆砌和互联网标准破碎实现的产物。也许部分是正确的，Windows 在世界上某些地区可以相处得很好。其中两个领域是电子邮件和网络服务。

在网络的发展史上，许多公司试图以各种方式拥抱并扩展网络，以便能够排除竞争并为自己的业务提供强力助力。微软在浏览器层面仍在参与这场战斗，拥有许多针对 Internet Explorer 特有的扩展。然而，Windows 和 Windows 浏览器是相对与平台无关的。

微软提供了了自己的 Web 服务器 IIS，但从历史上看，IIS 的采用率远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

[content]
...
，也许部分是正确的，Windows 在世界上某些地区可以相处得很好。其中两个领域是电子邮件和网络服务。

在网络的发展史上，许多公司试图以各种方式拥抱并扩展网络，以便能够排除竞争并为自己的业务提供强力助力。微软在浏览器层面仍在参与这场战斗，拥有许多针对 Internet Explorer 特有的扩展。然而，Windows 和 Windows 浏览器是相对与平台无关的。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

微软提供了了自己的 Web 服务器 IIS，但 IIS 的采用率在历史上远落后于运行在 Linux 上的 Apache。除非你被锁定在 ASP 等服务器端技术上，否则 Windows 在世界上某些地区可以表现得很好。

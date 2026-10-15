
请参阅 Martin S. Michael 编写的国家半导体公司“应用笔记 AN-493”。5.0 描述了 NS16550 和 NS16550A 的区别。简单来说，NS16550 在 FIFO 电路中有缺陷，而 NS16550A（及后续）芯片修复了这些问题。然而，国家半导体在很久以前生产的 NS16550 很少，且实际板上的许多“16550”部件来自许多兼容部件制造商，这些部件可能没有使用国家半导体后缀。此外，某些多端口板将使用来自国家半导体或其他供应商的 1652 或 1653 或各种多端口芯片（通常采用高密度封装）。

### 15.1. 支持的

任何标准的串口/摇杆/组合卡。Linux 支持 8250, 16450, 16550 和 16550A UART。可以使用支持非标准 IRQ（`IRQ > 9`）的卡。

### 15.2. 其他

任何标准的串口/摇杆/组合卡。Linux 支持 8250, 16450, 16550 和 16550A UART。可以使用支持非标准 IRQ（`IRQ > 9`）的卡。

## 16. CD 刻录机

## 17. 可移动驱动器

## 18. 鼠标

### 18.1. 支持的

任何标准的串口/摇杆/组合卡。Linux 支持 8250, 16450, 16550 和 16550A UART。可以使用支持非标准 IRQ（`IRQ > 9`）的卡。

### 18.2. 其他

### 18.3. 注意

触摸板设备如 Alps Glidepoint 也可以工作，只要它们兼容另一种鼠标协议。新鼠标

## 19. 调制调器

所有内部调制调器或连接到串口的外部调制调器都应该工作。此外，某些制造商创建了仅限 Windows 95 的调制调器。请查看附录 D 获取不支持 Linux 的硬件。

Digicom Connection 96+/14.4. - DSP 代码下载程序

# 44 第1章：规划

`linux.1.02.tar.gz`

摩托罗拉调制调器 SURFR 内部 56K。在 `RC.SERIAL` 中添加几行代码以考虑 IRQ 和端口（如果它们是非标准的）。

友讯 U-1496 系列 - 友讯 1.4 调制器/传真/语音控制程序 <http://www.pelchl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz>

友讯 Elite 2864 系列 - 调制器/传真/语音控制程序 <http://www.pelchl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz>

友讯 Omni - 调制器/传真/语音控制程序 <http://www.pelchl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz>

Linux 还支持多功能调制调器卡。

Moreton Bay RAStel 多功能调制调器卡 <http://www.moreton.com.au/linux.htm> 查看 Linux 驱动程序。

- 20. 打印机/绘图仪

- 21. 扫描仪

- 22. 其他硬件

- 23. 相关信息来源

Cameron Spitzer 的硬件 FAQ 存档 (?? <http://ftp.rahul.net/pub/cameron/PC-info/>)

计算机厂商导指南 <http://guide.sbanetweb.com/>

系统优化信息 <http://www.dfw.net/-sdw/>

- 24. 致谢

感谢所有其他 HOWTO 的作者和贡献者；这里的许多内容都是理颜无耻地借用了他们的作品；感谢 FRIC、Zane Healy 和 Ed Carp，本 HOWTO 的原始作者；感谢所有提供更新和反馈的人。特别感谢 Eric Boerner 和 lilo（那个人，不是程序）提供的“sanity检查”。感谢 Dan Quinlinan 提供的原始 SGML 转换。

25. 附录 A。XFree86 3.3.1 支持的 S3 卡。

注意：对于 VIRGE/VX, DX, GX2 芯片组，你需要 XFree86 3.3.1。你应该使用 XF86_SVGA 服务器。

26. 附录 B。支持的 PCMCIA 卡

27. 附录 C。即插即用设备

28. 附录 D。Linux 不兼容驱动器

29. 词汇表

# 请记住...

如果你专门为了给 Linux 系统购买硬件，有几点需要记住：

- 避免专有产品，例如非 SCSI 或非 IDE 的 CD-ROM 驱动器。
- 包装上写着“需要 Windows”的硬件。
- Winmodems（软调制调器）。Winmodems 是通过专有接口在系统处理处理的调制调器。由于这些接口通常不公布，Linux 不支持这些设备。
- 未列在硬件兼容性列表上的硬件。虽然硬件兼容性列表中未明确提到的某些硬件可以在 Linux 上运行，但你应该在购买前进行研究。询问制造商或其他运行 Linux 的人。
- Intel 及其兼容机。

# 46 第I章：规划

- 硬件兼容性列表。
- 应该避免的内容。
- 参考来源。
- 安装与配置。

# 参考来源

使用 Linux 经常被提及的原因之一是其强大的支持基础。如果你遇到问题、想询问某些硬件是否受支持，或者只需要 Linux 信息，这里是一些资源：

- 手页 `man` pages：在 Linux 提示符下使用 `man` 命令可以获得 Linux 命令和库的帮助。例如，要获取 `ls` 命令的用法，请在命令提示符输入 `man ls`。要获取使用 `man` 命令的帮助，输入 `man man`。
- 软件包文档：许多 Red Hat 包将其文档存储在 `/usr/doc/` 中。
- HOWTO 和 FAQ：它们分别位于 `/usr/doc/HOWTO` 和 `/usr/doc/FAQ`。
- `info` 命令将提供系统上许多命令的超文本信息。
- Linux 文档项目 `LDP` 位于网络上的 http://www.linuxdoc.org。
- 红帽知识库：http://www.redhat.com/knowledgebase。
- Usenet 新闻组
- 红帽邮件邮件列表：http://www.redhat.com/community/list_subscribe.html。
- 自由软件基金会：http://www.gnu.org。
- 开源社区：http://www.opensource.org。

# 认证总结

本章涵盖了开源与自由软件之间的区别与联系，它们构成了大多数 Linux 发行版。我们介绍了让 Linux 可可行运行环境的特性，例如抢占式多任务处理和内存管理。我们还介绍了 UNIX 背后的历史以及推动它的社区。涵盖并比较了两个主要的许可证：通用公共许可证 `GPL` 和开源定义。

还涵盖了网络支持和硬件兼容性。最后，我们介绍了 Red Hat Linux 安装的不同类型以及它们各自的优缺点。

## 两分钟演练

- Linux 是一种现代、灵活且成熟的操作系统。尽管它起始于 Intel 平台，但之后移植到了许多其他平台，如 Amiga、DEC Alpha、Apple Power PC、Sun 工作站等。
- 所有 Linux 发行版都基于同一个理念：获取 Linux 内核并用免费软件围绕它，创建一个可用的操作系统。Red Hat Linux 是 Red Hat Software 的最新发行版，也不例外。
- 虽然 Linux 的历史可以追溯到 1991 年，但它的遗产可以追溯得更远。1969 年，贝尔实验室的一位程序员 Ken Thompson 发明了 UNIX 操作系统。大约同一时间，另一位程序员 Dennis Ritchie 发明了 C 语言。Linux 的遗产源于 UNIX 和 C 的结合。“Free software”（自由软件）通常是指在通用公共许可证下发布的软件。由于 UNIX，他们用 C 语言重写了。

# 48 第I章：规划

如果你专门为了给 Linux 系统购买硬件，有几点需要记住：

- 避免专有产品，例如非 SCSI 或非 IDE 的 CD-ROM 驱动器。
- 包装上写着“需要 Windows”的硬件。
- Winmodems（软调制调器）。Winmodems 是通过专有接口在系统处理处理的调制调器。由于这些接口通常不公布，Linux 不支持这些设备。
- 未列在硬件兼容性列表上的硬件。虽然硬件兼容性列表中未明确提到的某些硬件可以在 Linux 上运行，但你应该在购买前进行研究。询问制造商或其他运行 Linux 的人。
- Intel 及其兼容机。

在开始 Linux 安装之前，你需要知道机器的用途。它是作为开发工作站？还是 FTP 服务器？还是数据库服务器？在 Intel 计算机上安装非常简单。完整的硬件兼容性列表在 Red Linux 光盘上，或在 `/usr/doc/HOWTO` 中。

## 自测

以下自测题将帮助你衡量对本章内容的理解。请仔细阅读所有选项，因为可能有多个正确答案。为每个问题选择所有正确答案。

- 5. Linux 使用什么类型的内核？
- 1. 虽然最初打算运行在 Intel 平台，但它已移植到哪些其他平台？

  A. 静态

  B. 微内核

  C. 分布式

  D. 单内核

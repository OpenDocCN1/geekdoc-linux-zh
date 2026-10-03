
## /usr/src/linux/CREDITS

![](img/3e9d313887e2c1cabeb5043769cbf08f_11_0.png)

2003年在加拿大安大略省举行的内核开发者峰会上的Linux内核黑客，由Richard Guy Briggs拍摄并由Robert Love提交。

## milter-sender:

www.snert.com/Software/milter-sender

milter-sender是Sendmail milter插件，在接收邮件时可回连到邮件发送者。基本上，如果发送者在其声称的主要邮件服务器上不存在，则该邮件几乎肯定是垃圾邮件并将被拒绝。该插件显著减少了我的垃圾邮件。而且，虽然军备竞赛尚未结束，但我始终可以添加更多milter插件。我现在通过milter运行milter-sender和SpamAssassin。需要：Berkeley DB、带milter的Sendmail、libsnert和glibc。

> —DAVID A. BANDEL

## LJ 索引—2004年1月

- 1. 2002年至2003年9月中旬开发中的Linux 2.6内核的更改次数：12,479
- 2. 内核中的合并次数，不计入代理应用补丁：2,386
- 3. 每日合并的近似平均次数：9
- 4. 参与内核开发的个人开发者数量：554
- 5. 内核开发者前10%完成的所有更改的百分比：78
- 6. 内核开发者前20%完成的所有更改的百分比：90
- 7. 2002年Linux在付费服务器操作系统环境（SOE）类别中的占比：23.1
- 8. 2002年微软在付费SOE类别中的占比：55.1
- 9. 2002年SOE环境中出货的新许可证数（百万）：5.7
- 10. 2002年Linux在客户端操作系统环境（COE）类别中的份额占比：2.8
- 11. 2002年Macintosh在COE类别中的份额占比：2.9
- 12. 2002年其他操作系统在COE类别中的份额占比：0.5
- 13. 2002年微软在COE类别中的份额占比：93.8
- 14. 2002年除Linux和Windows外收入增长的操作系统数量：0

## Sources

1–6：Linus Torvalds

7–14：International Data Corp.

## They Said It

> 有很多关于企鹅的原因。我被企鹅咬过。这是一个真实的故事。有趣的是，关于企鹅的网站有很多。有《Tux的历史》(www.sjbaker.org/tux)之类的。有些网站也有我的解释。它们几乎都说，“这是一个很棒的故事，但不是真的。”——我被企鹅咬了。

这是真的！我被企鹅咬了！

> 我的意思是，真的！听我的！我受伤了！

好吧，所以他不是六英尺高。

—LINUS TORVALDS，摘自他在2003年9月Linux Lunacy极客巡航上的演讲

> 我们在迁移到Linux方面非常积极；目标是不购买新的UNIX设备……直到一年前，大多数主流应用都在UNIX上。后勤系统在大型机上，但其他一切都在Sun上。

—LEHMAN BROTHERS CIO EMEA RUSSELL (www.cbronline.com/magazine/2d7f2e75fecd8bbfc2256d7800317032)

> 任何涉及Linux的东西。

—GAP CORP. CIO KEN HARRIS，关于其公司技术项目优先事项 (asia.cnet.com/newstech/systems/0,39001153,39154483,00.htm)

## Linux On Demand

您决定...每块板上都准备好Linux

### IanPMC-4Gx

![](img/3e9d313887e2c1cabeb5043769cbf08f_12_0.png)

### 四端口千兆以太网铜缆或光纤 PMC 适配器

- 2 或 4 个自动协商的 10/100/1000 以太网端口
- 光纤版本支持长距离和短距离
- 铜缆版本自动检测速度、单工/全双工、流控制以及极性和电缆长度检测

### wanADAPT-C4T1E1

![](img/3e9d313887e2c1cabeb5043769cbf08f_12_1.png)

### 通道化四端口 T1/E1/J1 PCI WAN 适配器

- 128 个通道（DS0）
- 从 DSX 到 DS1 的线路构建
- 支持 D4、SF、ESF、SLC-96、JT-6704 帧格式
- 可选时钟选项

### HW400c/M DKL

![](img/3e9d313887e2c1cabeb5043769cbf08f_12_2.png)

### 具有双 PTMC 站点的 6U CPCI 处理刀片

- 333 MHz PowerPC CPU
- 启用 PICMG 2.16 分组交换背板
- 双 10/100 以太网端口
- 包含 TimeSys Linux GPL 软件开发工具包
- 适用于 T1/E1、T3/E3、HSSI、V.35、X.21 及其他 SBE PMC 的驱动程序

## SBE®

WAN • LAN • 存储 • 运营商 • 定制

按需灵活性 | 925-355-2000 | info@sbei.com | www.sbei.com

## diff -u：内核开发的新变化

Intel已发布了一些事件通知补丁，除了进程创建时已有的钩子外，还在进程终止时提供分析钩子。Intel的工作应有助于增强Oprofile、Perfmon和VTune等分析工具。尽管添加此类钩子可能为专有软件供应商绕过GPL许可限制提供途径，但似乎Intel的工作并不存在该问题。Frederic Rossi也在从事自己无关的事件通知代码，即异步事件机制（AEM）。AEM允许通用用户空间应用程序通过提供自己的事件处理程序集来注册系统事件[LJ，2003年7月]。其主要目标是能够快速地将数据从内核传递回用户空间。虽然Intel和AEM的工作没有直接关系，但它们揭示了Linux开发中系统各层之间通信日益增强的有趣趋势。

DSI开发团队制作了一个独立模块，名为digsig，在运行可执行程序之前检查其嵌入的数字签名。如果文件被修改，digsig会阻止其调用。各种各样的应用都可以使用它——从蠕虫保护到数字版权管理。与可信计算的证明功能不同，digsig的验证过程仍由机器所有者控制。例如，远程系统无法依赖您系统上的digsig模块来验证您的计算机是否正在运行那些远程系统批准的特定版本的特定软件。

显然，所有AMD Athlon处理器都存在一个错误，在某些条件下会导致预取指令对某些地址产生内存管理故障。这与臭名昭著的f00f Pentium错误类似，因为两者都是硬件本身的错误，操作系统只能绕过。好消息是，在大多数情况下，该错误不会造成任何实际损害。触发该错误的情况很少，这可能解释了为什么它长期未被发现。Andi Kleen一直在为2.4和2.6开发Linux变通方法，而AMD方面已确认他的变通方法将与硬件中已修正该错误的未来Athlon向前兼容。然而，据Andi称，一些Athlon，包括K7，可能永远不会被修复，因此他的变通方法可能需要在新系统上使用很长时间。

SGI已发布其Altix串行控制台的GPL驱动程序，但在版权声明中，SGI明确保留了该代码中使用的任何专利的权利。虽然自由软件基金会已向SGI确认这在技术上并不违反GPL，但它可能导致一种情况，即来自GPL项目（如内核）的代码不被允许用于其他GPL项目。那么问题就来了，在这种条件下，代码是否应被允许进入内核？Alan Cox决定与SGI和FSF一起调查此事，以确认FSF确实不认为这违反GPL，并查看SGI是否愿意修改其立场。

Chris Rivera和Robert Love发布了slabtop独立实用程序，这是一个用于监控缓存中内存分配和释放的工具。内核维护一个分配内存的缓存，根据需要将其分配给进程。但有时需要释放这部分内存，而slab就是实现这种释放的方式。slabtop工具监控每个slab缓存，实时呈现该slab的数据，并同时更新系统上所有slab活动的一组全局统计信息。

Matthew Wilcox开始将内核头文件分为两类，即应对用户空间源可见的头文件和不应可见的头文件。当用户应用程序依赖错误的内核头文件时总是一个问题。随着内核的增长和变化，头文件也可能发生变化，用户软件可能会中断。为此，必须保持严格的分离。Matthew的工作使这变得更容易。他还成功地激励了其他人，如Erik Andersen，开始清理一些类型命名约定，为2.6做准备。

已启动一种新的内核代码划分方式，与arch/目录类似。但与按架构划分代码不同，新划分按编译器划分。自从Intel的ecc编译器成为继GCC之后第二个能够成功构建Linux内核的编译器以来，出现了细微的冲突，导致开发人员开始提交专门处理一个编译器或另一个编译器特殊性的补丁。在最近关于内联汇编支持的争论之后，GCC支持但ecc不支持，Linus Torvalds决定创建按编译器划分的目录来容纳与特定编译器相关的所有补丁。Sam Ravnborg和David Mosberger似乎决定领导该工作，他们已经提交了补丁以启动过渡。

—ZACK BROWN

## They Said It

找到既不发火、冷静理性、又有品味的人非常非常困难。我的意思是……给我一个诚实的人。这……不太发生。同时，当它发生时，意义很大。只是少数几个人就能产生巨大差异。

> —LINUS TORVALDS, ALSO FROM HIS TALK ON THE LINUX LUNACY GEEK CRUISE

在早期，Linux在首席信息官（CIO）不知情的情况下被采用。这是针对文件和打印服务器等事物的技术决策，成本或可靠性是驱动因素。现在我们有了CIO的采用。

> —ADAM JOLLANS, IBM WORLDWIDE LINUX SOFTWARE MARKETING STRATEGY MANAGER (www.vnunet.com/News/1144291)

计算尺是一种精密仪器。好的计算尺会很耐用，事实上，如果不滥用，可以使用一生。如果你想确保物有所值，就必须提前10、20、30甚至40年考虑。

> —“HOW TO CHOOSE A SLIDE RULE” BY DON HEROLD (1940 KEUFFEL & ESSER CO. BROCHURE POSTED ON mccoys-kecatalogs.com)

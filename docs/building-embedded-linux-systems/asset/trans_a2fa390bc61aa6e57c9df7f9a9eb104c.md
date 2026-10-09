
## 行业

在认识到 Linux 在嵌入式市场中的潜力后，许多公司开始拥抱并推广该领域的 Linux。行业参与者至关重要，因为他们是推动 Linux 作为最终用户产品的主力。通常，他们是第一个收到来自这些最终用户反馈的人。虽然各种邮件列表上的帖子可以告诉开发者软件是如何被使用的，但并非所有用户都会参与这些邮件列表。因此，供应商必须在协助用户和促进构成 Linux 的各个项目开发之间取得平衡，同时避免陷入试图将开发方向引向自身利益的陷阱。在这方面，许多供应商已成功在嵌入式 Linux 市场中确立了自己的地位。

以下是一些较知名的供应商。

![](img/617fee0f2d5cdaf31b3f8601bc6c454f_36_0.png)

> 此处列出的供应商仅用于讨论目的。作者和出版商均未评估本书中这些供应商提供的任何服务，因此不应将该列表解读为任何形式的认可。

### MontaVista

MontaVista 由嵌入式行业资深人士 Jim Ready 创立，并以他当时居住城镇的一部分命名。通过其产品和服务以及 Linux 在工业应用中的推广，MontaVista 将自己定位为嵌入式 Linux 市场的领导者。它生产各种带有 MontaVista 名称的产品，包括“Professional”、“Carrier Grade”和“Mobile”等变体。MontaVista 对一些开源项目做出了贡献，包括内核调度器增强和实时扩展、ViewML、Micro-windows 以及 Linux 跟踪工具包（LTT）。由于从 2.4 内核过渡到 2.6 内核稍晚，MontaVista 通过成为首家提供带有 Linux 内核实时补丁产品的嵌入式供应商来弥补这一点（这不是 RTLinux；请参见第 14 章）。它还提出了各种能力主张，并在手机市场取得了相当大的成功，特别是摩托罗拉基于其 MontaVista MobilLinux 产品构建了整个产品系列。

MontaVista 在一定程度上因作为嵌入式 Linux 革命的典范而遭受了一些困扰。它目睹了许多工程师分拆出去并创建较小的咨询公司——Embedded Alley 就是一个典型的例子，由一群极具知识的 former MontaVista 员工创立——以及随着他们决定市场将把他们带向何方而发生的公司方向变化。MontaVista 不维护其社区代码贡献的公开存储库（显然它有参与上游项目开发的开发者），但它确实拥有 *http://source.mvista.com/* 网站，提供了一些关于项目（如其实时计划）的公开信息。MontaVista 的主要网站位于 *http://www.mvista.com*。

### Wind River

作为嵌入式 Linux 领域的相对后来者，Wind River 拥有作为专有实时操作系统 vxworks 作者的历史。这意味着它背后拥有庞大的客户群，范围从机顶盒供应商到汽车公司，再到“深度嵌入式”应用（一些 Linux 不适用的非常小型系统），以及 NASA 发射的火星探测机器人。在试探市场多年后，Wind River 最终决定放手一搏，发布了一款基于 Eclipse 的开发产品，支持以 vxworks 或 Linux 为目标（这对现有的 vxworks 开发者来说是一个伟大的迁移工具）。Wind River Linux 中心包含各种下载和信息，包括其致力于“设备软件优化”（DSO）的更多细节，DSO 是一个它最近帮助确立的术语。通常，这是指嵌入式操作系统（如 Linux）不仅仅是其（自由软件）组件的总和，而是需要精心调整和知识才能在给定的嵌入式产品中发挥作用的系统。

Wind 最近从 FSM Labs 收购了 RTLinux 技术，因此预计当你读到本文时，它将拥有多种实时 Linux 产品系列。你可以在 [http://www.windriver.com](http://www.windriver.com) 上了解更多关于 Wind River 的信息。

### LynuxWorks

该公司以前称为 Lynx 实时系统（Lynx Real-Time Systems），是另一家传统嵌入式操作系统供应商。与其他传统嵌入式操作系统提供商相反，Lynx 很早就决定拥抱 Linux，并更改其名称以反映这一决定。加上后来 Wind River¹ 收购 BSDi 以及 QNX 决定免费供人下载其操作系统，这表明开源（尤其是 Linux）在嵌入式领域正取得重大进展。话虽如此，LynuxWorks 仍然开发、分发和支持 Linux 操作系统。事实上，LynuxWorks 推广了一种开发解决方案。根据 LynuxWorks 的说法，需要硬实时性能的程序员应继续使用 Lynx，而那些希望使用开源解决方案的人应使用 BlueCat，即其嵌入式 Linux 发行版（确实，过去曾因使用类似反 GPL 的策略来倡导使用 Lynx 操作系统而非 Linux 而招致一些批评）。LynuxWorks 甚至修改了其 Lynx 操作系统，以便未修改的 Linux 二进制文件可以原样运行。LynuxWorks 作为一家成功的嵌入式操作系统供应商这一事实及其早期采用 Linux 的事实，证实了嵌入式市场向开源操作系统转变的重要性。

> ¹ Wind River 后来改变了主意，其与 BSD 的关系似乎已成为过去式。

### Timesys

Timesys 已从生产单一的一刀切嵌入式 Linux 发行版转向软件服务模式（类似 DSO），专注于定制构建的、基于 Web 的、交叉编译的包，以满足各种需求。其 LinuxLink 订阅服务旨在为定制所需的软件选择提供简单的在线体验，自动为广泛的构建目标进行构建，并提供可在目标设备上使用的软件包。它声称通过脚本化和自动化即时构建定制发行版的过程，可以消除查找补丁、版本和依赖关系的不确定性和麻烦。你可以在 [http://www.timesys.com/](http://www.timesys.com/) 上了解更多。

还有许多较小的参与者（并且数量不断增多），他们为嵌入式设备应用提供围绕开源和自由软件的各种服务。事实上，许多开源和自由软件贡献是由独立人士或为小型供应商工作的个人做出的。因此，这些小型参与者提供的服务往往与较大参与者提供的服务持平，有时甚至超越。例如，Wolfgang Denk 的 DENX 软件是一家位于德国慕尼黑附近的小型咨询公司，但嵌入式 Linux 领域的几乎所有人都听说过 Wolfgang、他的 Das U-Boot 固件或其公司免费嵌入式 Linux 开发工具包（ELDK）中提供的详尽文档。部分得益于本书的第一版，大量嵌入式 Linux 开发者也知道 Karim Yaghnour 及其 Opersys 咨询公司。

## 资源

大多数开发者通过各种资源网站和出版物进入嵌入式 Linux 世界。正是通过这些网站和出版物，Linux 开发社区、行业和机构宣传其工作并了解其他参与者的工作。本质上，资源网站和出版物是所有关注嵌入式 Linux 的人们的聚会场所。有两种资源尤为突出：LinuxDevices.com 和 *Linux Journal* 等杂志。

LinuxDevices.com 由 Rick Lehrbaum（与 MontaVista 的创始人之一有关联）于 1999 年万圣节¹创立。LinuxDevices.com 设有新闻条目、文章、投票、论坛以及与嵌入式 Linux 相关的许多其他链接。虽然其职业属性显然是商业性的，但我们绝对建议偶尔查看该网站，以了解嵌入式 Linux 的最新动态（并且凭借其每周电子邮件新闻稿，这很容易做到）。除此之外，LinuxDevices.com 在启动嵌入式 Linux 联盟（Embedded Linux Consortium）中发挥了重要作用。

*随着对嵌入式系统中使用 Linux 的兴趣日益增长，嵌入式 Linux 期刊（ELJ）由 *Linux Journal*（LJ）的所有者 Specialized System Consultants 于 2001 年 1 月推出，旨在服务于嵌入式 Linux 社区，但后来停刊。虽然 ELJ 不再作为单独的杂志出版，但它在鼓励其他 Linux 杂志参与方面发挥了重要作用。有几*

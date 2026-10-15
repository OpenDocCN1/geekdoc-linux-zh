
- 我们在 Digital Press/Butterworth-Heinemann 的联系人 Pam Chester；新汉布郡大学计算与信息服务部的 Bill Costa，他为我们提供了详尽的评审意见，并为我们提供了访问他自己关于 UNIX 和 OpenVMS 迁移优秀网站的权限；额外感谢 Tim 对 Perl 以及整个第 10 章提供的大量帮助；
- 所有曾在 DEC 和 Compaq 工作过的 Linux 倡导者、爱好者和传教士（你们知道你们指的是谁！）；
- 特别感谢 ngh，真正的大导师；
- 当然，还有我们的家人。

Richard Holstein 和 Joseph McMullen

2003年4月

## 章节插图

章节图由 Maria Ruotolo 绘制，改编自一些伟大的大师作品：

1. 选自奥古斯塔·罗丹（1840-1917）的《思想者》。
2. 改自米开朗基罗（1475-1519）的《人类的创造》。
3. 改自毕加索（1881-1973）的《恋人》。
4. 改自《床前的年轻女子》（Jeune Femme Devant le Lit）。
5. 改自毕加索的《爱人》。
6. 改自《春天的午宴》。
7. 改自《苏丹的访问》。
8. 改自凡·高的《肖像》。
9. 改自《奥斯曼肖像》。
10. 改自《医学解剖课》。
11. 改自伦勃特的《割地的妇女》。
12. 改自莫奈《劳动者》。
13. 改自达芬奇的《最后的晚餐》。

## 序言

## I 引言

与 OpenVMS 不同，UNIX 对大写和小写字符的处理方式不同。

本书旨在介绍 UNIX 操作系统，假设你预先了解 OpenVMS...

## I 演进

与 OpenVMS 不同，UNIX 不是一个单一的产品……

### I.I 演变

关于 UNIX 的演进以及当前向标准化的趋势，已有大量论述。本节仅提供一个简要的概述，并将 UNIX 的演进与 OpenVMS 的相应开发进行对比。

第一版本的 UNIX 用汇编语言编写的，包含了 Multics 的许多特征。

决定用高级别语言重写 UNIX 从而使其在不同计算机系统间具有可移植性，是在 1972 年，当时 Thompson 使用一种名为 `B` 的语言重写了 UNIX。同样位于实验室的 Dennis Ritchie 在 1973 年对 `B` 进行了大量修改，并将其命名为 `C`。无论是否偶然，使 UNIX 可移植的决定是今天 UNIX 流行的主要原因。

1974 年，将 UNIX 许可给大学的决定建立了第二条主要的演进路径——伯克利软件发行版（BSD）。1979 年发布的 BSD 版本 3.0 对原始实验室版本的 UNIX 进行了许多增强，其中一些我们将在后续章节中讨论。值得注意的是有几种可移植的语言编译器，它们扩展了不同类型硬件上的透明操作系统功能，包含了透明的程序开发工具。BSD 的开发说明了其一个方面。

![](img/e259ba2750941fa3d146eda78c65e89d_8_0.png)

UNIX 的原始设计哲学：系统是模块化的；也就是说，它可以相对容易地扩展额外功能。

在大约 BSD 发布期间，第一个版本的 UNIX 在 VAX 计算机上出现。它被称为 32V，代表了贝尔实验室 16 位第 7 版（Version 7）的 32 位实现，而该版本已经在多台 PDP-11 系列计算机上运行。

随着反垄断法律的放宽以及一系列微型和小型计算机系统的发布，AT&T 发现自己比以前更有优势来激进地向市场推广 UNIX。1983 年，AT&T 发布了 UNIX System V，它包含了许多 BSD 特性。

1984 年，数字设备公司（Digital 或 DEC）发布了 ULTRIX，这是一个源自 BSD 和 System V 的 UNIX 版本。ULTRIX 逐渐支持完整的 VAX 和 MIPS 处理器线。对于个人电脑市场，微软公司开发了 Xenix，这是基于 UNIX System V 的 16 位微机版本。与此同时，国际商业机器（IBM）为了应对市场压力，一直在不同的硬件平台上静静地支持多个不同的 UNIX 版本，但没有任何显见的整体公司战略。随着 1986 年为 IBM RT 引入高级交互执行系统（AIX），IBM 的立场发生了变化。AIX 是 IBM 内部的 UNIX 标准，目前它可以在各种 IBM 处理器上运行。其他主要的 UNIX 版本还包括 Sun Microsystems 的 SunOS 和 Solaris，以及惠普的 HP-UX。

随着各企业采用并增强 UNIX 以创建自己的专有商业版本，出现了一种来自自发的反响，即为开发者（特别是教育机构）维护“自由软件”的概念。MIT 人工智能实验室的 Richard Stallman 在 20 世纪 80 年代初启动了 GNU 项目。GNU 项目的主要目标之一是创建一个自由操作系统。这个新操作系统将在 UNIX 已经提供的技术基础上构建。为了强调其独特性，选择了 GNU 作为一个“GNU's Not UNIX”（GNU 不是 UNIX）的缩写。GNU 项目开发的一些重要早期软件包括 GNU C 编译器（GCC）和 GNU Emacs 编辑器。

GNU 项目在 20 世纪 90 年代继续进展，重点开发内核。与此同时，芬兰学生 Linus Torvalds 创建了 Linux，这是他自己的非专有操作系统版本。Torvalds 在 1991 年在“网上”发布了 Linux。随着开发者下载和测试 Linux，这个新操作系统迅速流行起来。不久后，Linux 在 GNU 通用公共许可协议下授权，确保源代码对所有人免费供复制和修改。GNU/Linux（在本书随后的所有引用中简称为“Linux”）是一种可以从互联网网站、大学和其他来源免费获取的开源软件。它也可以通过 Red Hat、Caldera、Debian 和 SUSE 等公司进行商业销售，这些公司将基础 Linux 发行版与它们自己的工具和实用程序打包在一起。

Linux 被认为是一个运行在各种处理器（包括英特尔处理器）上的完全独特的操作系统。Linux 基于 UNIX，它的许多命令、外壳、文件系统和实用程序与许多标准 UNIX 实现中的几乎完全相同。因此，在书中，我们将 Linux 视为 UNIX 的另一种实现。有关 Linux 的更多信息，请参阅附录 E 中的参考资料。

当 Linux 在 20 世纪 90 年代兴起时，UNIX 继续进入企业“级”计算领域。随着互联网的发展，UNIX 证明自己是 Web 服务器的可靠平台。不仅技术得到了改进（UNIX 运行在更快的处理器上），而且行业标准的重要性也让各种 UNIX 实现变得更加开放。

Digital 在 1992 年引入了其 Alpha 计算机架构。Alpha 计算机拥有当时最快的芯片，是第一个支持 64 位计算的商业架构。Digital 在 Alpha 上引入了对 OpenVMS 的支持，并为 Digital 计算机引入了 64 位 UNIX，即 DEC OSF/1。Digital 后来将其 Alpha 的 UNIX 产品从 DEC OSF/1 改名为 DIGITAL UNIX，随后改为 Tru64 UNIX。Digital 以其 OpenVMS 和 UNIX 系统赢得了卓越声誉；然而，像许多其他高科技公司一样，Digital 在 20 世纪 90 年代中期陷入了困境。作为不断变化的商业计算市场的受害者，Digital 在 1998 年被康贝计算机（Compaq）收购。Compaq 扩展了 OpenVMS 和 Tru64 UNIX 的开发。几年后，HP 收购了 Compaq。2002 年，HP 计划将 OpenVMS 的开发从 Alpha 移到 Intel IA-64。使用高级语言而非汇编语言编写 UNIX 的决定，使得一小部分处理输入/输出的汇编代码被解耦。

![](img/e259ba2750941fa3d146eda78c65e89d_10_0.png)

各个联盟的自愿合规性了 UNIX 的“开放性”：

表 1.1 流行的 UNIX 版本

| 名称 | 公司 |
| :--- | :--- |
| 32V | AT&T |
| UNIX System V | AT&T |
| ULTRIX | Digital Equipment Corporation (DEC) |
| Xenix | Microsoft Corporation |
| AIX | IBM |
| SunOS / Solaris | Sun Microsystems |
| HP-UX | Hewlett-Packard |
| OpenVMS | Digital Equipment Corporation (DEC) |
| DEC OSF/1 / DIGITAL UNIX / Tru64 UNIX | Digital Equipment Corporation (DEC) |
| AIX | IBM |

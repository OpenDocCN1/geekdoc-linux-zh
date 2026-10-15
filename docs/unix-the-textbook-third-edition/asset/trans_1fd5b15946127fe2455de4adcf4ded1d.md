

3. 系统的设计允许用户并发运行多个进程，并通过 IPC 通道连接这些进程，包括管道、FIFO 和套接字，如第 1.7.2 节所述。我们将在第 9 章介绍该设计方面的实现。

## 1.8.3 AT&T System V

为应对 20 世纪 80 年代初不断变化的商业环境，贝尔实验室/AT&T 将 UNIX 的后续版本许可为 System III，最终在 1983 年起以 System V 发布。UNIX 的这一主分支继续发展，如图 1.3 所示，直至 System V 第 4 版（SVR4），随后在 20 世纪 90 年代中期至后期再次分化并演变为 SCO UNIX 而得以延续。目前，有四个主要基于 System V 的 UNIX 系统：AIX 7.x、OpenServer 6.x、UnixWare 7.x、Solaris 11.x、OpenSolaris 及其变种，以及 HP-UX 11i v3。

## 1.8.4 Berkeley Software Distributions

加州大学伯克利分校在 20 世纪 80 年代至 90 年代期间在其第二主分支上启动并维护了 UNIX 的开发。合同协议使操作系统可免费提供给大学，因此这些版本在很大程度上促进了 UNIX 的普及。这些版本作为伯克利软件发行版（BSD）发布，分别为 3BSD 和 4BSD-4.4BSD。最近，BSD UNIX 以 FreeBSD 及其分支 PC-BSD、OpenBSD 和 NetBSD 的形式存续。今天，BSD UNIX 最流行的变种是 FreeBSD 10.x、OpenBSD 5.x、NetBSD 6.x 和 Mac OS X 10.9.x（Darwin）。

在本书中，我们主要在 PC-BSD 下展示示例命令。在适当的情况下，我们还讨论 Solaris 的特性。

## 1.8.5 History of Shells

Shell 作为 UNIX 实用程序的发展与系统本身的发展并行。Steven R. Bourne 编写了第一个商业可用的 shell，即 Bourne shell。它在 1979 年的第七版中提供，是许多 System V 版本的默认 shell。C shell 由 Bill Joy 在 20 世纪 70 年代末主要编写，并在 2BSD 中很快提供。引入时，它为编写 shell 脚本提供了类似 C 程序的编程接口。在 C shell 发展之后，Korn shell 于 1986 年在 SVR4 中正式引入。由贝尔实验室的 David Korn 编写，它包含 Bourne shell 命令的超集，但功能更强。它还包含 C shell 的一些有用特性。我们将在第 2 章中更详细地讨论 UNIX shell 的发展历史。

三个主要 shell 具有略有不同的特性和命令集。在本教材中，我们讨论所有 UNIX shell 和版本共有的特性和命令集。每当我们讨论特定于某个 shell 或版本的特性或命令时，我们会明确说明。

## 1.8.6 Current and Future Developments

对于除 Solaris 和 FreeBSD 之外的所有其他 UNIX 变种来说，最令人兴奋和最具挑战性的当前 UNIX 开发可能集中于将 ZFS 纳入内核，并让启动磁盘使用 ZFS。ZFS 由 Sun Microsystems 在 2006 年将其纳入 Solaris 系列之前几年开发。它现在仅是 Solaris（及其非商业等价物 OpenIndiana）和 FreeBSD（及其分支 PC-BSD）的标准文件系统。自 Sun 被 Oracle 收购以来，ZFS 的源代码开发基本上沿着两个分支进行：Oracle Solaris 分支和开放分支。

UNIX 系统未来面临的另一个主要挑战是将 systemd 纳入内核。目前，systemd 是一套系统管理守护进程、库和实用程序，旨在作为 Linux 的中央管理和配置平台。systemd 用于当前 Linux 内核的大多数当前实现和官方发行版中。它是 Linux 的 init 系统（由 Linux 内核在 Linux 启动过程中调用以初始化用户空间并在之后管理所有进程的过程），从而取代了 UNIX System V 和 BSD 风格的 init 守护进程。名称 systemd 遵循了使守护进程更容易区分的惯例，即文件名以字母 d 结尾。systemd 是否会被纳入 UNIX 内核还有待观察。

最后，用各种其他软件系统取代 X Window System 协议有望带来更小、更有效的 GUI 系统。Wayland 是一种协议，规定了显示服务器（称为 Wayland compositor）与其客户端之间的通信，以及该协议的 C 语言参考实现。

## 1.9 VARIATIONS IN UNIX SYSTEMS

如图所示 1.3 所示，UNIX 系统的开发从单一核心沿着三个主分支进行。分支的分歧和相似之处在很大程度上是由 20 世纪 70 年代和 80 年代贝尔实验室和 AT&T 的法律许可安排造成的。分歧的主要优势是每个分支都拥有命令和功能丰富的操作系统。早期的贝尔实验室版本作为源代码被自由复制和分发，学术和商业用户可以轻松修改以适应其硬件和软件。这种改编导致操作系统各个方面演进方式的激增。即使是 System V 和 BSD 的后期版本，也可以通过操作系统版本供应商提供的便利进行轻松修改，即使源代码不可用。许多后期版本是兼容性版本，旨在在特定实现与其 perceived 竞争对手之间提供统一性。这些兼容性版本及其分支的重要贡献是提供了一定程度的同质性，无论您使用的是 SVR4、Solaris、4.4BSD、Linux 还是 Apple OS X 的现代衍生产品。

分歧的缺点是，在一个版本上运行的程序甚至命令在另一个版本上无法运行，从而削弱了系统本身固有的用户友好性优势。人们曾尝试标准化 UNIX——例如通过 IEEE 可移植操作系统接口（POSIX）。该软件标准不仅涵盖 UNIX，而且特别规定了程序操作和用户界面，而将其实现留给开发者。已采用了多个标准，还有更多


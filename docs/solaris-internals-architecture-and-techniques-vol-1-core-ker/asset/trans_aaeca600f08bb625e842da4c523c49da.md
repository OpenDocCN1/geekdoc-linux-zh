
本文包含了上述内容。因此，我们强调了可以在 Solaris 系统上用于提取信息的方法和工具，这些信息通过标准的捆绑命令和工具无法轻易获取。我们希望说明如何根据你的工作或兴趣以有意义的方式应用这些知识。

为了提高本书的实用性，我们包含了关于 Solaris 2.5.1、2.6 和 Solaris 7 的特定信息。我们涵盖了 Solaris 子系统，包括内存管理、进程管理、线程和文件系统。我们没有涵盖低层 I/O、设备驱动程序、STREAMS 和网络的细节。有关这些主题的参考资料，请参见《编写设备驱动程序》[28]、《STREAMS编程指南》[29]以及《UNIX编程》[32]。书中包含的内容并不一定是以入门水平呈现，尽管在可能的情况下，我们在讨论某个话题时都会从概念背景开始。我们假设你对操作系统概念有一定了解，并使用过基于 UNIX 的操作系统。一些 C 语言的知识会有帮助，但并非必须。

由于运行 Solaris 的硬件平台多种多样，要讨论所有不同处理器和架构的低层细节是不切行的，因此在需要细节时，我们的硬件重点承认是以 UltraSPARC 为中心的。这种方法最有意义，因为它代表了当前的技术并针对了最大的安装量。通常情况下，在需要细节时提出的概念也适用于所支持的其他处理器和平台。区别在于具体的实现细节，例如每个处理器的硬件寄存器。

在整本书中，当我们在描述各种代码段时会引用特定的内核函数。这些例程是操作系统系统内部的，不应被解释为、或与作为 Solaris 产品线一部分交付的公共接口（系统调用和库接口）相淆。文中引用的函数除非另有说明，否则它们是内核私有的，应用程序无法调用，也无法以任何方式被程序使用。

## 目标读者

我们希望这本书能为从事 Solaris 操作系统环境的各种技术人员提供有用的参考。

- **应用开发人员**可以在书中找到关于 Solaris 如何在应用程序编程接口（API）背后实现功能的信息。这些信息帮助开发者在开发 Solaris 应用程序时理解每个接口的性能、可扩展性和实现细节。系统概述章节以及关于调度、进程间通信和文件系统行为的章节应该是最有用的部分。
- **设备驱动程序和内核模块开发者**（针对驱动程序、STREAMS 模块、可加载系统调用等）可以在这里找到 Solaris 操作系统的通用架构和实现理论。书中关于 Solaris 内核框架和设施的部分（特别是锁和同步原语章节）为为。
- **系统管理员**、系统分析师、数据库管理员以及负责性能调优和容量规划的 ERP 经理可以学习主要 Solaris 系统的特性。文件系统缓存和内存管理章节提供了大量关于 Solaris 在真实环境中如何运行的信息。Solaris 可调参数背后的算法（详见附录 A）在书中得到了深入介绍。
- 负责 Solaris 诊断、调试和支持的**技术支持人员**将在书中找到大量关于 Solaris 实现细节的丰富信息。每一章都提供了主要的数据结构和数据流图，以辅助 Solaris 系统的调试和导航。
- 想了解更多 Solaris 内核如何工作的**系统用户**可以在每个章节的开头找到高层次概述。

除了列出的各种技术人员外，我们认为学术界的成员也会在研究单机生产内核如何实现主要子系统并解决操作系统开发中固有问题方面发现本书的价值。

## 本书结构

我们将《Solaris Internals》分为几个逻辑部分，每个部分将包含相关信息的多个章节分组在一起。我们的目标是为材料提供一种模块化的方法，让后续章节建立在早期章节提供的信息之上。然而，对于熟悉操作系统设计和实现某些方面的读者来说，各个部分和章节在主题涵盖上也可以独立存在。

- 第一部分：Solaris 内部原理
    - 第 1 章 — Solaris 简介
    - 第 2 章 — 内核服务
    - 第 3 章 — 内核同步原语
    - 第 4 章 内核引导与初始化
- 第二部分：Solaris 内存系统
    - 第 5 章 — Solaris 内存架构
    - 第 6 章 — 内核内存
    - 第 7 章 内存监控
- 第三部分：线程、进程与 IPC
    - 第 8 章 — Solaris 多线程进程架构
    - 第 9 章 — Solaris 内核调度器
    - 第 10 章 进程间通信
- 第四部分：文件与文件系统
    - 第 11 章 — Solaris 文件与文件 I/O
    - 第 12 章 — 文件系统概述
    - 第 13 章 — 文件系统框架
    - 第 14 章 — UNIX 文件系统
    - 第 15 章 — Solaris 文件系统缓存

## Solaris 源代码

2000年2月，Sun 宣布提供 Solaris 源代码。本书是 Solaris 源代码的重要伴侣，可以作为 Solaris 内核框架和架构的指南。还需要注意的是，Sun 提供的源码是 Solaris 8 源码。虽然本书涵盖了包括 Solaris 7 在内的版本，但几乎所有材料与 Solaris 8 相关。

## 更新与相关材料

为了补充本书，我们创建了一个网站，在其中我们将放置更新的材料、提到的工具以及所涵盖主题的相关材料链接。该网站地址为：

http://www.solarisinternals.com

我们将定期更新网站，发布有关本文的信息以及对《Solaris Internals》的未来工作。我们将在该 URL 发布 Solaris 7 和 8 之间的差异信息，发布当前版本可能出现的任何错误，并分享读者的反馈、评论和其他相关信息。

## 符号规范

表 P-1 描述了书中使用的排版规范，表 P-2 显示了我们描述的工具的默认系统提示符。

**表 P-1** 排版规范

| 字体或符号 | 含义 | 示例 |
| --- | --- | --- |
| AaBbCc123 | 命令名、文件名和数据结构 | `vmstat` 命令。`<sys/proc.h>` 头文件。`proc` 结构。 |
| AaBbCc123 () | 函数名。 | page_create_va() |
| AaBbCc123(2) | 手册页。 | 请查看 `vmstat(1M)`。 |
| AaBbCc123 | 在示例中输入的命令。 | $ vmstat swap free re mf 0 0 |
| AaBbCc123 | 引入时的新术语* | 当发生主页缺页时…… |

**表 P-2** 命令提示符

| Shell | 提示符 |
| --- | --- |
| C shell 提示符 | machine_name% |
| C 超用户提示符 | machine_name# |
| Bourne 和 Korn shell 提示符 | $ |
| Bourne 和 Korn shell 超用户提示符 | # |
| crash 工具提示符 | crash > |

 作者寄语

我们希望读者从阅读《Solaris Internals》中获得的收获与我们编写它时一样多。我们欢迎读者的意见、建议和问题。

## 谢谢

很难感谢所有帮助我们完成这本书的人。至少我们要感谢：

- 感谢 Brian Wang、Adrian Cockcroft、Paul Strong、Lisa Musgrave 和 Fraser Gardiner 在本书结构和内容方面提供的帮助和建议。
- 感谢 Tony Shoumack、Phil Harman、Jim Moore、Robert Miller、Martin Braid、Robert Lane、Bert Beals、Calum Mackay、Allan Packer、Magnus Berg-man、Chris Larson、Bill Walker、Keith Bierman、Dan Mick 和 Raghunath Shenbagam 评审材料。
- 特别感谢 David Collier-Brown、Norm Shulman、Dominic Kay、Jarod Jensen、Bob Sneed 和 Ever Hoogdoorn 对全书逐页评审。
- 感谢 Solaris 部门的工程师 Jim Lichfield、Michael Shapiro、Jeff Bonwick、Wolfgang Thaler、Bryan Cantrill、Roger Faulkner、Andy Tucker、Casper Dik、Tim Marsland、Andy Rudolf、Greg Onufer、Rob Gingell、Devang Shah、Deepak Das、Dan Price 和 Kit Chow 的建议和指导。我们确定还有其他人，对遗漏的名字预先表示歉意。
- 感谢 Sun 的系统工程师和技术支持人员在此过程中提供的修正和建议。
- 感谢 Lou Marchant——为了无止寻找发动机图片，以及 Lotus Cars USA 的 Dwayne Schumat 协调使用 Lotus V8 发动机图片的许可。
- 感谢 Prentice Hall 的同事——Greg Doench 的耐心（我们确实弄丢了好几次）和支持。

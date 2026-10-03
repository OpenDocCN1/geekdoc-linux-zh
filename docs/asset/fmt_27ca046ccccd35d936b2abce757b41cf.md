
由于 `=` 命令只打印到标准输出，你无法在与模式相同的行上打印行号。你需要编辑多行模式来实现此点。

## 13.24 Linux 简史

Linux 是一个操作系统，一个控制你计算机的软件程序。大多数供应商在交付 PC 之前会在 PC 的硬盘上加载操作系统，因此，除非你 PC 的硬盘出现故障，否则你可能并不理解操作系统的功能。

1991 年，Linus Torvalds 开始开发一个操作系统内核，他将其命名为“Linux” [Torvalds 1999]。

### 13.24.1 Linux 的起源

Linux 的祖先可以追溯到 Multics（多路信息和计算服务）操作系统。Multics 起于 1965 年，是最早的多用户计算机系统之一，并一直使用至今。贝尔实验室与麻省理工学院以及通用电气共同参与了 Multics 的开发。

1969 年，贝尔软件工程师 Ken Thompson 和 Dennis Ritchie 离开了该项目。他们的爱好之一是玩一种名为 Space Travel 的游戏。由于没有 Multics 计算机，他们发现无法实现幻想。为了解决这个问题，他们决定将 Space Travel 移植到 PDP-7。最终，他们实现了一个名为 Unics 的操作系统（这对 Multics 是一个双关语）。名字的拼写变成了 Unix。

### 13.24.2 X 窗口系统

Linux 的另一个组件是它的图形界面，X 窗口系统。Unix 最初是一个无鼠标的文本系统，使用打字机而非 CRT 显示器。Unix 命令行界面非常复杂，即使是今天，高级用户也倾向于它而不是点击式的图形环境。因此，有些人不知道 Unix 早已经过了它的文本时代，现在为用户提供了图形或命令行界面的选择。

X 窗口系统（简称 X）是麻省理工学院（MIT）Athena 项目的一部分，该项目始于 1984 年。1988 年，MIT 将 X 发布给了 X 委员会，该委员会在 1995 年 9 月发布了 6。

X 在两个方面是独特的图形界面。首先，X 与计算机网络集成，允许用户访问本地和远程应用程序。例如，X 可以让你打开一个表示在远程服务器上运行的程序的窗口：远程服务器进行计算；你的计算机只需要传递服务器输入并显示服务器输出即可。

其次，X 让你极大地配置其外观和感觉。为了做到这一点，你需要在 X 之上运行一个特殊的应用程序——称为窗口管理器。

### 13.24.3 Linux 发行版

由于 Linux 可以自由分发，你可以通过多种方式获取它。在 Linux 社区中，不同的组织以不同的方式组合可用组件。每种组合被称为一个“发行版”，开发发行版的组织被称为“发行商”。各种个人和组织打包 Linux，通常将其与免费的专有应用程序结合。Linux 的种类有：

- Caldera OpenLinux
- Red Hat Linux
- Slack Linux
- Debian
- SuSE Linux
- GNU/Linux
- Mandriva (原 MandrakeSoft)
- Ubuntu
- Knopix: 一种从 CD-ROM 运行的操作系统，你无需安装任何内容。

Caldera、Red Hat、Slack 和 SuSE 由商业公司封装，这些公司旨在通过销售 Linux 相关产品和服务来获利。Debian GNU/Linux 是在公共利益软件协会（Software In The Public Interest, Inc.）这一非营利机构赞助下，通过志愿者努力的成果。Linux 内核不是 GNU 项目的一部分，但使用了与 GNU 软件相同的许可证。

大多数发行版提供了一套适用于通用 PC 的程序集，并带有包含针对 x86 Intel 基 CPU 优化内核的特殊软件包。这些发行版经过充分测试并定期进行维护，侧重于可靠的服务器实现以及易于安装的更新程序。例如 Debian、Ubuntu、SuSE 和 Mandriva，它们是到为止最受欢迎的 Linux 系统，通常被认为初学者易于上手，同时又不会限制专业人士充分利用其 Linux 设备。Linux 也运行在笔记本电脑和中型服务器上。新硬件的驱动程序经过广泛测试后才会包含，这增加了系统的稳定性。

## 13.24.4 Linux 的优势

1. 低成本：你不需要花费时间和金钱来获取许可证。由于 Linux 及其大部分软件采用 GNU 公共许可证，这些是大型存储库，你可以从中免费下载高质量的软件。
2. 稳定性：Linux 不需要定期重启以维持性能水平。它不会由于内存泄漏而随着时间推移导致或或缓慢。
3. 性能：Linux 在工作站和网络上提供高性能。它可以同时处理异常大量的用户。
4. 网络友好性：Linux 是由一组在互联网上工作的人员开发的，因此对网络功能有强力支持。它可以作为网络备份因素执行任务，并且比替代系统更真实。
5. 灵活性：Linux 可用于高性能服务器应用、桌面应用和嵌入式系统。
6. 兼容性：Linux 运行在所有常见的 Unix 软件软件包上，并可以处理所有常见的文件格式。
7. 选择：众多的 Linux 发行版提供了选择，你可以挑选你最喜欢的一个；核心功能是相同的，大多数软件可以在大多数发行版上运行。
8. 安装快速简便：大多数 Linux 发行版带有用户友好的安装和设置程序，流行的 Linux 发行版还带有工具，使得安装额外软件也变得非常用户友好。
9. 充分利用硬盘：即使硬盘几乎满，Linux 也能继续良好工作。
10. 多任务处理：Linux 设计用于同时执行许多事情。例如，后台中的一个大型打印作业不会减慢你的其他工作。
11. 安全性：Linux 是最安全的操作系统之一。Linux 用户可以选择选择并安全地从包含成千上万高质量软件包的在线存储库中免费下载软件。不需要信用卡号和其他敏感个人信息的购买交易。
12. 开源：如果你开发的软件需要了解或修改操作系统代码，Linux 源代码对你触手可及。Linux 应用也是开源的。

## 13.24 Linux 与 Unix 的区别

| 序号 | Linux | Unix |
| --- | --- | --- |
| 1 | Linux 是免费的 | Unix 不是免费的 |
| 2 | Linux 运行在许多硬件平台上 | Unix 受限于专有硬件 |
| 3 | Linux 价格便宜 | Linux 昂贵 |
| 4 | Linux 感觉非常像 80/90 年代后期的 DOS/WINDOWS | Unix 感觉像 60/70 年代的主机机 |
| 5 | Linux 更多偏向于想要运行自己的服务器或工程工作站的普通用户。 | Unix 在某些领域（如安全、工程应用）可能被认为更成熟，对尖端硬件有更好的支持。 |
| 6 | Linux 在这方面欠缺，因为大型应用程序难以通过认证。 | Unix 的商业版本在历史上对如 oracle 或 SAP 等企业级应用提供了大量的支持。 |
| 7 | Linux 不仅在不同发行版之间变化很大，有时在同一发行版的发布之间也是如此，导致很难理解工具所处的准确环境。 | Unix 从版本到版本的变化非常不大。 |
| 8 | Linux 代码库不断变化。 | Unix 代码库不变化，因此运行时间更长。 |

## 13.24.6 Linux 操作系统的结构

Linux 操作系统分为三个主要部分——内核（Kernel）、外壳（Shell）和实用程序应用程序（Utilities Application Programs）。

- **内核 (The Kernel)**
  这是 Linux 操作系统的核心。它执行创建和维护 Linux 环境的任务。它跟踪磁盘、磁带、打印机、终端、通信线路以及连接到计算机的任何其他设备。它还在计算机硬件和用户之间充当接口。

- **外壳 (The Shell)**
  这是一个在用户和 Linux 操作系统之间提供接口的程序。它监听用户的终端并翻译用户请求的操作。有许多不同的 Shell 可以使用。参见“外壳（The Shell）”章节。

- **实用程序和应用程序 (Utilities and Application Programs)**
  实用程序是 Linux 命令。应用程序（如文字处理器、电子表格和数据库管理系统）可以与 Linux 命令一起安装。用户可以通过 shell 运行实用程序或应用程序。

## 外壳 (The Shell)

外壳是一个提供在用户和 Linux 操作系统之间提供解释器和接口的程序。它执行从终端或文件中读取的命令。

有许多不同的 Shell 可以使用。每个 Shell 都为用户提供略有不同的界面。最广泛的是 Bourne shell (`bash`)。其他 Shell 如 `csh`、`ksh` 和 `zsh`。

## UNIX 和 SHELL 编程

当用户登录系统时，会自动启动一个 shell。它会监控用户的终端，等待发布任何命令。使用的 shell 类型存储在名为 `passwd` 的文件中。任何其他 shell 都可以通过作为命令运行子 shell。例如，`/usr/bin/ksh` 将运行 Korn shell。在 Korn shell 终止之前，原始 shell 仍在后台模式下运行。

## 用户 (Users)

Linux 是一个多用户操作系统。每个用户都需要创建和访问自己的文件。这些文件必须免受其他用户的侵扰。因此，每个用户在 Linux 系统上都有唯一的标识，并可以选择密码来增强安全性。

- **普通用户 (Ordinary Users)**
  每个用户都有一个主目录，文件和子目录通常存储在那里。登录系统后，用户通常会直接进入该目录。每个用户都是用户组的成员。出于安全考虑，用户拥有的文件（和目录）可以被用户、同组成员以及不同权限的所有用户访问和使用。

- **超级用户 (Super-User)**
  超级用户是特用户，对所有文件具有完全访问权限，无论所有者是谁或访问权限是什么。超级用户有一个责任：管理和维护系统。超级用户通常被称为 `root`。

# 练习题

- 1. 解释 UNIX 操作系统的系统结构。
- 2. 描述 UNIX 的文件和目录结构。
- 3. 定义操作系统的服务。
- 4. 进程在 UNIX 系统上运行时使用了多少个层级？请详细描述。
- 5. 画出系统内核的框图并解释其工作原理。
- 6. 什么是进程（Process）和进程上下文（Context）？定义状态和转换。
- 7. 如果内核尝试唤醒所有在某个事件上睡眠的进程，但在唤醒时没有进程在该事件上睡眠，会发生什么？
- 8. 在系统初始化期间，内核为缓冲区分配空间时缓冲区处理器（buffer handler）是什么？假设内核对某个块执行延迟写入。当另一个进程从哈希队列中获取该块时会发生什么？从空列表中获取又会怎样？
- 9. 在 `getblk` 算法（缓冲区分配算法）中，如果内核从空列表中移除缓冲区，必须在检查空列表之前提高处理器优先级以阻塞中断。为什么？
- 10. 假设内核对某个块执行延迟写入。当另一个进程从哈希队列中获取该块时会发生什么？
- 11. 在 UNIX 文件系统中，当块大小为 2048 且架构保持不变时，找到字节偏移 265100 的物理位置。
- 12. 当 UNIX 系统中包含 10 个直接地址、1 个单间接地址、1 个双间接地址且没有三级间接地址时，其最大的可能文件大小是多少？每个间接地址（单间接和双间接）指向一个 2K（2048字节）块。每个块号可用 32 位寻址。
- 13. 描述一种从缓冲区池请求并接收任何空缓冲区的算法。
- 14. 你如何理解向前搜索（forward search）和向后搜索（backward search）？
- 15. 将系统响应时间定义为完成系统所需的平均时间。描述缓冲区缓存如何帮助响应时间。它一定有助于系统吞吐量吗？

# UNIX 与 Shell 编程

- 16. 写一个用于缓冲区分配 `getblk` 算法。
- 17. 描述缓冲区缓存如何帮助响应时间。它一定有助于系统吞吐量吗。
- 18. C 语言规定数组从 0 开始计数。为什么 Inode 编号从 1 开始而不是 0？
- 19. 如果进程在算法中发现缓存中的 Inode 被锁定而进入睡眠，为什么在唤醒后必须从头重新开始循环？
- 20. 解释 `vi` 编辑器的三种模式。
- 21. 描述一个以内存中 Inode 为输入并更新相应磁盘 Inode 的算法。
- 22. 讨论使用位图（bit map）而不是块链表来跟踪空磁盘的系统实现。这种方案的优缺点是什么？
- 23. 写下磁盘块分配算法。
- 24. Inode 如何分配给新创建的文件？
- 25. 定义以下术语：
  - (i) 文件子系统（File-subsystem）
  - (ii) 进程僵尸状态（Zombie state）
  - (iii) 用户文件描述符（User file descriptor）
- 26. 写关于以下操作符短记：
  - (i) d-delete
  - (ii) c-change
  - (iii) y-yank
  - (iv) !filter
- 27. 写关于以下内容的短记：
  - (i) 引导块（Boot Block）
  - (ii) 超区块（Super Block）
  - (iii) Inode 块（Inode Block）
  - (iv) 数据块（Data Block）
- 28. 设计一种目录结构，通过避免线性搜索来提高路径搜索效率。
- 29. 描述普通文件的结构。
- 30. 讨论 UNIX 内存管理的特征。
- 31. 什么是系统调用（System call）？列出 10 个系统调用。
- 32. 你如何理解父进程和子进程？还要解释进程的状态。
- 33. 描述 `Fork()` 系统调用。为什么 `Fork` 不向子进程返回父进程 ID 而向父进程返回零？
- 34. 讨论 `Unlink` 系统调用。如何取消一个已打开的文件？
- 35. 假设目录对某个用户有读取权限但没有执行权限。当该目录作为带有 "i" 选项的参数使用时会发生什么？-l 选项又如何？
- 36. 如果内核允许两个进程同时在两个点挂载同一个文件，可能会发生什么奇怪的事？
- 37. 在目录上执行 `ls -ld` 命令时，注意目录的链接数永远不是 1。为什么？
- 38. 详细解释进程的过早终止。
- 39. 用户在更改密码时，是如何更新 `/etc/passwd` 的，即使该文件没有写权限？
- 40. 设计一个在虚拟地址和区域项地址的情况下，将虚拟地址翻译为物理地址的算法。
- 41. 设计一个分配和释放内存页及页表的算法。什么数据结构可以实现最佳性能或最简单的实现？
- 42. 实现内核栈在用户栈之上的系统是可能的。讨论这种实现的优缺点。
- 43. 假设一个进程进入睡眠且系统没有就绪运行的进程。当睡眠进程进行上下文切换时会发生什么？
- 44. 如果内核对所有在地址 A 上睡眠的进程发出唤醒调用，但此时没有进程在相应地址上睡眠，会发生什么？
- 45. 解释以下用于的 UNIX 命令：
  - (i) news
  - (ii) mail
  - (iii) wall
  - (iv) write
  - (v) mesg
  - (vi) crontab
- 46. `Fork()` 系统调用如何创建新进程。写一个 `Fork` 系统调用算法。
- 47. 画出进程状态图以及检查和处理信号的算法。
- 48. 写一个 shell 脚本，打印当前日期、用户名和登录 shell 的名称。
- 49. 在目录上执行 `ls -ld` 命令时，目录的链接数永远不是 1。为什么？
- 50. 当 shell 创建新进程执行命令时，它如何知道该文件是可执行的？如果是可执行的，它如何区分 shell 脚本和编译产生？检查上述情况的正确顺序是什么？

# UNIX 与 Shell 编程

- 51. 编写一个菜单驱动的程序，包含以下选项：
  - (i) `/etc/passwd` 的内容
  - (ii) 当前工作目录
  - (iii) 当前已登录用户列表
  - (iv) 退出
- 52. 阐述 Linux 操作系统开发开源通用许可证（GPL）的情况。给出 Linux 操作系统的发展历史。
- 53. `get` 和 `iput` 算法不需要提高处理器执行级别来阻塞中断，这说明什么？
- 54. 描述 `kill` 系统的实现。
- 55. 进程在进入或离开睡眠状态时检查信号，并在完成系统调用或处理中断后返回用户态。为什么进程在进入系统调用时不需要检查信号？
- 56. 解释如果 setuid 程序不受写保护会存在什么安全问题。
- 57. 如果 Annoop 使用 `su` 命令变成超级用户，他无法执行目录中的任何脚本。请解释原因。
- 58. 解释以下 shell 变量的：`$#`、`$*` 和 `$@`。
- 59. 写一个 shell 脚本，按大小降序报告指定目录下大于 40 字节的文件名和大小。也显示搜索文件的总数。
- 60. 提到不同的 grep 系列命令并简要解释每一个。所有 grep 系列命令都可以使用多个搜索模式吗？
- 61. 写一个 shell 脚本，从当前目录提取所有的 'C' 程序文件并在每个文件后添加 '.CPP' 扩展。
- 62. 使用 `sed` 命令统计数据库中 1977 年出生学生的数量。
- 63. 讨论如何使用 `sed` 插入输入文件的内容。
- 64. 当 shell 创建新进程执行命令时，它如何知道该文件是可执行的？如果是可执行的，它如何区分 shell 脚本和编译文件？检查上述情况的正确顺序是什么？
- 65. 以下 UNIX 命令的功能是什么？请通过示例并编写该命令的正确语法来解释：
  - (i) tr
  - (ii) awk
  - (iii) grep, egrep, fgrep
  - (iv) finger
  - (v) batch
  - (vi) bc
  - (vii) sort
  - (viii) cut
  - (ix) copy
  - (x) umask
- 66. 你如何理解在 UNIX 中挂载（mounting）和卸载（unmounting）文件系统？它是如何实现的？
- 67. shell 的基本功能是什么？讨论 UNIX 操作系统中使用的不同类型的 shell。
- 68. 什么是 shell 编程？编写一个在 UNIX 中备份的 shell 脚本。
- 69. 密码文件（password file）和组文件（group file）的意思是什么？列出这些文件中存在的不同条目。
- 70. 解释 UNIX 中的 case 语句（case statement）。
- 71. 写出进程调度的算法。写出调度参数。
- 72. 写出客户端进程和接收消息的算法。
- 73. 共享内存是如何一次或多次附加到进程的？
- 74. 详细描述套接字（sockets）模型。
- 75. 多处理器系统的问题是什么？如何通过主从处理器和信号量（semaphore）来解决？
- 76. 描述 Linux 结构并定义 Linux 的特性。
- 77. awk 中内置的特殊模式（specials built in pattern）有哪些？描述这些模式。
- 78. 延迟写入机制（delayed write mechanism）的优点是什么？
- 79. 写出一个为数据块分配缓冲区的算法。针对输入数据的所有可能变化，追踪你的算法。
- 80. inode 节点的内容是什么？内存中节点（in-core inode）中还需要存储哪些额外信息？为什么？
- 81. 给出 UNIX 系统内存的布局。描述每个部分。
- 82. 写下 UNIX 的安全特性。
- 83. 什么是 awk 模式（patterns)?描述 BEGIN 和 END 模式。
- 84. 简述 UNIX 中使用的一种进程同步技术。
- 85. 什么是管道（pipes）？区分命名管道（named pipes）和无名管道（unnamed pipes）。
- 86. 描述 write 系统调用是如何工作的。它的输入参数和返回信息是什么？请结合算法进行描述。
- 77. 讨论普通文件的结构。如何将字节偏移量（byte offset）转换为块号算法？
- 88. 写关于以下内容的短记：
  - (i) Linux 的特性
  - (ii) 设备驱动程序
  - (iii) 文件系统的挂载
  - (iv) 多处理器系统的局限性/问题。
  - (v) Linux 的种类（Flavors）
- 你如何将字符串 "Linux" 替换为 "Red Hat Linux"?
- 89. 解释 perl 中的列表（Lists）、数组（Arrays）和哈希（Hashes）。如何获取以下内容：
  - (i) 仅关联数组中的键（keys）
  - (ii) 关联数组中的值（values）
  - (iii) 从关联数组中删除元素
  - (iv) 从关联数组中插入元素
- 91. 写一个 `sed` 序列来查找文件中某个模式的出现次数。
- 92. 讨论 awk 脚本的结构。解释 awk 的运行机制。提到不同的 awk print 函数，并列出它们行为之间的差异（如果有的话）。
- 93. 什么是关联数组（associative arrays）？一个文件书籍列表列出了不同工程学科每月销售的书籍数量。写一个 awk 脚本，找出每个学科销售的书籍总数以及书籍销售总数。
- 94. 你如何删除文件末尾的所有空格？
- 95. 使用 `sed` 在每行的开头插入两个空格。
- 96. 在不使用循环的情况下，打印字符串 "Anoop" 15 次。
- 97. 什么是 perl 编程？写一个 perl 脚本将二进制数（作为参数提供）转换为十进制。
- 98. 使用 (i) `grep` (ii) `sed` (iii) `perl` 找出两个连续且相同的单词字符（如 aa 或 bb）的出现次数。
- 99. 写一个 perl 脚本按逆序打印行。
- 100. 解释 Linux 安全特性。

# 索引

## A
- `@ARGV` 和 `%ENV`, 160
- 磁盘块分配 (Allocation of Disk Block), 32
- 数组迭代 (Array Iteration), 162
- 数组—`@`, 157
- 等待进程终止 (Awaiting Process Termination), 365
- `awk`, 128
- awk 程序中的注释 (Comments in awk Programs), 129
- 控制码 (Control Codes), 167
- 跨越挂载点 (Crossing Mount Points), 63
- C-Shell, 103

## B
- 块地址方案 (Block Addressing Scheme), 13
- 块预读 (Block read ahead), 32
- 布尔表达式 (Boolean expression), 110
- 引导块 (Boot Block), 12
- Bourne Shell (Bourne Shell), 103
- 缓冲区缓存 (Buffer Cache), 23
- 缓冲区头 (Buffer Headers), 23
- 缓冲区 (Buffer), 10, 36
- 数据块 (Data Blocks), 13
- 数据报文 (Datagram), 98
- Date 命令 (Date Command), 107
- 直接块和间接块 (Direct and Indirect block), 38
- 磁盘控制器 (Disk controller), 31
- 磁盘 inode (Disk Inodes), 35
- Dup, 60

## C
- 内置函数 (Built-in Functions), 140
- 挂载点 (Crossing Mount Points), 63
- [此处对应原文格式]

## E
- 环境变量 (Environment Variable), 113

## F
- 字符码 (Character Codes), 166
- 清除命令 (Clear Command), 108
- 管道关闭 (Closing pipes), 59
- UNIX 的特性 (Features of UNIX), 31
- 文件创建 (File Creation), 56
- 文件输入 (File Input), 163
- 文件系统布局 (File system), 12
- 进程创建 (Fork()), 83
- 释放块 (Freeing a Block), 47

## G
- 获取行 (Getline), 137
- grep 家族 (Grep Family), 116

## H
- 如何运行 awk (How to Run awk?), 129
- 哈希数组 (Hash Arrays), 159

## I
- 内存 inode (Incore Copy), 35
- inode (Inodes), 13
- 内部和外部命令 (Internal and External Command), 105
- 中断和异常 (Interrupts and Exceptions), 8

## K
- 内核数据结构 (Kernel Data Structure), 21
- Knoix, 180

## P
- 模式匹配 (Pattern Matching), 112
- 进程表 (Process Table), 17
- `perl`, 148
- Chop 函数 (Chop Function), 150
- perl 脚本 (Perl Script), 149
- perl-$ 和 _, 156
- perl 算术运算符 (PERL--Arithmetic Operators), 152
- perl 赋值运算符 (PERL--Assignment Operators), 153
- perl 逻辑和关系运算符 (PERL--Logical and Relational Operators), 154
- 管道 (Pipes), 58
- 进程 (Process), 15
- 进程创建 (Process Creation), 83
- 进程结构 (Process Structure), 17
- 进程状态和转换 (Process State and Transitions), 70
- 进程终止 (Process Termination), 89
- 进程追踪 (Process Tracing), 90
- 进程树和共享 (Process Tree and Sharing), 59

## L
- 内存布局 (Layout of System Memory), 72
- 链接 (Link), 66

## R
- Linux, 177
- 分配节点竞争条件 (Race condition assigning nodes), 45
- Linux 发行版 (Linux Distributions), 178
- 读取 (Read), 50
- Linux 操作系统 (Linux Operating System), 181
- 读者和写进程 (A Reader and A Writer Process), 53
- awk 中的循环 (Loops in awk), 131
- 区域表 (Region Table), 17
- 寻 (LSeek), 54
- 关系表达式 (Relation expression), 110
- 内存中的 inode (Remembered Inode), 43

## M
- 删除文件和目录 (Remove file and directory), 106
- 消息 (Messages), 92
- mknod, 56
- 挂载 (Mount), 61

## S
- 多处理器系统 (Multiprocessor Systems), 99
- 获取缓冲区的场景 (Scenarios for retrieval of a Buffer), 25
- sed (Sed), 171
- 信号量 (Semaphores), 95, 102
- 共享内存 (Shared Memory), 93
- shell 编程 (Shell Programming), 117

## O
- 打开 (Open), 49

## 索引 191
- shell, 88, 103
- 系统调用 (System Calls), 49
- 睡眠和等待 (Sleep and Wait), 120
- 系统 V IPC, 91
- 睡眠和唤醒 (Sleep and Wakeup), 20

## T
- 睡眠 (Sleep), 77
- X 系统 (The X Window System), 178
- 套接字 (Sockets), 97
- UNIX 系统的树形结构 (Tree Structure of UNIX O.S.), 5
- 启动和清理动作 (Startup and Cleanup Actions), 132
- shell 类型 (Types of Shell), 2

## U
- 字符串处理 (String Processing), 165
- U 区域 (U-Area), 17, 72, 75
- 字符串 (Strings), 150
- UNLINK, 68
- UNIX 系统结构 (Structure of UNIX System), 1
- 卸载 (Unmounting), 65
- 子程序 (Subroutines), 169
- user-ID, 86
- 超数据块 (Super Block), 12
- 系统管理 (System Administration), 21
- 系统调用和库 (System Calls and Libraries), 9

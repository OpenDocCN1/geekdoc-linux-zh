

第三部分，“LSB 认证”，概述了 Linux 发行版及其软件产品的 LSB 认证流程。此信息将帮助希望申请自由标准组织 LSB 认证的读者。

第四部分，“为 LSB 项目做贡献”，解释了如何将新的接口和架构添加到 LSB 书面规范中。理解 LSB 标准化过程有助于欣赏 LSB 的准确性，并了解扩展标准范围的程序。

第五部分，“使用 LSB 资源”，概述了如何使用 LSB 提供的资源。此信息包括对 LSB 书面规范、测试套件、示例实现、开发环境和应用程序测试套件的描述。本部分还解释了如何使用和获取这些资源的最新发行版。

## 格式高亮说明

本书使用以下高亮约定：

-   **粗体** 命令。
-   `等宽字体` 文件、路径、函数、选项、标志和变量的名称。
-   `等宽斜体` 文件或路径名称中可替换的元素，如架构类型或提供商名称。
-   $ command_line 可作为任何用户执行的命令（在示例中）。
-   # command_line 应作为 root 用户执行的命令（在示例中）。
-   vxs$ command_line 必须作为用户 vxs0 执行的命令。
-   \\ 在程序列表示例中，反斜杠用于长行末尾，以延续到下一行。

![](img/d75cffbcb54aabfb0f9854162061d394_23_0.png)

注释用于标识特殊说明。

## 关于作者

**Stuart Anderson**  
开源顾问，netSweng

Stuart Anderson 在“开源”这一术语诞生之前就参与到了开源事业中。Stuart 是一名软件工程师，自 1989 年以来，他曾在 NCR、AT&T 和 Metro Link, Inc. 工作，为从小型嵌入式设备到大型多处理器服务器在内的各种操作系统开发软件。Stuart 自 1992 年起参与 XFree86 项目，现在是 XFree86 核心团队的成员。Stuart 在 90 年代中期曾参与 X Consortium 和 System V ABI 的标准化工作，自 LSB 创立之初便参与其中。

**Mark Brown**  
IBM 公司高级技术员工

Mark Brown 拥有 16 年的 UNIX 和 Linux 经验，并曾担任多个 AIX 版本发布的架构师。他专门从事操作系统标准规范和实现，以及二进制兼容性问题。他拥有德克萨斯州立大学的学士学位。

**Kevin Caunt**  
IBM 系统与科技集团，Linux 技术中心顾问软件工程师

Kevin Caunt 拥有超过二十五年的计算机行业经验，并于 2000 年加入 Linux 标准基（LSB）项目。加入后，他一直在 LSB 的各个方面工作，包括测试套件开发和试点项目。Kevin 还是 LANANA 指导委员会的成员。Kevin 自 1982 年起在 IBM 工作，担任过各种软件和硬件工程职位，目前在大德克萨斯奥斯汀的 Linux 技术中心工作。

**Marvin Heffler**  
IBM 系统与科技集团，Linux 技术中心顾问软件工程师

Marvin Heffler 是自由标准组织 Linux 标准基工作组的核心成员。该工作组正致力于标准化 Linux 操作系统中与应用程序运行至关重要的部分，从而扩大应用程序可移植性的范围。虽然 Marvin 参与了 LSB 的多个领域，但他的主要工作是领导开发用于验证 Linux 发行版正确运行的 LSB 应用程序测试套件。Marvin 在 IT 行业从事软件工程及软件开发管理工作近二十年。Marvin 于 1984 年从 Texas A&M University 获得计算机科学学士学位。毕业后，Marvin 开始为 Texas Instruments 工作。在接下来的九年里，Marvin 参与了各种 TI 计算机系统中固件、SCO Xenix/Unix 和 System V.3 的开发。1993 年，Marvin 加入 IBM，大部分职业生涯都作为 AIX 操作系统的开发人员和经理。2001 年夏天，Marvin 加入 IBM Linux 技术中心，开始从事 Linux 工作。除了参与 LSB 核心团队的工作外，Marvin 还与 IBM 内部的应用程序开发团队合作，以促进 LSB 的采用。

**Andrew Josey**  
The Open Group 认证总监

目前，Andrew Josey 担任 Austin Group 主席，该工作组负责 POSIX 和 Single UNIX Specification 联合修订版的开发。这项工作最近已获得 ISO/IEC 9945:2003 国际标准化地位。他是 IEEE 计算机协会 Golden Core 的成员，也是 IEEE P1003.1 主席和 IEEE PASC 解释功能主席。

Andrew 是 The Open Group 中 Linux 和开源领域的倡导者。他是 Linux 标准基测试项目的技术负责人，曾担任自由标准组织董事会成员，并代表自由标准组织成功管理并部署了 LSB 认证项目。

Andrew 自 1987 年起在行业内工作，在 1996 年加入 The Open Group 之前，曾在 AT&T UNIX Europe、UNIX System Laboratories 和 Novell 工作。

**George Kraft IV**  
IBM 系统与科技集团，Linux 技术中心高级软件工程师

George Kraft 于 1999 年 10 月作为记录员开始参与 LSB 工作（LSB v0.1），2000 年 6 月成为项目经理（LSB v0.2），2001 年 3 月当选为主席（LSB v0.7）。George 担任主席和项目经理近三年。在他的任期内，LSB 工作组发布了 LSB v1.0 (6/01)、LSB v1.1 (1/02)、LSB v1.2 (6/02)、LSB v1.3 (12/02) 和 LSB v1.9 (8/03)，后者是 LSB v2.0 (9/04) 的预览版。

作为主席，George 协调了 LSB 书面规范的开发工作，与其他 LSB 团队负责人、架构师和团队成员密切合作。George 在 IT 行业拥有大约十七年的 UNIX/Linux 软件工程师经验。自 1982 年起，他在印第安纳州西拉法叶的普渡大学开始本科学习，当时他便开始使用 UNIX 进行开发，并于 1987 年获得计算机科学和数学学士学位。自 1993 年起，他开始使用 Linux 进行开发。George 主要在命令和库领域工作，为普渡大学的 SunOS、BSD 和 Dynix，Texas Instruments 的 System V.3，以及 IBM 的 AIX 3.x-4.x 和 NetBSD 1.4 做出了贡献。此外，他还在 Linux 瘦客户端领域为 IBM 的 Network Station（现归入 Netvista 品牌）工作。他曾是 CAD（计算机辅助设计）框架倡议的 UNIX 团队负责人，该倡议是德克萨斯州奥斯汀的一个电子设计自动化标准机构。George 在 IBM Linux 技术中心的角色是作为 IBM 内部顾问，专注于如何最好地将 LSB 的标准和规范整合到 IBM 的软件组合中。

**Scott McNeil**  
自由标准组织执行总监

Scott McNeil 是自由标准组织的联合创始人和执行总监。通过 Scott、他的团队以及众多贡献者的努力，自由标准组织已成为 Linux 和开源软件领域领先的标准化组织，受到国际开发社区、主要 IT 供应商、政府机构和非营利组织的有力支持。自 2000 年成立以来，自由标准组织发布了多个版本的 Linux 标准基（LSB）书面规范和测试套件，并启动了 LSB 认证项目，全球主要 Linux 发行版厂商均参与其中。

2003 年，ISO（国际标准化组织）和 IEC（国际电工委员会）联合技术委员会正式承认自由标准组织为 Linux 公开可用规范（PAS）的提交者——这是 Linux 操作系统获得 ISO 认证的关键前提。

在 Scott 的指导下，自由标准组织还管理了 OpenI18N 工作组开发和部署国际化规范和测试套件的努力。Scott 负责将自由标准组织的工作组数量扩展到包括 DWARF、LANANA、OpenPrinting、Open Cluster 以及新的 Accessibility 工作组。

Scott 活跃于 Linux 和开源社区超过八年，此前曾在 VA Linux 和 SuSE 等公司担任管理职务，目前在 IBM 工作。

**Kristin Thomas**  
IBM 系统与科技集团信息开发者

Kristin Thomas 是一名支持 AIX 操作系统的信息开发者。在从事 AIX 工作之前，Kristin 曾在 IBM 的 Linux 技术中心编写 Linux 文档。在 Linux 技术中心，她为开源项目编写文档，例如 Linux 标准基、openCryptoki 和 IBM


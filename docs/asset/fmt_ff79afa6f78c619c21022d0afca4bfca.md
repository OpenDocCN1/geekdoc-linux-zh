
该网站还包含 SNMP 工具，包括请求或设置 SNMP 代理信息的工具、生成和处理 SNMP Trap 的工具以及基于 Perl/Tk/SNMP 的图形 MIB 浏览器。

eCos SNMP 两个包：代理和库。SNMP 包以这种方式安排是为了与原始的 UCD-SNMP 实现保持一致。包的分离允许 eCos 客户端应用程序使用 SNMP 库而不包含代理包。

代理包含特定的应用程序处理程序，允许远程管理器检索有关设备的 MIB 信息。库包含使用 SNMP 协议格式化包和 MIB 文件的代码，其使用了抽象语法表示法 (ASN-1)。库支持 SNMP 版本 2，并确保版本 3 的安全身份验证。数据库信息兼容 MIB-II。

eCos SNMP 包位于 `net` 目录下的 `snmp` 子目录下。SNMP 代理 (`CYPGKG_SNMPAGENT`) 位于 `agent` 子目录，SNMP 库 (`CYPGKG_SNMPLIB`) 位于 `lib` 子目录。SNMP 包要求包含网络包。

代理包含一个位于 `snmp.c` 文件中的单线程 `snmp`，它在 `cyg_net_snmp_init` 程序中初始化。该任务运行的优先级比后台网络任务 (`CYPGKG_NET_THREAD_PRIORITY`) 低一级。应用程序必须调用位于 `snmptask.c` 文件中的 `cyg_net_snmp_init` 函数来启动 SNMP 代理。

# 第 8 章 附加功能与第三方贡献

库包包含依赖于文件系统存在的功能。目前，在 eCos 中尚未实现该功能；因此，如果需要此功能，则由应用程序提供文件系统支持。

SNMP 包中还包含一个 MIB 编译器工具。MIB 编译器位于代理包中 `utils\mib2c` 子目录。。该工具是一个 Perl 脚本，它接收 SNMP 代理包中包含的 MIB 并将其编译为 C 语言。MIB 编译器的输出可以进行修改，以支持特定应用程序所需的 MIB 功能。然后可以对新的 MIB 重新编译并在应用程序中使用。默认的 eCos MIB 位于代理包中 `mgroup\mib1` 子目录下。在 MIB 编译器中有两个 readme 文件：`readme.mib2c` 和 `readme-ecos`。

## 8.8 GoAhead 嵌入式 Web 服务器

尽管 SNMP 长期以来一直是远程管理的标准，但越来越多的设备正在寻求一种替代方法，以消除 SNMP 的缺点。目前的趋势是使用 Web 协议（如超文本传输协议 (HTTP)、超文本标记语言 (HTML) 和 Java）进行远程设备管理，这也称为基于 Web 的管理。这是通过在设备上运行嵌入式 Web 服务器实现的。设备的数据可以生成并在 Web 页面上表示动态内容。这些页面可以通过任何标准浏览器访问，并成为设备的图形界面。当设备可以使用通用接口（如浏览器）进行控制时，设备变得更加用户友好。例如，如果任务可以通过浏览器界面完成，那么为录像机编程可能不再是一项令人生畏的任务。

使用 SNMP 进行远程管理存在一些缺点。缺点之一是需要应用程序软件来控制远程设备，这通常成本高昂且难以使用。另一个缺点是 SNMP 使用 UDP，这在跨网络通信中是一种不可靠的协议。传输过程中丢失的数据包不会重传，也不会提供对接收数据包的确认。如果数据包包含的信息对系统至关重要，这可能会导致严重的后果。

随着 Web 这一新兴趋势，基于 Web 的管理允许使用大多数用户熟悉的标准接口。将浏览器作为接口还允许使用手持设备（大多数设备将浏览器作为标准软件）进行便携式管理。设备的网络通信使用 TCP 实现，这是一种可靠的协议。

目前在产品中使用 GoAhead Web 服务器的公司包括惠尔-帕奇（Hewlett-Packard）、霍尼韦（Honeywell）、西门子（Siemens）和佳能（Canon）。完整的客户列表在 GoAhead 网站上提供：

www.goahead.com/webserver/customers.htm

> 我妻子觉得录录像机是一项令人生畏的任务，她对此证实，因此依赖我来处理她所有的视频录制需求。然而，她是计算机方面的小天才，可以使用她最喜欢的浏览器浏览网页。

### GoAhead 嵌入式 Web 服务器

基于 Web 管理方法的一个缺点是，一旦页面发送到浏览器，其内容就是静态的，除非有某些用户干预（例如刷新请求）。如果需要持续的数据流或需要通知用户设备上的警报状态，就会出现问题。解决此问题的一种方案是使用 HTTP REFRESH 标签，强制浏览器在指定的间隔重新请求数据。另一种方案是通过使用 Java applets 和 JavaScript 持续从设备请求数据。

GoAhead Web 服务器是一个专为嵌入式系统设计的开源嵌入式 Web 服务器。源代码用 C 语言编写。与典型的基于服务器的服务器不同，GoAhead Web 服务器专注于满足嵌入式系统中的限制条件，包括：

- 小的内存占用
- 可配置的安全模型
- 支持生成动态 Web 页面内容
- 支持没有文件系统的设备
- 跨广泛平台和 CPU 架构的移植性
- 将源代码集成到高度定制的设备中

Web 服务器需要 TCP/IP 栈和大约 60 kbytes 的内存。GoAhead Web 服务器支持：

- 活动服务器页 (ASP)
- 进程内通用网关接口 (CGI)
- 嵌入式 JavaScript
- 带有 HTTP 1.1 持久连接的 HTTP 1.0
- 每秒 65 个连接
- 安全套层 (SSL) 版本 3.0
- 摘要访问认证 (DAA)
- 通过登录访问进行用户管理
- 在 ROM 中存储 Web 页面

目前，eCos 不提供 SSL 支持。可以在 GoAhead Web 服务器网站上在线找到更多信息：

www.goahead.com/webserver/webserver.htm

与 eCos 许可类似，GoAhead Web 服务器 免费提供其源代码，以换取对源码库的任何增强。在产品中使用 GoAhead Web 服务器有三个基本要求。第一，在出货使用 Web 服务器的产品之前必须通知 GoAhead。第二，必须在初始页面上显示 GoAhead 标记（可以在其网站上找到）。最后，GoAhead 允许识别使用 Web 服务器的公司进行市场营销活动。GoAhead Web 服务器的许可可以在在线找到：

www.goahead.com/webserver/license.htm

GoAhead 网站包含一个可以搜索的问题数据库及其解决方案。GoAhead 提供了一个错误报告表单，允许您提交有关 Web 服务器的特定问题。错误也可以通过电子邮件发送到：

webserverbugs@goahead.com。

系统需要识别哪些公司正在使用 Web 服务器进行市场营销活动。关于此的附加信息可以在此处找到：
goahead.com

## 8.9 对称多处理

SMP 是一种使用多个 CPU 协同工作的架构。这在许多高性能系统中很常见，但在嵌入式系统中也变得常见。eCos 支持 SMP，但存在一些局限性。在 SMP 系统中，内核必须能够保护其数据结构免受并发访问。这是通过调度锁实现的，调度锁在获取锁时原子递增，释放时递减。当计数值为零时，调度器允许选择不同的线程。某些中断服务程序 (ISR) 只能在特定的文中调用。对于 SMP 系统，需要一种不依赖中断操作的内核锁定机制。这种特殊的同步机制称为自旋锁。自旋锁在第 6 章线程与同步机制中介绍。

此外，还添加了用于 SMP 处理的函数。其中一个允许将中断路由到特定的 CPU。另一个函数允许您查找系统中的中断是由哪些 CPU 处理的。有关这些以及中断函数的详细信息可以在第 3 章异常与中断中找到。

## 8.10 附加功能

现在我们已经涵盖了 eCos 系统中可用的一些主要功能，让我们快速查看 eCos 支持的其他附加功能。本节旨在让您了解 eCos 支持的其他功能；但这些包的操作细节被省略了。

动态加载器允许在运行时加载可执行链接格式 (ELF) 文件。加载新的 ELF 文件后，运行的应用程序可以调用新镜像中的函数。动态加载器包 (`CYPGK_LOADER`) 位于 `services\loader` 目录。

www.gzip.org/zlib

eCos 提供了支持 Microwinds 图形用户界面（GUI）。Microwinds 是一个开源项目，旨在让现代图形窗口界面的特性运行在较小的设备上。Microwinds 程序包（`CYPGKG_MICROWINDS`）位于 `services\gfxmw` 目录下。关于 Microwinds 的更多信息可以在软件包内的 `doc` 目录下找到，也可以在网上查看：

www.microwinds.org

eCos 还提供了一个通用的电源管理包。该包提供了一个框架，允许在嵌入式系统中整合额外的电源管理功能。电源管理包（`CYPGKG_POWER`）位于 `services\power` 目录下。关于电源管理包的更多信息包含在软件包内的 `doc` 目录中。

## 8.11 总结

在本章中，我们简要回顾了 eCos 系统以及第三方贡献者提供的某些可以包含在应用程序中的额外功能。这些额外功能扩展了 eCos 的核心功能，使 eCos 能够满足更广泛嵌入式系统的需求。既然你已经了解了这些功能，通过额外的调研，就可以快速将它们集成到你的系统中。

## 参考文献

Sakamura, Ken. µITRON 3.0, An Open and Portable Real-Time Operating System for Embedded Systems. (IEEE Computer Society Press, 1997).

Stevens, W. Richard. TCP/IP Illustrated, Volume 1: The Protocols. (Addison-Wesley, 1994).

McUsick, Marshall Kirk, and Keith Bostic. The Design and Implementation of the 4.4BSD Operating System. (Addison-Wesley Longman, Inc., 1996).

## RedBoot ROM 监控器

本章介绍了 RedBoot ROM 监控器嵌入式软件工具。RedBoot ROM 监控器提供了调试和引导支持。我们涵盖了让 RedBoot 在目标硬件上运行并与主机单元通信所需的安装和配置细节。

我们查看了用于控制所提供功能的 RedBoot 用户界面和命令。理解构建 RedBoot 镜像的方法对于利用升级和扩展默认命令集至关重要；然而，我们将在本书的后续章节中介绍这些信息。尽管 RedBoot 是一个可以与任何实时操作系统配合独立程序，但本章的内容侧重于结合 eCos 使用 RedBoot。

## 9.1 概述

RedBoot 是 Red Hat Embedded Debug and Bootstrap 的缩写。它是一个为嵌入式系统设计的程序，提供调试和引导环境。RedBoot 旨在取代旧的程序；特别是 CygMon 和 GDB stub ROM。事实上，CygMon 已不再受支持。

RedBoot 是一个基于 eCos 的应用程序，使用 eCos 硬件抽象层作为其基础。然而，RedBoot 可用于任何嵌入式系统或配合任何 RTOS。RedBoot 可在产品开发周期用于调试支持，或在发布的产品中提供闪存和网络启动。RedBoot 提供的某些功能包括：

- 引导脚本支持
- 用于监控和控制的命令行界面 (CLI)
- 通过串口或以太网端口访问
- GDB 支持
- Flash 镜像系统支持
- X/Y  支持
- 使用 BOOTP 或静态 IP 地址配置的网络引导支持

RedBoot 是一个独立的、自包含的模块，作为应用程序运行在目标平台上。RedBoot 包含一个 GDB 存根（更多信息请参阅第 8 章“附加功能与第三方贡献”），允许从 GDB 主机连接到目标平台进行应用程序调试。此调试连接可以通过串口或以太网端口实现。RedBoot 使用独立的栈，与 eCos 网络栈分离，它为网络通信提供了功能基础。

RedBoot 支持从 ROM、RAM、软盘或使用 ext2 文件系统的集成磁盘电子 (IDE) 硬盘启动。还提供 ROMRAM 模式；在这种情况下，RedBoot 留存在 ROM 中，但在开始运行之前会被复制到 RAM 中。

当我们在构建 RedBoot 镜像时（如第 12 章“使用 eCos 的应用程序示例”所示），结果是一个二进制文件，该文件被直接程序化加载到目标硬件上。取决于配置选项和软件包，RedBoot 镜像可以包含用于使用目标硬件所有功能的所有软件组件。

图 9.1 显示了 RedBoot 监控器包含的一些功能的块图架构。从该插图中，我们可以看到 RedBoot 提供的功能都包含在 RedBoot 程序镜像中。RedBoot 与 eCos 应用程序之间的交互取决于两个镜像中的配置选项设置。RedBoot 可以配置为提供简单的加载和运行功能，也可以配置为提供闪存管理支持、通过串口使用 CLI 对 eCos 应用程序进行监控和控制，以及 GDB 调试能力。

RedBoot 目前在市场上的许多产品中都有提供，包括：

- Intel 家庭用网关
- Intel XScale 开发板
- Intel StrongARM 开发板
- MIPS Malta 4kc/5kc/20kc 开发板
- MIPS Atlas 4kc/5kc/20kc 开发板

RedBoot 的最新开发信息可以在网上找到：

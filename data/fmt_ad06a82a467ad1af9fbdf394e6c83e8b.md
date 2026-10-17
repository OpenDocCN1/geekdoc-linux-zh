
## 总结

多年来，Progress 数据库证明是一个极其可靠的产品，同时易于使用和管理。安装只需从介质复制并设置几个变量。尽管它有许多如向前恢复（`Roll Forward Recovery`）和两阶段提交（`2-Phase commit`）等高级功能，但这些并非强制性的，且管理非常简单。许多启动选项允许自定义 Progress 操作、提高性能并平衡资源利用。虽然 Progress 是成本敏感型中小型企的极佳选择，但某些大型公司可能需要 Linux 版 `v8.3` 中未提供的额外 24x7 运行功能。除了这些高端功能外，Progress 以更低的成本提供了大牌数据库具备的所有真正重要的功能。

## 常见问题 (FAQs)

- **问：旧的 Progress Corporation 是怎样的？**
  **答：** `PSC`于 1981 年以 Data Language Corp. 的名成立。这就是安装期间使用的 `DLC` 变量的起源。自 1983 年商业化以来，该产品一直被称为 Progress。为了保持这一品牌知名度，公司名称在 1987 年进行了更改。`PSC` 于 1991 年上市，并在 Nasdaq 上以代码 `PRGS` 交易。

- **问：WorkGroup 版本和 Enterprise 版本数据库有什么区别？**
  **答：** WorkGroup 设计用于最多 35 个用户，且仅支持最高 50 用户级别。几乎所有高级性能功能，如可变数据库块、后台页面写入器和 `-spin` 参数都是不可用的。向前恢复、崩溃保护（Crash Proof）、网络化、单连接中的多个数据库连接以及两阶段提交等基础功能在两种数据库中都适用。但任何对性能有要求的用户，最终都会考虑购买 Enterprise 版。

- **问：Progress 国际可用吗？**
  **答：** 是的；事实上，Progress 在全球设有办事处。在某些 Progress 未设分支的地方，建立了国家分销网络。每个办公室都有不同的政策和价格表，因此请务必与您的当地办公室联系。Progress 网站上提供列表。

- **问：对于 Progress 有推荐的 RAID 级别吗？**
  **答：** 没有推荐基于校验的 RAID (`2,3,4,5,7, ...`)。基于校验的 RAID 会导致性能的“滑稽模仿”。它的存在是为了让你成为 RAID 供应商的回头客，因为你需要不断地升级和增强才能从此类系统中获得合理的性能。`RAID 0`（条带）和 `RAID 1`（镜像）不是基于校验的 RAID 性能，因此是很好的选择（尤其是当结合使用时）。你必须添加 RAM 并伪造 I/O 请求的完成（“写回”缓存与“直写”缓存）来提高基于校验的 RAID 性能，而你可以通过增加磁盘来提高条带和镜像系统的性能。磁盘比 RAM 便宜（尤其是 RAID 阵列和大型服务器所需的 RAM），你可以添加更多（即使预算无限，可添加的 RAM 数量也有严格限制……）。而且在掉电时，如果启用了写回缓存（基于校验的 RAID），一个小失误你的数据库就会处于危险（电池备份已知会），因为阵列向 Progress 告知了磁盘上的真实情况，这使得崩溃恢复变得非常不稳定。

- **对 RAID 5（及其兄弟版本）说不。**

- **问：为什么 Progress 不支持 RAID 5？**
  **答：** Progress 支持 `RAID 5`。但像其他所有数据库一样，它在其他磁盘技术上运行要快得多。Progress 并不会感知你使用的是哪种 RAID 系统。只有你的用户能感受到这一点。

- **问：我目前通过安装 SCO 二进制文件使用 Progress。我需要做什么才能切换到原生 Linux 版本？**
  **答：** 首先，联系您的 `PSC` 销售代表切换到 Linux 平台，并按照本章描述安装原生二进制文件。为该版本的 Progress 选择一个单独目录。修改环境变量，特别是 `SDLC` 变量，以及现有的启动/关闭/备份脚本应准备就绪。如果你使用的是 `v 8.3` 格式，则不需要数据库转换。如果你使用的是早于 `v 8.2` 的版本，为了安全，使用二进制文件创建一个新的 `v 8.3` 数据库。这两种方法都有保障。

- **问：我知道 `4GL` 支持 Windows 下的图形化编程，Progress 支持 Linux 客户端。我可以在 Windows 下编程吗？**
  **答：** 是的，但仅限 Progress V7 版本支持 Windows 原生（也就是说，使用 SCO 二进制文件）。在构建 Windows 环境时，市场团队审查发现许可证数量较小。随着时间的推移，支持 Windows 的能力增长。无论如何，请联系您的 Progress 销售代表并表达对支持 Windows 的兴趣。

- **问：我听说镜像（after-imaging）会消耗性能。我真的需要它吗？反正我每天备份数据库。**
  **答：** 镜像将节省你的时间。运行镜像允许将数据库恢复到崩溃前一分钟的状态。即使你每天备份整个系统，如果你不运行镜像，你整天的工作都会丢失。始终要问：“我能承受自上次备份以来的数据丢失吗？”24x7 和其他关键系统认为数据丢失是可以接受的。

- **问：Progress 文档说即使我只有运行时客户端，也可以通过 Dictionary 管理数据库。我如何进入 Dictionary？**
  **答：** Dictionary 代码以源码形式提供。只需使用 `-tx` 参数启动你的 Progress 会话即可。

- **问：当我启动 Progress 会话时，它显示“This Version Of Progress Requires A Startup Procedure”。是怎么了？**
  **答：** 有几种可能。这发生在你启动了 Progress 会话并尝试进入 Procedure Editor 时。Client/Networking 产品旨在运行编译代码或源码。如果你购买了这些产品之一但消息仍然出现，检查 `$DLC` `$PROCFG` 变量是否存在错误。损坏的 `progress.cfg` 文件也会导致此问题，以及会话启动参数 `-tr`。

## 在 Linux 上安装和管理 Progress • 第 8 章 355

## Linux 上的 PostgreSQL

本章的解决方案：

- 安装
- 配置
- 问题
- 故障排除

## 引言

世界上每台计算机系统都需要数据库来存储和检索信息。你使用计算机的主要目的是存储、检索和处理信息，并快速完成所有操作，从而为你节省时间。同时，系统必须简单、健壮、快速、可靠、经济且易于使用。数据库是最重要的系统，因为它存储了每个公司的关键信息。电信、汽车、银行、航空等行业如果没有数据库将无法高效运行。最流行的数据库系统基于国际标准组织 (`ISO`) SQL 规范和 `ANSI SQL`（美国）标准。用户希望使用 SQL, `ODBC`、`JDBC` 开发一次应用程序，然后自由地部署到所有数据库系统中。

`PostgreSQL` 是世界上最先进的开源对象关系数据库。`PostgreSQL` 最初在伯克利大学计算机科学系开发，开创了许多对象关系概念。它提供 `SQL92/SQL3` 语言支持、事务完整性、自定义函数、存储过程、触发器和类型扩展性。`PostgreSQL` 是这段原始代码的免费开源后代。数百万 `PostgreSQL` 数据库被安装为数据库服务器、Web 服务器和应用程序服务器。这是一个非常复杂的对象关系数据库系统 (`ORDBMS`)。

`PostgreSQL` 运行在 `Solaris`, `SunOS`, `HPUX`, `AIX`, `Linux`, `Irix`, `Digital Unix`, `BSDi`, `FreeBSD`, `SCO UNIX`, `NEXTSTEP`, `Solaris` 以及几乎所有的 Unix 版本。使用 Cygnus `cywin32` 包完成了到 Microsoft Windows NT 的移植。

- 标题：PostgreSQL RDBMS 数据库（对象关系数据库管理系统）
- 当前版本：7.0
- 年龄：自 1985 年开始开发，PostgreSQL 现在已有 15 年历史了。
- 作者：在过去的 15 年里，互联网上大学和公司的数百万人员开发了 PostgreSQL。

`MySQL` 是另一个开源准商业数据库系统，但它支持事务等重要功能。

## PostgreSQL

互联网起源于一个防御项目，后来变得非常广泛，连接了居住在地球各大洲的人们。这促进了全球范围内信息、智能思想和研究课题的快速交流。结果是，互联网成为了世界最大的软件“生成器”。软件开发方法从闭源转变为开源，而互联网促进了这种系统的产生。

互联网被用于创建 Linux 操作系统，它变得极其受欢迎。随着 Linux 的成功，许多人决定在计算机应用程序（如数据库系统、电子表格等）上继续延续这一理念。互联网上的开发者们并没有从零开始构建系统，而是利用了加利福尼亚大学的公有领域 Postgres，并对其进行修改和增强，最终形成了 PostgreSQL。

互联网是驱动 PostgreSQL 的真正引擎。物理学和统计学规律也部分归功于 PostgreSQL 的成功——它们青睐像 PostgreSQL 和 Linux 这样的源码系统。随着互联网速度每天都在提高，互联网变得越来越可靠，开源代码系统将产生非常迅速的动力。通过将统计学、数学和科学原理应用于软件质量，你只有在 PostgreSQL 这样的开源代码系统中才能获得质量最好的软件，因为其源代码对互联网这条“信息高速公路”开放。参与代码工作的人越多，软件质量就越好。开源代码大大减少了重复劳动，降低了开发成本，节省了发布时间，并遵循优化国家和全球资源的现代经济法则。一旦他人生产了软件包，你就不需要浪费宝贵的时间去重复已经做得很好的东西。

由于 PostgreSQL 遵循开源代码开发模型，你可以获得许多特性。互联网上的软件开发速度非常快，因为一个极其巨大的计算机和人员网络参与了其中。未来趋势表明，大多数软件开发将发生在遍布全球的信息高速公路上。在未来几年里，互联网将出现爆炸式增长，这将进一步加速行业对 PostgreSQL 的采用。

由于在过去的 15 年里已经在 PostgreSQL 上投入了大量工作，因此从头开始创建一个另一个满足 `ANSI/ISO SQL` 的数据库系统是没有意义的。利用现有代码为 PostgreSQL 添加缺失的功能或增强，并立即开始使用它，将是一个巨大的优势。

预计对 PostgreSQL 等互联网产品的需求将呈指数级增长，因为它能够保持高质量、低成本以及极其庞大的用户和开发者群体。不使用互联网的国家将严重错过全球互联网革命，并被其他国家远远，因为互联网本身就是世界最大的“软件公司”。

# 获取 PostgreSQL

如果你计划在 Linux 操作系统上使用 PostgreSQL，可以购买 Red Hat Linux CD-ROM、Debian CD-ROM 或 Slack Linux CD-ROM，它们已经包含了以包形式存在的 PostgreSQL（包括源码和二进制文件），你也可以从这些网站之一在线购买：

- Linux Systems Labs: http://www.lsl.com/
- Red Hat: http://www.redhat.com/
- Cheap Bytes Inc.: http://www.cheapbytes.com/
- Debian: http://www.debian.org/vendors.html

PostgreSQL 组织也出售 PostgreSQL CD-ROM，其中包含了许多 UNIX 操作系统的完整源代码和二进制文件，以及完整的在线文档：

- 来自主站的 PostgreSQL CD-ROM：http://www.postgresql.org

如果你想从互联网下载，请访问以下站点：

- PostgreSQL 源码 `RPM` 和二进制文件 `RPM`：http://www.ramifordast.net/postgres
- PostgreSQL `RPM` 的维护者是 Lamar Owen：amar.owen@wgrcr
- PostgreSQL 源码 `RPM` 和二进制文件 `RPM`：http://www.postgresql.org
- 点击 Latest News（最新新闻）并点击 Red Hat `RPMs`。
- PostgreSQL 源码 `RPM` 和二进制文件 `RPM`：http://www.redhat.com/pub/contrib/i386/
  - FTP 站点：ftp://ftp.redhat.com/pub/contrib/i386/
- Solaris、HPUX、AIX、IRIX 和 Linux 的二进制站点：ftp://ftp.postgresql.org/pub/bindist

# PostgreSQL 快速安装说明

尽管 PostgreSQL 是世界上最先进、最复杂的数据库系统，但安装 PostgreSQL 并不复杂，事实上，使用二进制 `RPM` 安装只需不到五分钟。PostgreSQL 极少需要 40MB 磁盘空间和 8MB 内存。但现在，即使是低价 PC 系统也配备了 10GB 硬盘和 64MB 内存。本节为你提供了安装过程的概览。如果你有一定的 Linux 和 Red Hat `RPM` 包经验，只需按照以下步骤几几分钟内完成 PostgreSQL 安装。如果你是 Linux/UNIX 新手，请将本节与下一节“详细说明”交叉引用，该节将详细解释每一步。

在 Red Hat Linux 系统上，使用以下步骤。在 Debian Linux 上，步骤类似，但将 `.rpm` 替换为 `.deb`。在 Debian Linux 上，如果你没有 PostgreSQL 包，则可以使用 `rpm2deb` 程序将 Hat PostgreSQL `RPM` 包转换为 Debian 包。

以 `root` 身份登录并在 `bash` 提示符下输入以下命令：

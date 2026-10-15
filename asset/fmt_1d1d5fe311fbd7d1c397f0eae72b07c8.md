
# Linux Web Hosting：WebSphere、DB2 和 Domino (IBM Redbooks)

**Budi Darmawan**
**Alistair le Roux**
**Yu-Phing Ong**
**Iwan Setiawan**

# 前言

本红书旨在帮助 Web 服务器管理员利用 IBM 软件，以 Linux 为基础操作系统构建并管理服务器。假设读者具备基本的管理技能，理解通 HTML 语法，并熟悉 Java 编程。因此，本红书并不提供关于 Linux 或 Linux 上的 IBM 软件的基础安装和配置信息。

本红书采用的方法是以 IBM 软件作为案例研究，在 Linux 上创建一个 Web 服务器。我们构建的 Web 服务器是一个自定义的 IBM Redbook 主页，我们使用了以下工具：

- Linux，使用 RedHat 版本 6.2 和 Caldera eDesktop 2.4
- IBM HTTP Server 版本 1.3.6
- IBM Database 2 (DB2) 版本 6.1 带有 FixPack 3
- IBM WebSphere Application Server 版本 2.03
- Lotus Domino Server 版本 5.03

我们讨论的话题包括：

- 使用 Java Server Pages (JSP)、Servlet 和 Java Bean 创建动态 Web 页面
- 通过 DB2 接口提供动态用户和用户配置管理
- 使用 DIIOP/CORBA 接口集成对 Lotus Domino 数据库的访问
- Web 服务器的操作

# 编写本红书的团队

本红书由来自奥斯汀国际技术支持组织（International Technical Support Organization, Austin Center）的全球专家团队制作。

**Budi Darmawan** 是奥斯汀国际技术支持组织的系统专家。他在全球范围内针对数据库、编程和系统管理的所有领域进行 IBM 和 Tivoli 的写作和教学。在加入 ITSO 之前，他在 IBM 印度尼西亚担任服务团队方案架构师。他在 OS/390 和分布式系统的数据库及通用系统管理领域工作了多年。他目前感兴趣的是 Tivoli 系统管理软件以及 Web 和 Java 编程。

**Alistair le Roux** 是南非的高级工程师（CE）。他在 IBM RS/6000 硬件和 AIX 方面有两年经验。他的兴趣领域包括 Linux、AIX、DB2 和电子商务产品。这是他的第一本 Redbook。

**Yu-Phing Ong** 是 IBM 澳大利亚的高级软件专家。他在数据库、商业智能和电子商务领域拥有六年的 IBM 经验。他的专长包括 WINTEL、Unix 和编程。他在红书和认证指南中编写了大量关于 DB2 和 Net.Commerce 的文章。

**Iwan Setiawan** 是印度尼西亚 PT Sistindo Mitralintas 的系统工程师。他在网络领域有三年的经验。他拥有印度尼西亚大学的物理学学位。他的专长包括 Linux 和 Windows NT 系统管理。

感谢以下人员对本项目做出的无私贡献：

- John Owczarczak，国际技术支持组织，奥斯汀中心
- Catherine A. Webb，IBM 集成解决方案 PDT 负责人

## 您的意见对我们非常重要！

我们希望我们的 Redbooks 尽可能提供帮助。请通过以下方式之一就本红书或其他红书发送意见：

- 填写第 229 页“IBM Redbooks 评审”中的评估表，并传真至表格所示传真号码。
- 使用位于 `http://www.redbooks.ibm.com/` 上的在线评估表。
- 通过电子邮件向 `redbooks@us.ibm.com` 发送您的意见。

# 第 1 章 项目介绍

在本章中，我们讨论了整个项目的背景信息。讨论分为以下几节：

- 1.1 节“Linux 与 IBM”显示了 IBM 对 Linux 作为受支持操作系统之一的承诺。
- 1.2 节“电子商务模式”展示了使用模式作为基本单元在企业内部构建电子商务的结构化方法。
- 1.3 节“网络上的企鹅”提供了本红书和项目的背景信息。
- 1.4 节“文档组织”提供了红书的整体文档结构和扩展目录。

## 1.1 Linux 与 IBM

正如 Linux at IBM 网站 `http://www.ibm.com/linux` 所示，IBM 致力于将 Linux 作为客户操作系统选项之一——我们将这一承诺扩展到对开源操作系统 Linux 的支持。为了满足这一动态操作系统日益增长的需求，我们提供了最全面的硬件、软件和支持解决方案。Linux 用户可以利用 IBM 丰富的经验、技能和资源来解决技术需求。需要 Linux 支持的客户可以联系 IBM 全球服务处理所有 Linux 支持需求，从咨询和协助到运营支持服务。客户可以拨打 24 小时电话热线或访问在线帮助中心以获得 Linux 支持。

目前已有多种 IBM 产品可在 Linux 上使用。许多其他 IBM 产品正在进行 Linux 的 Beta 测试。IBM 与 Linux 发行版的关键联盟包括：

- Caldera 联盟
- Red Hat
- Turbo Linux
- SuSE

然而，由于某些产品的可用性有限，我们仅在 RedHat 6.2 版本和 Caldera eDesktop 2.4 版本对场景进行了测试。

## 1.2 电子商务模式

电子商务模式旨在为构建电子商务系统提供一种快速可用的设计模式，包括系统架构和指南。这些模式被归类在以下方案中：

- 用户到业务
- 用户到在线购买
- 业务到业务 (B2B)
- 用户到数据
- 用户到用户
- 应用程序集成

有关这些电子商务模式的更多信息，请参阅 IBM developerWorks 网站：`http://www.ibm.com/software/developer/web/patterns`。

我们选择实现这些模式中最常见的子集，即“用户到在线购买”，它是“用户到业务”模式的子集。我们选择的应用程序拓扑是 Web-ub 方案，这意味着我们在 Web 服务器中从零创建应用程序，而不进行后端集成。图 1 显示了该模式的理想运行时拓扑。

在图 1 中，企业的电子商务系统跨越了非军事化区（DMZ）到企业内部网络。以下组件构成了“用户到在线购买”模式的电子商务解决方案：

- **协议防火墙**：过滤掉不需要的有害协议包。它只允许入站请求进入特定机器和特定端口。
- **请求分发器**：充当多个 Web 服务器系统的负载均衡。它将请求路由到特定的 Web 服务器以促进整体负载平衡，从而提高整体吞吐量。
- **商务服务器**：是带有应用程序服务器的 Web 服务器，处理来自互联网的 HTTP 请求。
- **域防火墙**：通过仅允许 DMZ 中的某些机器向内部网络发送数据包来保护内部网络。
- **DB 服务器**：为 Web 应用程序提供数据库支持。数据库数据被认为是安全的，因为它同时受到协议防火墙和域防火墙的保护。

| 外部世界 | 非军事化区 (DMZ) | 内部网络 |
| :--- | :--- | :--- |
| 购物者不在此完成订单 | Web 服务器 | 应用程序节点 |
| 零售客户互联网 | 商务服务器节点 | 应用程序节点 |
| | Web 服务器到后端的（可选） | 应用程序节点 |
| | DB 服务器节点 | 数据库 |
| | 静态页面 - 促销 | 内容管理节点 |

**图 1. 用户到在线购买的运行时拓扑**

电子商务模式还包括产品选择。然而，目前产品选择中没有选项；因此，我们必须定义产品选择。我们在商务节点中实现了 `IBM HTTP Server` 和 `WebSphere Application Server`；而在 DB 服务器上，我们放置了 `IBM DB2` 和 `Lotus Domino`。为了简单起见，我们没有实现分发器。

关于“用户到业务”和“用户到在线购买”模式及其指南的深入信息，请参考《电子商务模式：使用 WebSphere Advanced 版的拓扑 1 和 2》。

## 1.3 网络上的企鹅

本红书是根据奥斯汀的一个项目制作的。红书旨在展示使用 Linux 作为操作系统为通用 Web 托管和电子商务提供高级平台的能力。我们采取的方法实际上是在 Linux 上构建一个提供示例电子商务功能的 Web 服务器。我们使用的 Linux 发行版是 RedHat 6.2 版本和 Caldera eDesktop 2.4 版本。该项目使用的软件包括：

- IBM WebSphere 2.0 版本
- IBM HTTP Server 1.3 版本
- IBM Database 2 (DB2) 6.1 版本
- Lotus Domino 5.0 版本

该项目进一步扩展，以提供有关操作 Linux 服务器的一些考虑。考虑涵盖了从日常 Linux 操作到管理 Web 服务器可能需要执行的特定任务。我们选择提供的示例应用程序是一个自定义的 Web 网站。我们提供的 Web 应用程序包含：

- 使用 DB2 的动态管理
- 使用 Servlet、Java Server Page (JSP) 和 Java Bean 的动态页面
- 使用 WebSphere Application Server 的 Servlet 管理
- 访问 Lotus Domino 数据库
- 动态用户管理等

将上述功能整合在一起展示了我们遇到的许多互操作性问题。但构建一个运行的解决方案本身也是一项任务。

## 1.4 文档结构

本红书旨在为使用 Linux 服务器和 IBM 产品的管理员提供使用和管理信息。我们不涵盖产品的基本安装。假设读者具备基础 HTML 技能、Java 编程和 Linux 管理知识。本文包含以下章节：

- 第 1 章，“项目介绍”，提供了项目的背景信息。
- 第 2 章，“设置与配置”，提供了我们执行的安装过程概述。安装过程大多是简述的，但产品工作所需的特定任务除外。
- 第 3 章，“构建 Web 服务器”，讨论了我们构建 Web 服务器的步骤。本章讨论了我们使用的编程结构和构建的代码。涵盖的技术包括：
  - 使用 JDBC 访问 DB2
  - 使用 JDBC 访问 Domino
  - 通用访问
  - Java Server Page 实现
  - Java Bean 编程
- 第 4 章，“操作考虑”，展示了确保 Web 服务器运行可能执行的一些基本操作。这里讨论的操作是设施的基本启动和停止、常规维护以及一些监控和故障排除技巧。
- 第 5 章，“扩展案例”，讨论了一些可以实现但由于时间或产品限制尚未实现的内容。

我们提供的附录包含了整个项目中使用的各种源代码和 HTML 文件。我们还提供了一个光盘，包含了所有使用的 Java 文件、脚本、HTML 文件和 JSP 文件的源代码。使用光盘请参考附录 F，“使用材料”。

# 第 2 章 设置与配置

本章包含了实施场景时执行的基本设置和配置任务。我们讨论的项目包括：

- 2.1 节“系统配置”，展示了我们在环境中所使用的系统配置。
- 2.2 节“安装概述”，提供了整体设置和配置任务的概述。
- 2.3 节“Linux 设置”，讨论了设置 Linux 系统涉及的问题，包括硬件要求、磁盘分区方案以及对 RedHat 和 Caldera 的实际考虑。
- 2.4 节“应用程序安装”，展示了本项目中使用的 IBM 软件的安装和配置。

我们使用 `bstest1` 和 `bstest2` 作为前端 Web 服务器，即与世界的接口。所有的应用程序数据都存储在 `bstest3` 中，那里运行着 Domino 和 DB2 数据库。前端服务器使用了 Caldera eDesktop 版本 2.4 和 RedHat 版本 6.2，而后端服务器我们仅使用 RedHat 版本 6.2。

我们使用的机器是 IBM Netfinity 3000 系统。这些 Netfinity 3000 系统具有以下规格：

- 型号：8476-2U
- Flash EEPROM 级别：NTKT29AUS
- BIOS 日期：02/10/00
- 处理器：Pentium II 350/100 MHz
- 内存：192MB
- SCSI：Adaptec AHA 2940 uWB Bios 1.32S8
- 磁盘：8 GB
- 视频适配器：S3 Trio3D 4 MB RAM
- 网络：IBM PCI Token Ring 卡

## 2.2 安装概述

本节提供了用于安装系统的系列全局步骤。在本节中列出的步骤既可以概述，也可以作为执行安装的检查清单。有关每个步骤的详细讨论将在后续章节中提供。

我们首先介绍后端服务器的步骤，确保数据库可以访问，然后是前端服务器的步骤，最后验证前端服务器可以访问后端数据库。

### 2.2.1 后端服务器安装

后端服务器安装步骤如下：

1.  准备硬件并确保它满足所有将用软件的配置要求。
2.  安装我们选择的 Linux 发行版。
    - 将 userID `admin` 添加为普通用户。
    - 熟悉首选的 X-Window 环境：KDE 或 GNOME。
3.  安装 DB2
    - 安装 DB2，以 `root` 用户身份登录。
    - 对于 RedHat 安装，安装 `pdksh` 的 rpm 包以便 DB2 安装程序运行。
    - 在安装过程中，创建默认 DB2 实例和 DB2 管理服务器实例。
    - 通过以用户 `db2inst1` 登录并创建并访问示例数据库来验证 DB2 安装。
4.  从控制台安装 Domino 服务器。
    - 安装 Domino，以 `root` 用户身份登录。
    - 停止 `http`、`mail` 和其他服务以防止与 Domino 冲突。
    - 安装后，以 `notes` 用户 ID 登录，从 Domino 数据目录运行 `httpsetup` 命令，并使用 Web 浏览器运行 Domino 服务器的管理配置。
    - 从 Domino 数据目录运行 `server` 命令并使用 Web 浏览器测试 Domino 服务器的安装。
    - 验证 HTTP、DIIOP 和 Java 组件在 Domino 服务器中运行。
    - 使用 Domino 管理器客户端或 Web 管理来配置 Domino，例如 CORBA 访问、HTTP 端口等。确保 Domino 服务器配置了正确的完全限定 Internet 主机名。
    - 使用 Web 浏览器测试新配置。

### 2.2.2 前端服务器安装

前端服务器安装步骤如下：

1.  准备硬件并确保它满足所有将用软件的配置要求。
2.  安装选择的 Linux 发行版。
    - 将 `admin` 名称添加为普通用户。
    - 熟悉首选的 X-Window 环境：KDE 或 GNOME。
3.  安装 Java，我们使用了 `IBM JDK 1.1.8`。
    - 安装 Java，以 `root` 用户身份登录。
    - 对于 Caldera 安装，移除旧的 Java 版本。
    - 安装后，导出 `JAVA_HOME` 环境变量。
4.  安装 IBM HTTP Server 1.3.6
    - 安装 IBM HTTP Server，以 `root` 用户身份登录。
    - 移除任何其他 Web 安装，例如 Apache 及其相关依赖。
    - 安装后，修改运行级别以使 IBM HTTP Server 在重启动时启动。重启服务器。此时 IBM HTTP Server 守护进程将正常启动。
    - 使用 Web 浏览器测试 IBM HTTP Server。
5.  安装 WebSphere 2.0.3
    - 安装 WebSphere，以 `root` 用户身份登录。
    - 确保已设置 `JAVA_HOME` 环境变量。
    - 安装核心和特定 Web 服务器的 WebSphere rpm 包。
    - 对于 JSP，将 `pagecompile` 目录的所有者更改为用户 `nobody`。
    - 修改并验证各种 IBM HTTP Server 和 WebSphere 配置文件。
    - 重启 IBM HTTP Server。这将加载并运行 WebSphere。
    - 使用 Web 浏览器测试 WebSphere 是否运行了 `snoop` Servlet，以及 `localhost` 端口 `9527` 是否有 WebSphere 管理。
6.  配置对后端数据库的访问
    - 安装 DB2 客户端启用器 (CAE) 并创建带有 Java 支持的默认 DB2 实例。
    - 验证与后端服务器示例数据库的连接性。
    - 修改 `bootstrap.properties` 文件和 `ibmhttpd` 启动脚本以访问 DB2。
    - 重启 WebSphere 和 IBM HTTP Server，然后测试 DB2 到示例数据库的连接。
    - 从后端服务器拷贝 `NCSO.jar` 文件。
    - 修改 WebSphere `bootstrap.properties` 文件以访问 Domino 服务器。
    - 重启 WebSphere 和 IBM HTTP Server，然后测试 Domino 到示例数据库的连接。

## 2.3 Linux 设置

本节涵盖前端服务器的设置。本节详细介绍了安装系统的全局步骤。

### 2.3.1 磁盘分区

前端服务器安装步骤为：

1.  准备硬件并确保它满足所有将用软件的配置要求。

（根据文本流，此节关注下面的设置步骤）。

### 2.3.2 RedHat 安装

前端服务器安装步骤为：

1.  准备硬件并确保它满足所有将用软件的配置要求。
2.  安装选择的 Linux 发行版。
    - 将 `admin` 名称添加为普通用户。
    - 熟悉首选的 X-Window 环境：KDE 或 GNOME。
3.  安装 Java，我们使用了 `IBM JDK 1.1.8`。
    - 安装 Java，以 `root` 用户身份登录。
    - 对于 Caldera 安装，移除旧的 Java 版本。
    - 安装后，导出 `JAVA_HOME` 环境变量。
4.  安装 IBM HTTP Server 1.3.6
    - 安装 IBM HTTP Server，以 `root` 用户身份登录。

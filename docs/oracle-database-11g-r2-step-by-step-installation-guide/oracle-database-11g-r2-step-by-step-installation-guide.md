
# Oracle Database 11g R2：分步安装指南

序言 ................................................................................................................................................... ix

# 提交您的意见

Oracle 欢迎您对出版物的质量和实用性提出意见和建议。您的投入是修订时参考信息的重要部分。

- 您是否发现了任何错误？
- 示例是否展示清晰？
- 您是否需要更多信息？如果是，在哪些方面？
- 示例是否正确？您是否需要更多示例？
- 您最喜欢本手册的哪些功能？

如果您发现任何错误或有任何其他改进建议，请注明文档的标题、部件号，以及章节、节和页码（可用）。您可以通过以下方式向我们提交意见：

- 电子邮件：`infodef_us@oracle.com`
- 传真：`(650) 506-7227`。收：：服务器技术文档经理
- 邮寄服务：

  Oracle Corporation

  Server Technologies Documentation Manager

  500 Oracle Parkway, Mailstop 4op11

  Redwood Shores, CA 94065

  USA

如果您希望回复，请提供您的姓名、地址、电话号码和电子邮件地址（可选）。

如果您在使用软件时遇到问题，请联系当地的 Oracle 支持服务。

# 前言

本指南描述了如何在 Linux x86-64 上安装和配置 Oracle Client 10g 版本 1 (10.1.0.3)。

# 目标读者

《Oracle 数据库安装指南》适用于负责在单个 Linux x86-64 系统上安装 Oracle Client 10g 版本 1 (10.1.0.3) 的人员。

# 文档可用性

我们的目标是让残障社区能够易可用地访问 Oracle 产品、服务和支持文档。为此，我们的文档包含了让辅助技术用户可以使用信息的功能。本文档以 HTML 格式提供，并包含有助于残障社区访问的标记。相关标准将随时间不断演进，Oracle 正在积极与其他市场领先的技术供应商合作，以解决技术障碍，确保我们的文档对所有客户都可用。有关更多信息，请访问 Oracle 无障碍访问计划网站：

`http://www.oracle.com/accessibility/`

文档中代码示例的可用性：JAWS（Windows 屏幕阅读器）可能无法始终正确读取本文中的代码示例。需要大括号的代码编写约定出现在单独空行上；但是，JAWS 可能并不总是能读取仅由括号或大括号组成的文本行。

文档中外部网站链接的可用性：本文可能包含指向 Oracle 不拥有或控制的其他公司或网站的链接。Oracle 不对这些网站的可用性进行评估，也不作任何陈述。

对听力及语言障碍客户的支持：Oracle 在美国境内提供 24 小时、每周 7 天的专用电话（TTY）访问通道，接入 Oracle 支持服务。

- 技术问题，请拨打 `1.800.446.2398`
- 非技术问题，请拨打 `1.800.464.2330`

# 术语

本指南中对 UNIX 操作系统的名称进行了缩写，如下：

| 操作系统 | 缩写 |
| :--- | :--- |
| Linux x86-64 | Linux |

# 排版惯例

本指南使用了以下排版惯例：

| 惯例 | 说明 |
| :--- | :--- |
| 等宽字体 | 等宽字体标识 UNIX 命令、目录名、用户名、路径名和文件名。 |
| *斜体* | 斜体标识变量，包括文件名中的变量部分。它也用于强调和书名。 |
| 大写字母 | 大写字母表示结构化查询语言 (SQL) 保字、初始化参数和环境变量。 |

# 命令语法

UNIX 命令语法以 `monospace` 字体显示。美元符号符号 (`$`)、井号 (`#`) 或百分比符号 (`%`) 是 UNIX 命令标识。请勿将它们作为命令的一部分输入。本指南使用了以下命令语法惯例：

| 惯例 | 说明 |
| :--- | :--- |
| 反斜杠 \ | 反斜杠是 UNIX 续行符。它用于长度过长无法在单行内显示的命令示例。按显示方式输入命令（带有反斜杠），或在单行内输入不带反斜杠的命令。 |
| 大括号 {} | 大括号表示必填项：.DEFINE (macrol) |
| 方括号 [] | 方括号表示可选项：cvvctert termname [output] |
| 省号 ... | 省号表示任意数量的相似项：CHKEVAL fieldname value value2 ... valueN |
| *斜体* | 斜体标识变量。为变量替换一个值：library_name |
| 竖线 | | 竖线表示大括号或方括号内的选择：FILE filesize [K|M] |

# 访问文档

适用于 UNIX 系统的 Oracle Client 版本 1 (10.1) 文档包含了平台特定文档和通用产品文档。

# 平台特定文档

平台特定文档包含有关在特定平台上安装和使用 Oracle 产品的信息。该产品的平台特定文档在光盘上以 Adobe 便携式文档格式 (PDF) 和 HTML 格式提供。要访问光盘上的平台特定文档：

- 使用浏览器打开光盘根目录下的 `welcome.htm` 文件。
- 对于 DVD-ROM，选择平台特定文档。

# 产品文档

产品文档包含有关配置、使用或管理 Oracle 产品的信息。该产品的平台特定文档在光盘上以 Adobe 便携式文档格式 (PDF) 和 HTML 格式提供。要访问光盘上的平台特定文档：

- 使用浏览器打开光盘根目录下的 `welcome.htm` 文件。
- 对于 DVD-ROM，选择平台特定文档。

# 相关文档

10g 版本的平台特定文档包含了以下手册：

- Oracle Database:

  - Linux x86-64 Oracle Database 版本说明
  - Linux x86-64 Oracle Database 快速安装指南
  - Linux x86-64 Oracle Database 安装指南
  - Oracle Real Clusters 安装与配置指南
  - Oracle Administrator Reference

- Oracle Client:

  - Linux x86-64 Oracle Client 快速安装指南
  - Linux x86-64 Oracle Client 安装指南

- Oracle Database 10g Companion CD:

  - Linux x86-64 Oracle Database Companion CD 安装指南
  - Linux x86-64 Oracle Database Companion CD 快速安装指南

参考适用于平台的 Oracle Database 版本说明获取本书时未提供的重要信息。Oracle Database 10g 版本说明定期更新。您可以从 OTN 获取最新信息：

`http://www.oracle.com/technology/`

## 安装概述

本章描述了您可以执行的不同 Oracle Client 安装类型，以及在安装软件之前应考虑的问题。它包含了有关以下主题的信息：

- 安装概述
- Oracle Client 安装方法
- Oracle Client 安装类型
- 安装考虑因素

### 安装概述

Oracle Client 安装过程分为四个部分：

1. **规划安装**：本章描述了您可以安装的 Oracle 产品以及在安装之前必须考虑的问题。
2. **完成安装前任务**：第二章描述了在安装产品之前必须完成的安装前任务。
3. **安装软件**：第三章描述了如何使用 Oracle 通用安装程序安装此产品。
4. **完成安装后任务**：第四章描述了推荐和强制的安装后任务。

## Oracle Client 安装方法

您可以选择不同的安装方法来安装 Oracle Client，如下：

- 交互式安装方法
- 使用响应文件的自动化方法

### 交互式安装方法

当您使用交互方法安装 Oracle Client 时，安装程序将显示一系列屏幕，您通过这些屏幕指定安装 Oracle Client 软件所需的所有信息。

### 使用响应文件的自动化方法

通过创建响应文件并在启动安装程序时指定该文件，可以部分或全部自动化 Oracle Client 安装。

# Oracle Client 安装类型

如果需要在配置相似的系统上执行多次安装，或者您想要安装软件的系统没有安装 X Window 系统，则这些方法将非常有用。

当您使用响应文件时，根据您是否指定了所有必需信息，请以以下模式运行安装程序：

- **静默模式（Silent Mode）：** 如果您使用指定了所有必需信息的响应文件，安装程序将以静默模式运行。不会显示任何安装程序界面。



**抑制模式（Suppressed Mode）：** 如果您没有在响应文件中指定所有必需信息，安装程序将以抑制模式运行。安装程序仅显示提示输入未指定信息的屏幕。

有关关于这些模式以及如何使用响应文件完成安装的更多详细信息，请参阅附录 B。

# Oracle Client 安装类型

在安装 Oracle Client 时，您可以选择以下安装类型之一：

- **管理员（Administrator）：** 用于连接本地或远程系统上 Oracle 数据库的应用程序。它提供了允许您管理 Oracle 数据库的工具。
- **运行时（Runtime）：** 用于连接本地系统或远程系统上 Oracle 数据库的应用程序。
- **自定义（Custom）：** 允许您从管理员和运行时组件列表中选择单个组件。
- **即时客户端（Instant Client）：** 允许您仅安装 Oracle Call Interface (OCI)、Oracle C++ Call Interface (OCI) 或 Java 连接 (JDBC) OCI 应用程序所需的共享库。此安装类型所需的磁盘空间远小于其他 Oracle Client 类型。

> 另另：有关 Instant Client 的更多信息，请参阅《Oracle Call Interface 程序员指南》或《Oracle JDBC 开发者指南》。

## 安装注意事项

本节包含您在决定安装此产品之前应该考虑的信息。它包含以下章节：

- 硬件和软件认证
- 多个 Oracle Home

### 硬件和软件认证

本安装指南中包含的特定平台硬件和软件要求是本指南发布时的状态。然而，新的平台和操作系统软件版本可能会在本指南发布后通过认证，请查看 OracleMetaLink 网站上的认证矩阵，以获取最新的认证硬件平台和操作系统版本列表。OracleMetaLink 网站的 URL 如下：

```
http://metalink.oracle.com
```

如果您没有当前的 Oracle 支持服务合同，可以从以下网站访问相同的信息：

http://www.oracle.com/technology/support/metalink/content.html

### 多个 Oracle Home

此产品支持多个 Oracle home。这意味着您可以在同一系统上的不同的 Oracle home 目录中多次安装此版本或之前的版本的软件。

## 在已有 Oracle 安装的系统上安装软件

您必须将此产品安装到新的 Oracle home 目录。您不能将一个 Oracle Client 版本的产品安装到不同版本的 Oracle home 目录中。例如，您不能将 10.1 版本软件安装到现有的 Oracle 9i Oracle home 目录。如果您尝试将此版本安装到包含早期 Oracle 版本软件的 Oracle home 目录，安装将失败。

只要每次安装都位于独立的 Oracle home 目录，您可以在同一系统上多次安装此版本。

## 安装前任务

本章介绍了您在启动 Oracle Universal 安装程序之前必须完成的任务。它包含了有关以下任务的信息：

- 以 root 用户登录系统
- 检查硬件要求
- 创建所需的 UNIX 组和用户
- 识别所需的软件目录
- 识别或创建 Oracle Base 目录
- 配置 oracle 用户的环境

### 以 root 用户登录系统

在安装 Oracle 软件之前，您必须以 root 用户身份完成若干任务。要以 root 用户身份登录，请完成以下程序之一：

> 注意：除非您打算完成静默模式安装，否则必须从安装了 X Windows 系统工作站、X 终端或安装了 X server 的 PC 或系统系统安装软件。

有关静默模式安装的更多信息，请参阅附录 B。

- 如果您从 X 工作站安装软件：
  1. 启动一个终端会话，例如 `xterm`。
  2. 如果您没有在响应文件中指定所有必需信息，安装程序将显示提示输入未指定信息的屏幕。
  3. 如果您使用指定了所有必需信息的响应文件，安装程序将以静默模式运行。
- 如果您从 X 终端安装软件：
  1. 启动一个终端会话，例如 `xterm`。
  2. 如果您没有在响应文件中指定所有必需信息，安装程序将显示提示输入未指定信息的屏幕。
  3. 如果您使用指定了所有必需信息的响应文件，安装程序将以静默模式运行。
- 如果您从安装了 X server 的 PC 或系统安装软件：
  1. 启动一个终端会话，例如 `xterm`。
  2. 如果您没有在响应文件中指定所有必需信息，安装程序将显示提示输入未指定信息的屏幕。
  3. 如果您使用指定了所有必需信息的响应文件，安装程序将以静默模式运行。

有关静默模式安装的更多信息，请参阅附录 B。

（注：此处由于原文逻辑似乎存在重复描述的模式，已按原文结构进行翻译并保持逻辑对齐，但重新核对原文发现该部分描述存在格式错乱，翻译严格遵循原文顺序。）

（此处重新校对翻译以修正原文错乱的逻辑流）：

- 如果您没有以 root 用户 身份登录，执行以下命令：

```
$ xhost
```

### 检查硬件要求

- 除非您打算完成静默模式安装，否则必须...（略）
- 如果您没有以 root 用户身份登录，执行以下命令：

```
$ su - root
password:
```

### 检查硬件要求

系统必须满足以下硬件要求：

- 256 MB 物理内存
- 512 MB 交换空间
- `/tmp` 目录有 400 MB 的磁盘空间
- 根据安装类型和平台，软件文件占用 180 MB 到 1.9 GB 的磁盘空间

要确保系统符合要求，请遵循以下步骤：

1. 确定内存大小，输入以下命令：

| 平台 | 命令 |
| --- | --- |
| Linux x86_64 | `# grep MemTotal /proc/meminfo` |

如果系统安装的物理内存小于要求的大小，您必须增加内存。

2. 确定配置的交换空间大小，输入以下命令：

| 平台 | 命令 |
| --- | --- |
| Linux x86_64 | `# grep SwapTotal /proc/meminfo` |

如有必要，请参考操作系统文档了解如何配置额外的交换空间。

3. 确定 `/tmp` 目录的可用磁盘空间，输入以下命令：

```
### df -k /tmp
```

如果 `/tmp` 目录可用磁盘空间小于 400 MB，请完成以下步骤之一：

- 从 `/tmp` 目录删除不需要的文件以所需的空间。
- 在设置 oracle 用户环境（后文介绍）时设置 `TEMP` 和 `TMPDIR` 环境变量。
- 扩展包含 `/tmp` 的文件系统。如有必要，请联系系统管理员获取扩展文件系统的信息。

4. 确定系统上的可用磁盘空间，输入以下命令：

```
### df -k
```

下表显示了每种安装类型的近似磁盘空间需求：

| 平台 | 安装类型 | 软件文件需求 (MB) |
| --- | --- | --- |
| Linux x86-64 | Instant Client | 110 |
| Linux x86-64 | Administrator | 650 |
| Linux x86-64 | Runtime | 350 |
| Linux x86-64 | Custom (maximum) | 650 |

### 软件要求

查看以下章节获取有关检查软件要求的信息：

- 第 2-3 页：在 Linux x86-64 上检查软件要求

#### 在 Linux x86-64 上检查软件要求

检查系统中是否安装所需的软件和补丁。

##### 检查所需的软件

根据您打算安装的产品，验证以下软件是否已安装在系统中。表格后的步骤描述了如何检查这些要求。

##### 检查软件需求

| 安装类型或产品 | 要求 |
| :--- | :--- |
| 所有安装 | 以下操作系统版本之一：<br>* Red Hat Enterprise Linux 3 (Update 2)<br>* SuSE Linux Enterprise Server (SLES) 8 且安装了 service pack 3 或更高版本<br>* SuSE Linux Enterprise Server 9 |
| 所有安装 | 系统必须运行以下内核版本（或更高版本）：<br>**Red Hat Enterprise Linux 3 (Update 2):**<br>2.4.21-158<br>注：这是默认内核版本。<br>**SuSE Linux Enterprise Server 8 (x86-64):**<br>2.4.2-185-smp<br>**SuSE Linux Enterprise Server 9:**<br>2.6.5-79 |



# 所有安装

必须安装以下软件包（或更高版本）：

**Red Hat Enterprise Linux 3 (Update 2):**
`make-3.79.1`
`gcc-3.2.3-34`
`glibc-2.2.295.20`
`glibc-devel-2.3.2-95.20`
`glibc-devel-2.3.2-95.20` (32 bit)
`compat-db-4.0.14-5`
`compat-gcc-7.3.296.128`
`compat-gcc++-7.3.296.128`
`compat-libstdcc++-7.3.296.128`
`compat-libstdcc++-devel-7.3.296.128`
`openmotif-2.1.30-8`
`setharn-3.1`
`gnome-libaio-4.1.2.90-34` (32 bit)
`libaio-0.396-3`
`libaio-devel-0.396-3`

**SuSE Linux Enterprise Server 8 (x86-64):**
`make-3.79.1`
`gcc-3.3-43`
`gcc-c++-3.3-43`
`glibc-2.2.15-213`
`glibc-32bit-8.1-9`
`glibc-devel-32bit-8.1-9`
`openmotif-2.2.2-124`
`libaio-0.396-3`
`libaio-devel-0.396-3`

**SuSE Linux Enterprise Server 9:**
`gcc-3.3.1-48`
`gcc-c++-3.3-43`
`glibc-2.3.98`
`libaio-0.3.98-18`
`libaio-devel-0.3.98-18`
`make-3.80`
`openmotif-libs-2.2.2-7.519.1`

## 2-4 Oracle 数据库安装指南

| 安装类型或产品 | 要求 |
| :--- | :--- |
| PL/SQL 原生编译、Pro/C++、Oracle Call Interface (OCI)、Oracle C++ Call Interface (OCCI)、Oracle XML 开发工具包 (XDK) | 支持适用于上述发行版的 GNU C 和 C++ 编译器版本用于这些产品。 |
| Oracle JDBC/OCI 驱动 | 仅在 x86-64 系统上，你可以使用以下 JDK 版本配合 Oracle JDBC/OCI 驱动，但安装并非必需： |
- 带有 JNDI 扩展的 Sun JDK 1.4.2_63

为确保系统满足这些要求，请按照以下步骤操作：

1. 要确定安装的 Linux发行版和版本，输入以下命令：

```bash
#### cat /proc/version
```

> 注：仅支持上表列出的发行版版本。不要在其他 Linux 版本上安装软件。

2. 仅在 Red Hat Linux 3 系统上，输入以下命令确定是否安装了所需的内核错误修正 (errata)：

```bash
#### uname -r
2.4.21-15.EL
```

在此示例中，输出显示了 x86-64 系统上的内核版本 (`2.4.21`) 和错误修正级别 (`15.EL`)。如果错误修正级别小于 15，请安装最新的内核更新。内核更新可以从 Red Hat Network 获取。

3. 仅在 SuSE Linux Enterprise 8 系统上，输入以下命令确定是否安装了 Service Pack 3：

```bash
#### uname -r
2.4.21-185.smp
```

在此示例中，输出显示了 x86-64 系统上的内核版本 (`2.4.21-185`) 和类型 (`smp`)。如果 x86-64 系统上的内核版本低于 `2.4.21-185`，请联系 SuSE 获取有关获取和安装 Service Pack 3 或更高版本的信息。

4. 仅在 SuSE Linux Enterprise 9 系统上，输入以下命令确定是否安装了所需的内核：

```bash
#### uname -r
2.6.5-7.97
```

在此示例中，输出显示了内核版本 `2.6.5-7.97`。如果 x86-64 系统上的内核版本低于 `2.6.5-7.97`，请联系 SuSE 获取相关信息。

5. 要确定是否安装了所需的软件包，输入以下命令：

```bash
#### rpm -q package_name
```

如果未安装软件包，请从 Linux 发行版媒体下载。

6. 要继续操作，请前往“创建 UNIX 组和用户”。

### 创建 UNIX 组和用户

取决于是否是首次安装 Oracle，你可能需要：

- Oracle Inventory 组 (`oinstall`)

在首次安装 Oracle 软件时，需要创建此组。该组通常名称为 `oinstall`。

> 注：如果系统中已经安装了 Oracle，该 Oracle Inventory 组必须是用于安装新软件的用户的主组。

- Oracle Inventory 组 (`oinstall`)

在首次安装 Oracle 软件时，需要创建此组。该组通常名称为 `oinstall`。该组拥有所有已安装的 Oracle 软件。

#### 确定 Oracle Inventory 组是否存在

在系统中首次安装 Oracle 时，安装程序会创建 `oraInst.loc` 文件。该文件标识 Oracle Inventory 组名称和 Oracle Inventory 路径。要确定 Oracle Inventory 组是否存在，输入以下命令：

```bash
#### more /etc/oraInst.loc
```

如果 `oraInst.loc` 文件存在，输出类似于：

```
inventory_loc=/u01/app/oracle/oraInventory
inst_group=oinstall
```

`inst_group` 参数显示 Oracle Inventory 组的名称 (`oinstall`)。

#### 创建 Oracle Inventory 组

如果 `oraInst.loc` 文件不存在，请如下方式创建 Oracle Inventory 组：

- 输入以下命令创建 `oinstall` 组：

```bash
# /usr/sbin/groupadd oinstall
```

#### 创建 Oracle 软件所有者

在情况下你需要创建 Oracle 软件所有者：

- 如果不存在 Oracle 软件所有者，例如系统首次安装 Oracle 软件
- 如果存在 Oracle 软件所有者，但你想使用不同的 UNIX 用户

##### 确定现有的 Oracle 软件所有者

要确定 Oracle 软件所有者名称 `oracle` 是否存在，输入命令：

```bash
#### id oracle
```

如果用户 (`oracle`)存在，输出类似于：

`uid=440(oracle) gid=200(oinstall) groups=201(dba),202(oper)`

如果用户存在，请确定你是想使用现有用户还是创建一个新用户。如果你想使用现有用户，请确保该用户的主组是 Oracle Inventory 组。

> 注：如有时，在在使用或修改现有用户之前请联系您的系统管理员。

- 要创建一个新用户，请查看下节。

##### 创建新的 Oracle 软件所有者

如果不存在 Oracle 软件所有者，或者您需要一个新的 Oracle 软件所有者用户，请根据您的操作系统按照以下方式创建。在后续步骤中，除非已存在该用户，否则请使用名称 `oracle`。

1. 要创建 `oracle` 用户，请输入类似下所示的命令：

```bash
#### /usr/sbin/useradd -g install|-g dba oracle
```

在此命令中：

- `-g` 选项指定主组，该组必须是 Oracle 目录组，例如 `oinstall`
- `-G` 选项指定可选的次要组

2. 为 `oracle` 用户设置密码：

```bash
#### password oracle
```

请查看以下章节以继续：

- 在第 2-8 页识别所需的软件目录

#### 修改现有的软件所有者

如果 `oracle` 用户存在，但其主组不是 `install`，您可以按照以下方式对其进行修改：

- 输入类似所示的命令，使用 `-g` 选项指定主组，并使用 `-G` 选项指定任何所需的次要组：

```bash
#### /usr/sbin/usermod -g install -G dba oracle
```

### 识别所需的软件目录

您必须为 Oracle 软件识别或创建以下三个目录：

- Oracle 基目录 (Base directory)
- Oracle 目录目录 (Inventory directory)
- Oracle 实例目录 (Home directory)

以下小节描述了这些目录的要求：

#### Oracle 基目录



Oracle 基目录充当 Oracle 软件安装的顶层目录。它类似于 Windows 系统上用于 Oracle 的时使用的 `C:\Oracle` 目录。在 Linux 系统上，最优灵活架构 (OFA) 指南建议您使用类似下方的路径作为 Oracle 基目录：

```
/mount_point/app/oracle_sw_owner
```

在此示例中：

- `mount_point` 是包含 Oracle 软件的文件系统的挂载点。

本指南中的示例使用 `/u01` 作为挂载点目录。但是，您可以选择另一个挂载点目录，例如 `/oracle` 或 `/opt/oracle`。

- `oracle_sw_owner` 是 Oracle 软件所有者的 UNIX 用户名，例如 `oracle`。

您可以为多个安装程序使用同一个 Oracle 基目录，也可以为不同的安装创建不同的 Oracle 基目录。如果 UNIX 用户在同一系统上安装 Oracle 软件，则每个用户必须创建一个独立的 Oracle 基目录。以下示例基目录可以同时存在于同一系统上：

```
/u01/app/oracle
/u01/app/orauser
/oracle/app/oracle
```

后续章节描述了如何识别可能适用于您的安装的现有 Oracle 基目录，以及在必要如何创建一个新的 Oracle 基目录。

无论您是创建新的 Oracle 基目录还是决定使用现有的目录，都必须设置 `ORACLE_BASE` 环境变量来指定该目录的完整路径。

### Oracle 目录目录

Oracle 目录 (`oraInventory`) 存储系统上安装的软件清单。它是所有 Oracle 软件安装所需的且是共享的。当您首次在系统上安装 Oracle 软件时，安装程序会提示您指定此目录的路径。Oracle 建议选择以下路径：

```
oracle_base/oraInventory
```

安装程序会创建您指定的目录，并为其设置正确的所有者、组和权限。您不需要手动创建它。

> 注意：所有 Oracle 软件安装都依赖此目录。请确保定期对其备份。除非您已从系统中完全删除了所有 Oracle 软件，否则请删除此目录。

### Oracle 目录

Oracle 目录是您选择为特定 Oracle 产品安装软件的目录。您必须将不同的 Oracle 产品或同一 Oracle 产品的不同版本安装在不同的 Oracle 目录中。当您运行安装程序时，它会提示您指定此目录的路径以及一个标识它的名称。您指定的目录必须是 Oracle 基目录的子目录。安装程序建议使用类似下面的路径作为 Oracle 目录：

```
oracle_base/product/1...1
```

安装程序会创建您指定的目录，并为其设置正确的所有者、组和权限。您不需要手动创建它。

后续章节描述了如何识别可能适用于您的安装的现有 Oracle 基目录，以及在必要时创建一个新的 Oracle 基目录。

无论您是创建新的 Oracle 基目录还是决定使用现有的目录，都必须设置 `ORACLE_BASE` 环境变量来指定该目录的完整路径。

### 配置 oracle 用户环境

```
$ su oracle
```

+ 5. 要确定 oracle 用户的默认 shell，请输入以下命令：

```
$ echo $SHELL
```

+ 6. 使用任何文本编辑器打开 oracle 用户的 shell 启动文件：

> 注意：在 Red Hat Linux 上，`.bash_profile` 是 Bash shell 的用户启动文件。

- Bourne shell (`sh`)、Bash shell (`bash`) 或 Korn shell (`ksh`)：

```
$ vi .bash_profile
```

- C shell (`csh` 或 `tcsh`)：

```
% vi .login
```

+ 7. 输入或编辑以下行，指定默认文件模式创建掩码值为 022：

```
umask 022
```

+ 8. 如果文件中设置了 `ORACLE`、`SID`、`ORACLE_HOME` 或 `ORACLE_BASE` 环境变量，请从文件中删除相应的行。

+ 9. 保存文件并退出编辑器。

+ 10. 若要运行 shell 启动脚本，请输入以下命令之一：

- Red Hat Enterprise Linux 上的 Bash shell：

```
$ ./bash_profile
```

- Bourne、Bash 或 Korn shell：

```
$ ./.profile
```

- C shell：

```
% source ./login
```

+ 11. 如果您不是在本地系统上安装软件，请输入类似下面的命令，将 X 应用程序显示在本地系统上：

- Bourne、Bash 或 Korn shell：

```
$ DISPLAY=local_host:0.0 ; export DISPLAY
```

- C shell：

```
% setenv DISPLAY local_host:0.0
```

在此示例中，`local_host` 是您想要用于显示安装程序（您的工作站或 PC）的系统主机名或 IP 地址。

+ 12. 如果确定 `/tmp` 目录有超过 400 MB 的空闲磁盘空间，请识别至少有 400 MB 空闲空间的文件系统，并设置 `TEMP` 和 `TMPDIR` 环境变量指定该文件系统上的临时目录：

2-12 Oracle 数据库安装指南

### 配置 oracle 用户环境

+ a. 使用 `df -k` 命令识别一个具有足够空间的文件系统。

b. 如必要，输入类似下面的命令，在您识别的文件系统上创建临时目录，并对该目录设置适当权限：

```
$ su - root
#### mkdir /mount_point/tmp
#### chmod awr /mount_point/tmp
#### exit
```

+ c. 输入类似下面的命令来设置 `TEMP` 和 `TMPDIR` 环境变量：

- Bourne、Bash 或 Korn shell：

```
$ TEMP=/mount_point/tmp
$ TMPDIR=/mount_point/tmp
$ export TEMP TMPDIR
```

- C shell：

```
% setenv TEMP /mount_point/tmp
% setenv TMPDIR /mount_point/tmp
```

+ 13. 输入类似下面的命令来设置 `ORACLE_BASE` 环境变量：

- Bourne、Bash 或 Korn shell：

```
$ ORACLE_BASE=/u01/app/oracle
$ export ORACLE_BASE
```

- C shell：

```
% setenv ORACLE_BASE /u01/app/oracle
```

在这些示例中，`/u01/app/oracle` 是您之前创建的 Oracle 目录。

+ 14. 输入以下命令确保没有设置 `ORACLE_HOME` 和 `TNS_ADMIN` 环境变量：

- Bourne、Bash 或 Korn shell：

```
$ unset ORACLE_HOME
% unset TNS_ADMIN
```

- C shell：

```
% unsetenv ORACLE_HOME
% unsetenv TNS_ADMIN
```

注意：如果设置了 `ORACLE_HOME` 环境变量，安装程序将使用指定的值作为 Oracle 主目录的默认路径。然而，如果您设置了 `ORACLE_BASE` 环境变量，Oracle 建议取消 `ORACLE_HOME` 环境变量并选择安装程序建议的默认路径。

预安装任务 2-13

+ 15. 若要验证环境已设置正确，请输入以下命令：

```
$ umask
$ env | more
```

验证 `umask` 命令显示的值为 22、022 或 0022，并且您在本节中设置的环境变量具有正确的值。

# 3

## 安装任务

本章描述了如何启动 Oracle 通用安装程序并在您的系统上安装 Oracle 产品。它包含了关于以下主题的信息：

> 注意：在开始安装之前，请复阅第 1 章“安装概述”中的信息，并完成第 2 章“预安装任务”中列出的任务。

- 安装概述

- 从 OTN 网站下载 Oracle 软件

- 将 Oracle 客户端软件拷贝到硬盘

- 安装 Oracle 客户端软件

### 安装概述

Oracle 客户端软件通过光盘（CD-ROM 或 DVD-ROM）提供，或者您可以从技术网络 (OTN) 下载。本章描述了如何安装 Oracle 软件：

- 安装概述

- 从 OTN 网站下载 Oracle 软件

- 将 Oracle 客户端软件拷贝到硬盘

- 安装 Oracle 客户端软件

### 下载归档文件

某些平台在您将光盘插入驱动器时会自动挂载。如果光盘未自动挂载，请参附录 A 获取有关挂载的特定平台信息。

### 从 OTN 网站下载 Oracle 软件

要提取安装文件，请执行以下步骤：

+ 1. 使用任何浏览器访问以下地址：

`http://www.oracle.com/technology/`

2. 导航到您想要安装的产品的页面。



### 文件系统准备

在文件系统中，通过文件识别所需的空间。

选择一个具有足够空闲空间以扩展文件的文件系统。

在您选择的文件系统上：

识别一个具有足够空闲空间以扩展文件的文件系统。

可用空间至少为文件大小的两倍。

### 提取文件

要提取安装文件，执行以下步骤：

1. 如必要，切换到包含文件的目录。
2. 某些平台在您将光盘插入驱动器时会自动挂载。如果光盘未自动挂载，请参附录 A 获取有关挂载的特定平台信息。
3. 输入类似下面的命令来解压文件：

```
$ gunzip filename
```

4. 要提取文件，输入类似下面的命令：

```
$ cpio -idmv
```

### 将 Oracle 客户端软件拷贝到硬盘

将软件拷贝到硬盘：

1. 如果光盘没有挂载，您可以使用 NFS 或 FTP 将文件拷贝到目标系统。
2. 在硬盘上为光盘创建一个目录：

```
$ mkdir Diskl
```

3. 切换到挂载目录：

```
$ cd Diskl
```

4. 将挂载盘的内容拷贝到新的子目录：

```
$ cp -R /mount_point Diskl
```

下表列出了各平台的典型挂载点：

| 平台 | 挂载点 |
| --- | --- |
| Linux (Red Hat) | `/mnt/cdrom` |
| Linux (SuSE) | `/media/cdrom` |

## 安装 Oracle 客户端软件

安装 Oracle 客户端软件：

1. 如果光盘没有挂载，您可以使用 NFS 或 FTP 将文件拷贝到目标系统。
2. 在硬盘上为光盘创建一个目录：

```
$ mkdir Diskl
```

3. 切换到挂载目录：

```
$ cd Diskl
```

4. 将挂载盘的内容拷贝到新的子目录：

```
$ cp -R /mount_point Diskl
```

硬件集群安装模式屏幕。你必须在此屏幕上选择“本地安装”（Local Installation）。

- 重新安装 Oracle 软件
- 如果你在已安装 Oracle Client 的 Oracle 目录下重新安装 Oracle 软件，则必须重新安装在开始安装之前安装的任何组件。

### 运行 Oracle 安装程序

按照以下步骤启动安装程序并安装软件：

1. 如果你从光盘安装软件，如果尚未挂载，请挂载光盘。
- 某些平台在插入光盘时会自动挂载。如果光盘没有自动挂载，请参阅get A 获取有关挂载的信息。
2. 如必要，以 Oracle 软件用户（`oracle`）登录并设置 `DISPLAY` 环境变量。
3. 根据安装位置，完成以下步骤之一以启动安装程序：
- 如果安装文件在光盘上，执行类似下面的命令，`directory_path` 为 CD-ROM 挂载点或 DVD-ROM 路径：

```bash
cd /tmp
cd /directory_path/runInstaller
```

- 如果安装文件在硬盘上，更改到该目录并输入以下命令：

```bash
./runInstaller
```

如果安装程序未出现，请参阅第 C 页的“Windows 显示错误”部分进行故障排除。
4. 使用以下指南完成安装：
- 遵循安装程序窗口显示的说明。如果需要更多信息，点击“帮助”。
- 当安装程序提示你以 root 权限运行脚本时，在 root 用户登录的终端输入类似下面的命令：

```bash
### /script_path/script_name
```

注意：Oracle 安装程序会自动安装 Oracle 提供的 Java 运行时（JRE）。运行 Oracle 安装程序和多个向导需要此版本的 JRE。
5. 如果你选择了以交互式模式运行 Oracle 网络配置助手（NetCA）的安装类型，必须提供有关配置网络的详细信息。在交互模式下使用 NetCA 需要帮助时，点击任何屏幕上的“帮助”。

> 注意：如果你选择默认安装，NetCA 将非交互模式运行。
6. 当所有配置工具完成后，点击“退出”，然后点击“是”退出安装程序。
7. 请参阅第 4 章“安装后任务”，获取有关安装软件后必须完成的任务。

## 安装后任务

本章介绍了在安装软件后如何完成安装后任务。它包含以下主题：

- 必要安装后任务
- 推荐安装后任务
- 特定产品安装后任务

你必须执行“必要安装后任务”部分列出的任务。Oracle 建议在所有安装完成后执行“推荐安装后任务”部分列出的任务。

如果你安装并打算使用“特定产品安装后任务”部分列出的任何产品，必须执行特定子章节列出的任务。

> 注意：本章仅描述基本配置。请参阅 UNIX 系统 数据库管理员参考以及特定产品的管理和调整指南以获取更复杂的配置和调整信息。

### 必要安装后任务

完成安装后，必须执行以下章节描述的任务：

- 下载并安装补丁
- 运行 Enterprise Manager Java Console
- 使用 Instant Client
- 配置 Oracle 产品

#### 下载并安装补丁

检查 Oracle Metal 网站查看你安装所需的补丁。要下载所需的补丁：

- 使用浏览器查看 Oracle Metal 网站：

```
http://metalink.oracle.com
```

- 登录 Oracle Metal。

> 注意：如果你不是 Oracle Metal 注册用户，请点击“注册 MetaLink！”并按照注册说明操作。
3. 在 Oracle Metal 主页，点击“补丁”（Patches）。
4. 选择“简单搜索”（Simple Search）。
5. 指定以下信息，然后点击“前往”（Go）：
- 在“按搜索”（Search By）字段中，指定产品或家族，然后指定 RDBMS 服务器。
- 在“版本”（Release）字段中，指定当前版本号。
- 在“类型”（Type）字段中，指定补丁集/小型包。
- 在“平台”（Platform）或“语言”（Language）字段中，选择你的平台。

#### 使用 Enterprise Manager Java Console

除了使用 Enterprise Manager Database Control 或 Grid Control 管理 Oracle 10g 数据库，你还可以使用 Enterprise Manager Java Console 管理此版本或以前版本的数据库。Java Console 由“管理员”（Administrator）安装类型安装。

> 注意：Oracle 建议尽可能使用 Grid Control 或 Database Control 而不是 Java Console。

要启动 Java Console，请遵循以下步骤：

1. 设置 `ORACLE_HOME` 环境变量以指定安装 Oracle Client 的 Oracle 目录。
2. 设置系统的共享库路径环境变量包含以下目录：

| 平台 | 环境变量 | 所需设置 |
| --- | --- | --- |
| Linux x86-64 | `LD_LIBRARY_PATH` | `$ORACLE_HOME/lib/lib32:$ORACLE_HOME/lib:$LD_LIBRARY_PATH` |

3. 输入以下命令启动 Java Console：

```
$ $ORACLE_HOME/bin/orcmap
```

#### 使用 Instant Client 连接

如果你使用 Instant Client 安装类型，可以按照所示配置用户环境，允许动态链接客户端连接到数据库：

1. 为你的平台设置相应的共享库路径环境变量，指定包含 Instant Client 库的目录。对于 Instant Client 安装，此目录是安装时指定的 Oracle 目录，例如：

`/u1/app/oracle/product/10.1.0/client`

下表显示适用于平台的环境变量：

| 平台 | 环境变量 |
|---|---|
| Linux x86-64 | `LD_LIBRARY_PATH` |

2. 使用以下方法之一指定数据库连接信息：
- 使用以下格式指定 SQL 字符串：

```
//host:port/service_name
```

- 设置 `TNSADMIN` 环境变量以指定 `tnsnames.ora` 文件的位置，并从该文件中指定服务名。
- 设置 `TNSADMIN` 环境变量并设置 `TWO_TASK` 环境变量以从 `tnsnames.ora` 文件指定服务名。

> 注意：不需要指定 `ORACLE_HOME` 环境变量。

#### 配置 Oracle 产品

许多 Oracle 产品和选项在首次使用之前必须配置。在使用各个 Oracle 产品或选项之前，请产品文档库中指定相应的手册，该库位于 Oracle 文档 CD-ROM、DVD-ROM 或 OTN 网站上。

### 推荐安装后任务

Oracle 建议在安装完成后执行以下章节描述的任务：

- 备份 root.sh 脚本
- 设置用户账户
- 生成客户端静态库

#### 备份 root.sh 脚本



Oracle 建议在安装完成后备份 `root.sh` 脚本。如果你在同一个 Oracle 目录下安装其他产品，那么 Oracle 安装程序在安装期间会更新现有 `root.sh` 脚本的内容。如果你需要原始 `root.sh` 脚本包含的内容，可以从备份的 `root.sh` 文件中恢复。

### 设置用户账户

有关设置额外用户账户的信息，请参阅 UNIX 系统 数据库管理员参考。

### 生成客户端静态库

客户端静态库（`libclnt10.a`）在安装期间不生成。如果你想将应用程序链接到客户端静态库，必须先按照如下步骤生成它：

### 必须的特定产品安装后任务

1. 切换用户到 `oracle`。
2. 设置 `ORACLE_HOME` 环境变量以指定客户端程序安装时使用的 Oracle 根目录。例如：
    * Bourne shell (`sh`)、Bash shell (`bash`) 或 Korn shell (`ksh`)：

```bash
$ ORACLE_HOME=/u01/app/oracle/product/10.1.0/client_1
$ export ORACLE_HOME
```

    * C shell (`csh` 或 `tcsh`)：

```bash
% setenv ORACLE_HOME /u01/app/oracle/product/10.1.0/client_1
```

3. 输入以下命令：

```bash
$ $ORACLE_HOME/bin/lnInst
```

### 必须的特定产品安装后任务

以下章节描述了如果您安装并打算使用上述产品，则必须执行的特定于平台的安装后任务：

- 配置 Oracle Net 服务
- 配置 Oracle 预编译器

### 配置 Oracle Net 服务

如果您在该系统上安装了较旧版本的 Oracle 软件，您可能希望从旧版本的 Oracle Net `tnsnames.ora` 文件中复制信息到新版本对应的文件中。

> 注意：`tnsnames.ora` 文件的默认位置为 `$ORACLE_HOME/network/admin/` 目录。然而，您也可以为该文件使用一个中心化位置，例如 `/etc`。

如有必要，您可以向新文件为额外的数据库实例添加连接信息。

### 配置 Oracle 预编译器

下节描述了 Oracle 预编译器的安装后任务：

- 配置 Pro*C/C++

> 注意：所有预编译器配置文件都位于 `$ORACLE_HOME/precomp/admin` 目录。

### 配置 Pro*C/C++

验证 `PATH` 环境变量是否包含包含 C 编译器可执行文件的目录。表 4–1 显示了根据您的平台和编译器，验证路径设置的默认目录和相应命令。

### 表 4–1 C/C++ 编译器目录

| 平台 | 路径 | 命令 |
|---|---|---|
| Linux x86-64 | `/usr/bin` | `$ which gcc` |

# 5 移除 Oracle 软件

本章描述了如何从 Oracle 根目录完全删除所有软件。

> 注意：如果您只想移除单个产品，请检查该产品的特定文档以了解要求和限制。

## 移除 Oracle 软件

以下步骤描述了如何使用安装程序从 Oracle 根目录移除 Oracle 软件：

> 注意：请始终使用 Oracle 通用安装程序移除 Oracle 软件。不要在未使用安装程序移除软件的情况下删除任何 Oracle 根目录。

1. 如必要，以 `oracle` 用户身份登录：

   `$ su - oracle`

2. 设置 `ORACLE_HOME` 环境变量以指定您想要移除的 Oracle 根目录路径：
    * Bourne、Bash 或 Korn shell：

     `$ ORACLE_HOME=/u01/app/oracle/product/10.1.0/client_1`

     `$ export ORACLE_HOME`

    * C shell：

     `$ setenv ORACLE_HOME /u01/app/oracle/product/10.1.0/client_1`

3. 按照如下启动安装程序：

   `$ORACLE_HOME/oui/bin/runInstaller`

4. 在欢迎窗口中，点击“卸载产品”（Uninstall Products）。
5. 在清单（Inventory）窗口中，选择您想要移除的 Oracle 根目录和产品，然后点击“移除”（Remove）。
6. 当安装程序显示确认窗口要求您确认想要卸载产品及其依赖项组件时，点击`是`（Yes）。

安装程序在移除软件时会显示进度指示。

7. 当产品删除后，点击`取消`（Cancel）退出安装程序，然后点击`是`（Yes）。

## 挂载光片

此 Oracle 产品同时通过 CD-ROM 和 DVD-ROM 交付。这些光片采用 ISO 9660 格式并带有 Rockridge 扩展。本附录描述了如何在每个支持的平台上挂载和卸载光片。它包含了以下主题的信息：

- 见 A-1 页在 Linux x86-64 上挂载光片

### 在 Linux x86-64 上挂载光片

在 Linux 系统上，光片在插入光驱器时会自动挂载。如果光片没有自动挂载，请按照以下步骤挂载：

1. 切换用户到 `root`：

```
$ su - root
```

2. 如必要，输入与以下任一类似的命令以弹出当前挂载的光片并将其从驱动器中移除：
    - Red Hat:

      - `# eject /mnt/cdrom`

    - SuSE:

      - `# eject /media/cdrom`

在这些示例中，`/mnt/cdrom` 和 `/media/cdrom` 是光驱器的挂载点目录。

3. 将适当的光片插入光驱器。
4. 要验证光片是否自动挂载，根据您的平台输入以下命令之一：
    - Red Hat:

      - `# ls /mnt/cdrom`

    - SuSE:

      - `# ls /media/cdrom`

5. 如果此命令未能显示光片内容，请根据您的平台输入类似挂载的命令：
    - Red Hat:

      - `# mount -t iso9660 /dev/cdrom /mnt/cdrom`

    - SuSE:

      - `# mount -t iso9660 /dev/cdrom /media/cdrom`

在这些示例中，`/mnt/cdrom` 和 `/media/cdrom` 是光驱器的挂载点目录。

6. 如果安装程序正在显示“磁盘位置”（Disk Location）对话框，请输入光片挂载点目录路径，例如：`/mnt/cdrom`

要继续，请转到以下章节之一：

- 如果您想将软件拷贝到硬盘，请参见以下章节：

见 3-3 页将 Oracle 客户端软件拷贝到硬盘

- 如果您想从光片安装软件，请参见 3-3 页的“安装 Oracle 客户端软件”章节

## 使用响应文件安装和配置 Oracle 产品

本章描述了如何使用响应文件安装和配置 Oracle 产品。包含了以下主题的信息：

- 引言
- 创建 `oraInst.loc` 文件
- 准备响应文件
- 在静默或抑制模式下运行安装程序

### 引言

您可以通过在启动 Oracle 通用安装程序时指定响应文件，完全或部分地实现 Oracle 软件的安装和配置。安装程序使用响应文件中包含的值对某些或所有提示提供回答：

- 如果您在响应文件中包含了所有提示的响应，并在启动安装程序时指定了 `-silent` 选项，则安装程序将在静默模式下运行。在静默模式期间，安装程序不会显示任何屏幕。相反，它会在您用于启动安装程序的终端中显示进度。
- 如果您在响应文件中包含了部分或所有提示的响应，并省略了 `-silent` 选项，则安装程序将在抑制模式下运行。在抑制模式期间，安装程序仅显示您未指定信息的屏幕。您还可以使用响应文件中的变量或命令行选项来抑制其他屏幕，例如不需要提示信息的欢迎屏幕或摘要屏幕。

下表描述了您可能想在静默模式或抑制模式下运行安装器的原因：

| 模式 | 用途 |
|---|---|
| 静默 (Silent) | 如果想执行以下操作，请使用静默模式： - 完成无人安装，您可以使用系统实用程序进行调度，例如： - 在多个系统上在无用户交互的情况下完成类似的安装 - 在未安装窗口 系统的系统上安装软件 |
| 抑制 (Suppressed) | 如果您想在多个系统上完成简单的 Oracle 安装，并对某些但并非所有提示提供默认答案，请使用抑制模式。 |

### 安装概述

要使用安装程序在静默或抑制模式下安装和配置 Oracle 产品，请遵循以下步骤：

> 注意：在静默或抑制模式下运行安装程序之前，您必须在系统上完成所有要求的预安装任务。

1. 创建 `oraInst.loc` 文件。
2. 准备响应文件。
3. 在静默或抑制模式下运行安装程序。

这些步骤将在后续章节中描述。

### 创建 oraInst.loc 文件



如果您计划在静默或抑制模式下使用安装程序安装 Oracle 产品，如果 `oraInst.loc` 文件不存在，则必须手动创建。该文件指定了 Oracle 清单目录的位置，安装程序会在其中创建系统中安装的 Oracle 产品清单。

> 注意：如果系统之前安装过 Oracle 软件，`oraInst.loc` 文件可能已经存在。如果文件存在，则您不需要创建新文件。

要创建 `oraInst.loc` 文件，请遵循以下步骤：

1. 切换用户到 root：

```
$ su root
```

2. 按照如下切换目录：

```
#### cd /etc
```

- 使用文本编辑器创建 `oraInst.loc` 文件，其中包含以下行：

```
inventory_loc=ORACLE_BASE/orInventory
st_group=
```

在此示例中，`ORACLE_BASE` 是 Oracle 基础目录的路径，例如 `/01/app/oracle`。

- 输入命令为 `oraInst.loc` 文件设置适当的所有者和权限：

```
#### chown oracle:install oraInst.loc
#### chmod 664 oraInst.loc
```

### 准备响应文件

你可以使用两种方法来准备响应文件，以便在静默模式（silent-mode）或抑制模式（suppressed-mode）安装：

- 编辑响应文件模板

此方法对于即时客户端（Instant Client）、管理员（Administrator）或运行时（Runtime）安装类型最为有用。

- 使用安装程序记录响应文件

此方法对于自定义（Custom）或仅软件（software-only）安装最为有用。

以下各小节描述了每种方法。

#### 编辑响应文件模板

Oracle 为每个产品、实例类型以及每个配置工具提供了响应文件模板。这些文件位于 CD-ROM 上的响应目录中，或者 DVD-ROM 上的 `client/response` 目录中。

> 注意：如果你将软件复制到了硬盘，响应文件位于 `Disk1/response` 目录。

表 B-1 列出了随 Oracle Client 提供的响应文件。

| 响应文件 | 描述 |
|---|---|
| `instantClient.rsp` | Oracle Client 的即时客户端安装 |
| `clientAdmin.rsp` | Oracle Client 的管理员安装 |
| `clientRuntime.rsp` | Oracle Client 的运行时安装 |
| `clientCustom.rsp` | Oracle Client 的自定义安装 |

准备响应文件：

- 将响应文件从响应文件目录复制到你系统上的某个目录：

```
$ cp /directory_path/response/response_file.rsp local_directory
```

在此示例中，`directory_path` 是 CD-ROM 挂载点目录或 DVD-ROM 上的客户端目录。如果你已将软件复制到硬盘，也可以根据偏好编辑 `response` 目录中的文件。

- 2. 使用文本编辑器打开响应文件：

```
$$ vi /local_dir/response_file.rsp
```

- 3. 按照文件中的指令编辑该文件。

> 注意：如果你没有正确配置响应文件，安装程序或配置助手将失败。请参见第 C-4 页的“静默模式响应文件错误处理”，获取有关调试静默安装失败的更多信息。

#### 记录响应文件

你可以使用交互模式下的安装程序记录响应文件，然后对其进行编辑，并用于静默模式或抑制模式安装。在记录响应文件时，你可以完成安装，也可以在摘要（Summary）页面退出安装程序，在开始将软件复制到系统之前。

> 注意：你不能使用记录模式在使用基础安装（Basic Installation）方法安装期间创建响应文件。

记录新的响应文件：

- 1. 完成第 2 章中的预安装任务。

当你运行安装程序记录响应文件时，它会检查系统以验证其是否符合安装软件的要求。因此，Oracle 建议你在完成所有所需的预安装任务的同时记录响应文件。

- 2. 如果你尚未在该系统上安装 Oracle 软件，请按照上一节所述创建 `oraInst.loc` 文件。

- 3. 确保 Oracle 所有者用户（通常为 `oracle`）有权限在你运行安装程序时指定的 Oracle Home 路径中创建内容或写入内容。

- 4. 要记录响应文件，输入类似下面的命令来启动安装程序。

> 注意：不要为响应文件指定相对路径。如果你指定了相对路径，Oracle 通用安装程序将失败。

```
$ /directory_path/runInstaller -record -destinationFile filename
```

在以下示例中：

- `directory_path` 是 CD-ROM 挂载点目录、DVD-ROM 客户端目录路径，或硬盘上 `Disk1` 目录的路径

在静默或抑制模式下运行安装程序

- `-record` 参数指定你想记录在响应文件中输入的响应内容

- `filename` 是你想要记录的响应文件的完整路径和名称

5. 在安装程序的每个屏幕上，指定所需信息。

6. 当安装程序显示摘要屏幕时，执行以下操作之一：

- 点击 `Install` 创建响应文件，然后继续安装。

- 点击 `Cancel`，然后点击 `Yes` 创建响应文件但在不安装软件的情况下退出安装程序。

响应文件保存在你使用 `-destinationFile` 选项指定的 Location。

7. 如果你没有完成安装，请根据你在“指定文件位置”处指定的路径删除安装程序创建的 Oracle Home 目录。

8. 在另一个系统上使用响应文件之前，使用任何文本编辑器编辑文件并进行任何必要的更改。

编辑时请以文件中的注释作为指南。

### 在静默或抑制模式下运行安装程序

要在静默或抑制模式下运行 Oracle 通用安装程序，请遵循以下步骤：

- 1. 完成第 2 章列出的预安装任务。

2. 以 Oracle 软件所有者用户（通常为 *oracle*）登录。

3. 如果你正在完成抑制模式安装，请设置环境变量 `DISPLAY`。

> 注意：如果你正在完成静默模式安装，则不需要设置 `DISPLAY` 环境变量。

4. 要在静默或抑制模式下启动安装程序，请输入类似下面的命令：

> 注意：不要为响应文件指定相对路径。如果你指定了相对路径，Oracle 通用安装程序将失败。

```
$ /directory_path/runinstaller [-silent] -responseFile filename
```

在这些示例中：

- `directory_path` 是 CD-ROM 挂载点、DVD-ROM 上的客户端目录路径，或硬盘上 `Disk1` 目录的路径

- `-silent` 表示你想在静默模式下运行安装程序

- `filename` 是你配置的安装响应文件的完整路径和文件名

使用响应文件安装 Oracle 产品 B-5

注意：有关 `runInstaller` 命令选项选项的其他信息，请输入以下命令：

```
$ /directory_path/runInstaller -help
```

- 5. 安装完成后，以 root 用户登录并运行 `root.sh` 脚本：

```
$ su
#### /oracle_home_path/root.sh
```

### 调试

本附录包含有关调试的信息。它包含了以下主题的信息：

- 验证要求

- X Windows 显示错误

- 发生安装错误时的处理

- 查看安装会话日志

- 调试配置助手

- 静默模式响应文件错误处理

- 安装失败后的清理

#### 验证要求

在执行附录中的任何调试步骤之前，请确保系统符合要求并且你已完成第 2 章“预安装任务”中指定的所有任务。

阅读发行说明

在平台上安装产品之前，请阅读该产品的发行说明。发行说明位于 Oracle Database 10g 光盘上。最新版本的发行说明也可从 ONT 网站获取：

`http://www.oracle.com/technology/documentation/`

#### X Windows 显示错误

如果你在远程系统上运行安装程序并要在本地系统上显示安装程序的界面，你可能会看到类似的错误信息：

```
"Failed to connect to server"
*"Connection refused by server"
*"Can't open display"
```

如果你看到其中一个错误信息，请遵循以下步骤：

#### 如果发生安装错误该怎么办

> 注意：此步骤仅适用于 UNIX 工作站用户。如果您正在使用 PC或其他安装了 X server 软件的系统，请参阅 X server 文档获取有关如何允许远程系统在本地系统显示 X 应用程序的信息。

1. 在本地终端窗口中，以启动 X窗口会话的用户身份登录。

2. 输入以下命令：



`$ xhost +`

3. 输入以下命令，其中 `workstation_name` 是工作站的主名或 IP 地址：

- Bourne, Bash 或 Korn shell：

```bash
$ DISPLAY=workstation_name:0.0
$ export DISPLAY
```

- C 或 tsh shell：

```bash
$ setenv DISPLAY workstation_name:0.0
```

4. 要确定 X Window 应用程序是否在本地系统上正常显示，请输入以下命令：

```bash
$ xclock
```

X 时钟应该出现在您的显示器上。

如果时钟出现了，请关闭 X 时钟并重新启动安装程序。

#### 如果发生安装错误该怎么办

- 如果您在安装过程中遇到错误：

- 不要退出。

- 如果您在其中一个安装屏幕上输入错误信息后点击“下一步”，点击“上一步”返回屏幕并更正信息。

- 如果安装程序在复制或链接文件时遇到错误，请参阅 C-2 页的“查看安装会话的日志”部分。

- 如果在运行配置分配时遇到错误，请参阅 C-3 页的“排排除配置助手”部分。

- 如果您无法解决问题，请按照 C-4 页“安装失败后的清理”部分中列出的步骤删除失败的安装。

#### 查看安装会话的日志

在安装过程中，安装程序会在日志中记录其所执行的所有操作。如果您在安装期间遇到问题，请检查日志文件以获取有关问题可能原因的信息。

要查看日志文件，请按照以下步骤操作：

1. 如有必要，输入以下命令之一以确定 `oraInventory` 目录的位置：

```
$ cat /etc/oraInst.loc
```

此文件中的 `inventory_loc` 参数指定了 `oraInventory` 目录的位置。

2. 输入以下命令切换到安装程序日志目录，其中 `orainventory_location` 是 `oraInventory` 目录的位置：

```
$ cd /inventory_location/logs
```

3. 输入以下命令确定日志文件的文件名：

```
$ ls -ltr
```

此命令按创建顺序列出文件，并显示最近的文件。安装程序日志文件的名称类似于以下，其中 `date_time` 表示安装开始的日期和时间：

`installActionsdate_time.log`

4. 要查看日志文件中最近的内容（问题信息最可能出现在这里），请输入类似于以下命令的命令：

```bash
$ tail -50 installActionsdate_time.log | more
```

此命令显示日志文件的最后 50 行。

5. 如果安装程序显示或在日志文件中列出的错误表明存在重链接（relinking）问题，请查看以下文件以获取更多信息：

```
$ORACLE_HOME/install/make.log
```

#### 排排除配置助手的故障

要对配置助手运行时发生的安装错误进行排排除：

- 检查 C-2 页中“查看安装会话的日志”部分中列出的安装日志文件。

- 检查位于 `$ORACLE_HOME/cfgtoologs` 的特定助手日志文件。尝试修复导致错误的问题。

- 如果您看到“致命错误。重启”（Fatal Error. Restart）消息，请通过检查日志文件来查找问题原因。请参阅“致命错误”部分获取进一步说明。

#### 配置助手失败

Oracle 配置助手的失败会在安装屏幕底部。如果可用，配置助手界面会显示额外信息。配置助手的执行状态存储在以下文件中：`oraInventory_location/logs/installActionsdate_time.log`

执行状态代码列在下表中：

| 状态 | 结果代码 |
| --- | --- |
| 配置助手成功 | 0 |

#### 静默模式响应文件错误处理

| 状态 | 结果代码 |
| --- | --- |
| 配置助手失败 | 1 |
| 配置助手取消 | -1 |

#### 致命错误

如果在配置助手运行时收收到致命错误，请通过检查日志文件来查找问题原因。请参阅“致命错误”部分获取进一步说明。

#### 静默模式响应文件处理

要确定静默模式安装成功还是失败，请查看以下文件：

`oraInventory_location/logs/installActionsdate_time.log`

在以下情况下，静默模式安装失败：

- 您没有指定响应文件

- 您指定了不完整的响应文件

- 安装程序遇到如磁盘空间不足等问题

#### 安装失败后的清理

如果安装失败，请按照步骤删除失败的安装：

1. 按照 C-4 页“安装失败后的清理”部分中的描述启动安装。

2. 纠正问题原因。

3. 删除您想要删除的 Oracle home。

4. 删除安装期间创建的文件。

5. 重新安装软件。

## 索引

### A

- `administrator.rsp`, B-3

### B

- 基础目录

- Oracle 基础目录

- bash shell

- `bash_profile`, 2-12

- 基础安装类型

- 非交互式安装, B-4

- Bourne shell

- 默认用户文件, 2-12

### C

- 编译器

- Linux 上的, 2-5

- C shell

- 默认用户文件, 2-12

- CD-ROM

- 挂载

- Linux, x-64, A-1

- 硬件和软件认证, 1-2

- `chmod` 命令, 2-11

- 配置分配

- 排排除, C-3

- `custom.rsp`, B-3

### D

- 数据库配置助手

- 排排除, C-3

- 默认文件掩码

- 设置, 2-11

- 目录

- Oracle 基础目录, 2-8

- Oracle home 目录, 2-9

- Oracle Inventory 目录, 2-9

- `inventory`, 2-9

- 磁盘空间

- 检查, 2-3

- `DISPLAY` 环境变量

- 设置, 2-11, 2-12

### E

- 仿真器

- 从 X 安装, 2-2

- `env` 命令, 2-14

- 环境

- 检查设置, 2-14

- 为 `oracle` 用户配置, 2-11

- 环境变量

- `DISPLAY`, 2-11, 2-12

- `ORACLE_BASE`, 2-9, 2-11

- `ORACLE_HOME`, 2-11, 2-13

- `ORACLE_SID`, 2-11

- `PATH`, 2-11

- 从 shell 启动文件中删除, 2-12

- `SHELL`, 2-11

- `TEMP` 和 `TMPDIR`, 2-13

- `TNS_ADMIN`, 2-11

- 错误

- Linux 内核错误, 2-5

- 错误

- 配置助手, C-3

- 安装, C-2, C-4

- 非交互式安装, C-4

- 静默模式, C-4

- X窗口, C-1

- `/etc/orandst.loc`, C-3

- 示例

- Oracle 基础目录, 2-9

### F

- 致命错误, C-4

- 文件模式掩码

- 设置, 2-11

- 文件系统

- 适用于 Oracle 基础目录的 2-11 文件

- `administrator.rsp`, B-3

- `bash_profile`, 2-12

- `custom.rsp`, B-3

- 编辑 shell 启动文件, 2-12

- `/etc/orandst.loc`, C-3

- `instantclient.rsp`, B-3

- `.login`, 2-12

- `oralinst.loc`, 2-7, 10, B-2

- `oratab`, 2-10

- `profile`, 2-12

- 响应文件, B-3

- `runtime.rsp`, B-3

- `tnsnames.ora`, 4-4

## Korn shell

- 默认用户启动文件, 2-12

## L

## Linux

- 检查软件需求, 2-5

- 内核错误列表, 2-5

- Linux x86-64

## G

## group

- 检查是否存在安装组, 2-7

- 创建 `oinstall` 组, 2-6

- `groupupadd` 命令, 2-7

- 检查发行版, 2-5

- 检查版本, 2-5

- 软件需求, 2-3

- 日志文件, C-2

- 故障排除, C-2

- 登录文件, 2-12

## H

- 硬件认证, 1-2

- 硬件需求, 2-2

- home目录

  - 参见 Oracle home目录

## M

## mask

- 设置默认文件创建掩码, 2-11

- 内存需求, 2-2

- `mkdir` 目录, 2-11

- 设置默认文件创建掩码, 2-11

## mount point

- Oracle base目录, 2-8

- 挂载点目录, 3-3

- 多个 Oracle homes, 1-3

## I

## installation

- 概述, 3-1

- 可用产品, 1-2

- 完成, 3-5

- 注意事项, 1-2

- 错误, C-2 C-4



- 静默模式, C-4
- 指南, 3-3
- 日志文件, C-2
- 非交互式
  - 错误处理, C-4
  - `oracle.loc` 文件, B-2
  - 响应文件, B-3
  - 准备, B-3
  - 静默模式, C-4
- 模板, B-3
- 静默模式, B-5
- 安装指南, 3-3, 3-4
- Oracle 通用安装程序, 3-3
- 重装 Oracle 软件, 3-4

## installation software
- 拷贝到硬磁盘, 3-3
- 提取, 3-2
- 重装, 3-4

## instance
- 实例标识符 (SID), 2-11
- `instantclient.file`, B-3

## N

## Net Configuration Assistant
- 故障排除, C-3

## Network Information Services
- 参见 NIS

- `-interactive`
  - 本地用户和组的替代方案, 2-6

- 非交互式安装
  - `oracle.loc` 文件, B-2
  - 响应文件
    - 准备, B-3
    - 静默模式, B-5
    - 错误, C-4
  - 非交互式运行
  - Oracle 通用安装程序, B-5

## O

## OFA
- Oracle base目录建议, 2-8
- Oracle base目录的推荐路径, 2-8
- Oracle home目录的推荐路径, 2-9
- Oracle Inventory目录的推荐路径, 2-9

## J

## Java Runtime Environment
- 参见 IRE

## JRE
- Oracle 提供的版本, 3-4

## K

## kernel
- Linux 错误列表, 2-5
- `oinstall` 组
  - 检查是否存在, 2-7
  - 创建, 2-6
  - 描述, 2-6

## operating system
- 检查 Linux 发版和版本
  - x86-64, 2-5
- 操作系统需求
  - Linux x86-64, 2-5

## Optimal Flexible Architecture

## SOFA
- Oracle base目录
  - `ORACLE_BASE` 环境变量, 2-9
  - 创建, 2-1
  - 现在创建, 2-11
  - 描述, 2-8
  - Windows 中的对应目录, 2-8
  - 示例, 2-9
  - 识别适当的文件系统, 2-11
  - 识别现有, 2-10
  - 挂载点, 2-8
  - 推荐路径, 2-8
  - 与 Oracle 软件所有者的关系, 2-8

## Oracle Database
- 设置 `ORACLE_SID` 环境变量, 2-11

## Oracle Database Client
- 自定义安装, 1-2
- 运行时安装, 1-2

## Oracle home directory
- 描述, 2-9
- 推荐路径, 2-9
- 需求, 2-9
- 需求, 2-9
- 用于识别 Oracle base, 2-10
- Oracle home 名称, 2-9
- 描述, 2-9
- 指针文件, 2-7

## Oracle Inventory
- 描述, 2-9
- 推荐路径, 2-9
- Oracle Inventory 组
  - 检查是否存在, 2-7
  - 创建, 2-6, 2-7
  - 描述, 2-6

## Oracle Net
- 配置文件目录, 4-4

## Oracle Net Services
- 安装后任务, 4-4

## Oracle Precompilers
- 安装后任务, 4-4

## Oracle software
- 卸载, 5-1

## Oracle Software Owner user
- 为该用户配置环境, 2-11
  - 创建, 2-7
  - 描述, 2-6
  - 确定默认 shell, 2-12
  - 与 Oracle base目录的关系, 2-9
  - 组组成身份, 2-6
- Oracle 通用安装程序
  - 安装指南, 3-3

## response files
- 列表, B-3
- 运行, 3-4
- `oracle` 用户
  - 为其配置环境, 2-11
  - 爬取, 2-7, 2-8
  - 描述, 2-6
  - 确定默认 shell, 2-12
  - 与 Oracle base目录的关系, 2-9
  - 组组成身份, 2-6
- `ORACLE_BASE` 环境变量, 2-9, 2-11
- 从设置路径中移除, 2-12
- 设置, 2-11
- `ORACLE_HOME` 环境变量, 2-9
- 从设置路径中移除, 2-12
- 设置, 2-11
- `ORACLE_SID` 环境变量, 2-9
- 从设置路径中移除, 2-12
- 设置, 2-11
- `oratab` 文件, 2-10
- 位置, 2-7
- Oracle 目录
  - 位置, 2-7
  - `oratab` 格式, 2-10
  - 位置, 2-7

## P

## packages
- 在 Linux x86-64 上检查, 2-6
- 命令, 2-8
- 环境变量
- 设置, 2-11

## PC
- 安装, 2-2
- 权限
- 对于 Oracle base目录, 2-11
- 需求, 2-2
- 安装后
- 任务, 4-3
- 用户帐户, 设置, 4-3
- Oracle Net, 配置, 4-4
- Oracle Precompilers, 补丁, 4-4
- 在 Linux x86-64 上的需求, 2-5
- Pro
- 配置, 4-4
- 在 Linux x86-64 上的, 2-5

## R

## RPM
- 需求, 2-2
- Red Hat
  - 操作系统需求, 2-4
- Red Hat Package Manager
  - 参见 RPM
  - 需求
    - 硬件, 2-2
- 响应文件
  - `administrator.rsp`, B-3
  - `custom.rsp`, B-3
  - `instantclient.rsp`, B-3
  - `runtime.rsp`, B-3
  - `root` 用户, 3-4
- 备份, 3-1
- RPM
  - 在 Linux x86-64 上检查, 2-6
  - 命令, 2-6
  - `runtime.rsp`, B-3
- 取消, 2-13
- `tnsnames.ora`, 4-4
- 故障排除, C-1

## U
- `umask`, 2-14
- `umask.command`, 2-11
- `umask`, 2-11
- `chown`, 2-14
- `chmod`, 2-11
- `env`, 2-14
- `groupadd`, 2-7
- `midir`, 2-1
- `password`, 2-8
- `rmp`, 2-6
- `swap`, 2-3
- `swapon`, 2-3
- `umask`, 2-11
- `unset`, 2-13
- `unsetenv`, 2-13
- `useradd`, 2-8
- `xhost`, 2-1
- UNIX group
- 检查是否存在, 2-7
- 创建 `oinstall` 组, 2-6
- `installgroup`, 2-6
- 对于 Oracle 用户, 2-6
- 需求, 2-6
- 使用 NIS, 2-6
- UNIX user
- 创建 `oinstall` 组, 2-7
- `oracle`, 2-6
- 需求, 2-6
- 使用 NIS, 2-6
- UNIX workstation
- 安装, 2-1
- 取消, 2-13
- `unsetenv` 命令, 2-13

## S

## shell
- 确定 用户的默认 shell, 2-12
- `SHELL` 环境变量
- 取值, 2-12
- 启动文件
  - 编辑, 2-12
  - 移除环境变量, 2-12

## SID
- 设置 `ORACLE_SID` 环境变量, 2-11
- 静默安装, 1-2
- 软件认证
  - 软件需求
    - 在 Linux x86-64 上检查, 2-5
    - Linux x86-64, 2-3
- 启动文件
  - 对于 shell, 2-12

## SuSE
- 操作系统需求, 2-4

## swap space
- 需求, 2-2

## T
- `TEMP` 环境变量, 2-3
- 设置, 2-12
- 临时目录, 2-3
- 临时磁盘空间
  - 检查, 2-3
  - 释放, 2-3
  - 需求, 2-2
- `/tmp` 目录
  - 检查空间, 2-3
  - 释放空间, 2-3



`TMPDIR` 环境变量, 2-3

设置, 2-12

## W

### Windows
- Oracle base 的类比, 2-8

## X

### X 模拟器
- 安装, 2-2

### X窗口系统
- 启用远程主机, 2-1, 2-2
- X 窗口
  - 显示错误, C-1
- `xhost` 命令, 2-1
- `xterm` 命令, 2-2

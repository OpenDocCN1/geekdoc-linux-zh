
我们将在第 10 章探索如何将应用程序迁移到 Linux；现在，你应该注意你今天使用的应用程序是否具有专有格式。例如，Linux 对于 Intuit 制作的常用财务软件包 Quicken 或 Quickbooks 并没有直接的对等替代品。你可能希望将你的 Quicken 文件保存为 `.qif` 格式，以便运行在 Linux 上的 Windows 应用程序导入。当你迁移这些文件时，你可以使用这些工具的导入功能重新获取你的设置和数据。

# 帮助迁移设置和数据的软件

出现了一个专门围绕 Windows 到 Linux 迁移的整个行业，随着这个行业出现，许多可以从 Windows 获取设置和数据并移动到 Linux 的产品。所有这些产品的工作原理相似，并提供良好的结果。区别在于它们移动数据的方式以及它们支持的目标平台。当你考虑到进行这些迁移所需的时间时，使用这些自动化工具之一来节省时间就成了“明智之举”。

## Alacos Linux Migration Agent™

Alacos Linux Migration Agent 是从 Windows 迁移数据到 Linux 的独特方式之一，因为它是为通过网络迁移设计的。旧的 Windows 机器运行 Windows 版本的 Linux Migration Agent，而 Linux 目标机接收要迁移的数据。这种方法是独特的，它提供了在 Windows 机器仍在服务时将数据移动到目标机器的能力。Alacos Linux Migration Agent 允许你选择你想要迁移的设置，如图 9.9 所示。

### 276 Linux 商务桌面迁移

![](img/72e1c6125676a623b5032cfdab8d797c_294_0.png)

**图 9.9** 你可以选择使用桌面迁移代理 仅迁移你想迁移的设置和数据。

该产品以及所有其他产品最有用的功能之一是从 Outlook迁移到 Linux 上的邮件客户端的能力。这种解析 `.pst`文件的能力使得与从 Outlook 导出到 Thunderbird 导入以及从一个平台过渡数据到另一个平台进行繁琐操作相比，变得变得异常简单。你还可以使用连接到每台 PC 网卡的交叉网线进行直接的机器到机器拷贝。

## Resolve MoveOver

Resolve 开发了一款名为 MoveOver 的产品，功能正如此——它帮助你将设置从 Windows 迁移到原生 Linux 桌面，但 Resolve 的方法是将设置存储在 `.zip` 文件中，该文件可以存储或写入 CD，然后移动到 Linux。MoveOver Windows 到 Linux 迁移工具已作为一个开源项目发布，尽管开源版本仅支持某些操作系统。Resolve 还为 Linux 发布了开源的 MoveOver 产品，以鼓励 Linux 社区为 Linux 发行版开发代码。这是 MoveOver 以及这些自动化工具的阿喀琉斯之踵。这些产品都必须针对每个特定的 Linux 发行版开发和测试设置，因为某些发行版存储设置和数据的方式与其他不同。MoveOver 的 Resolve 既有默认界面也有高级界面，用于在 Linux 上导出 Windows 会话，如图 9.10 所示。

# 数据迁移与备份 277

## MoveOver 向导 - 步骤 7

### MoveOver

Windows 桌面到 Linux 迁移工具

欢迎！

1. 选择目标文件夹 / 设置类型

2. 高级选项

3. 开始文件/设置收集

第 2 步：高级用户选项

你想传输什么？

- m2v - video

- m3 - audio/- mpeg

- m4 - audiom4

- m5 - audiom4

- m6 - video

- m7 - audio

- m8 - mpeg4/macspaint

- m9 - Access.Extension.11

- m10 - Access.Application.11

- m11 - Access.ADEFile.11

- m12 - MSPower Document

- m13 - mfo - audio/-shockwave-flash

- 仅设置

- 仅文件

- 设置和文件

- 添加设置

- 添加文件夹

- 类型

- 添加文件

- 删除

- 删除全部

![](img/72e1c6125676a623b5032cfdab8d797c_295_0.png)

**图 9.10** Resolver 的 MoveOver 允许你选择从一个迁移到另一个的文件。

虽然不是每个 Linux 发行版都被 MoveOver 完全覆盖，但最常见的 SUSE 和 Red Hat 被 Resolve 针对。

**Versora Progression Desktop**

Versora 是一家专门专注于服务器和桌面 Windows 到 Linux 迁移的软件公司。他们的产品在迁移从 SQL Server 到 PostgreSQL 等开源数据库方面非常有价值。Versora 的 Progression Desktop 产品允许你在 Windows 上创建所有文件的包，一旦就可以将其所有设置导入到 Linux。你也可以选择将 Windows 桌面的某些部分创建便携包，如图 9.11 所示。

Versora 的 Progression Desktop 工作方式与 Resolvo 相同；它备份稍后扩展的文件。通过这个过程，你可以保留迁移前数据的备份。

# Linux 商务桌面迁移

![](img/72e1c6125676a623b5032cfdab8d797c_296_0.png)

**图 9.11** Versora Progression 允许你选择从 Windows 迁移到 Linux 的设置。

## Neotek Outlook2Evolution

Outlook2Evolution 或 O2E 是由 Neotek 开发的解决方案，用于从 Microsoft Outlook 导出个人信息并导入到 Evolution。与这里提到的其他工具不同，O2E 工具根据 GPL 许可，用户可以导出数据。O2E 工具依赖于 Thunderbird 的存在来导出并将数据迁移回你的 Linux 邮件客户端。这再次比 Alacos、Resolvo 和 Versora 的过程不够优雅，但它是免费的，如果你有迁移邮件和其他数据的需求，可以使用此工具协助数据迁移。

# 备份

有一句古语说，“防胜于治疗”。如果这句话没有首先归于本·富兰林，它在服务器崩溃后很容易被归于系统管理员。通常情况下，计算机用户不对自己的个人计算环境采取最基本的预防措施。备份可能是桌面用户被忽视的实践中最重要的之一。在遭遇 PC 崩溃时，大多数人可能会感到恐惧，不知道上次备份是什么时候做的以及恢复的可能性有多大。结论是，没有防止 PC 崩溃的方法，因此备份至关重要。

此外，如果你开始定期备份，你将有一个机制在预期 Windows 到 Linux 迁移之前将数据迁桌面。理想情况下，你将达到这样一个点：你确信所有关键信息都存储在便携的地方，即使你选择留在 Windows，你将能够在无需遭受的情况下引入硬件升级。

## 数据位置

为数据制定备份策略的第一步是确定数据位于系统的哪个位置。默认情况下，大多数用户数据存储在 `/home/$USER` 目录中。一旦你确认信息在这里，你就可以决定如何进行备份——到 DVD 驱动器或服务器等媒介。如果你的数据量较小（700MB 或更少），使用流行的 CD 刻录软件 `k3b`，你可以创建一个数据项目将所有关键文件拷贝到 DVD。易用的拖放界面允许你制作副本，但这只是你存档数据的许多方法之一。你也可以将其拷贝到第二个硬盘或其他存储设备，甚至通过网络备份你的数据。然而，方法并不如记得执行或安排系统定期执行它那么重要。

## 操作系统备份

![](img/72e1c6125676a623b5032cfdab8d797c_297_0.png)

创建备份的一种方法是使用 Knoppix CD-ROM 向额外的硬盘执行完整磁盘拷贝。这不是完成工作最快的方法，但它捕获了硬盘上的所有内容，包括你的所有数据，并且非常容易验证备份的内容。在这种情况下，考虑一台带有两个硬盘的 PC。第一块硬盘是你的操作系统所在的地方；第二个硬盘是你存储数据的地方。并不是每个人都有第二个硬盘，但在廉价存储的时代，拥有第二个内部或外部硬盘并不是不可接受的。对于一个 60 GB 的硬盘，有许多低于 100 美元的选择，而且由于你不需要投资备份软件，这很容易证明。

### 280 Linux 业务桌面迁移

#### 如何使用 Knoppix 备份你的硬盘

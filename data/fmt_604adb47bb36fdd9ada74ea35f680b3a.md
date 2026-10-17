
## 表 14.1 显示标签值

当你更改每个显示标签时，网格中的列标题会立即更新（只需将其视为 Borland 的双向工具即可）。现在网格看起来像图 14.9 所示。这看起来更好，但当你运行应用程序时，你会发现 `HIRE_DATE` 字段的默认宽度太宽了（见图 14.10）。

![](img/cb7f728580e05ab3a6dcf423bcc2f2_698_0)

图 14.9 带有新显示标签的网格。

![](img/cb7f728580e05ab3a6dcf423bcc2f2_698_1)

图 14.10 隐藏日期的网格。

为了增强外观，你可以使用字段编辑器编辑 `HIRE_DATE` 字段的 `DisplayWidth` 属性将其大小设置为 10。你可以立即在 IDE 中看到这一变化。

现在你想从网格中隐藏与工作相关的字段。要做到这一点，在字段编辑器列表中通过 Shift 击选择 `JOB_CODE`、`JOB_GRADE` 和 `JOB_COUNTRY` 字段，并将它们的 `visible` 属性设置为 `False`。现在网格不再显示这些字段，尽管它们仍然存在于数据集中。

操作字段属性演示了网格如何使用你为数据集定义的持久化字段来在网格中显示数据。你可以使用列编辑器（`Columns Editor`）更改列的默认顺序来进一步完善网格的外观。通过右键点击网格并在组件菜单中选择“列编辑器”菜单选项可以打开它。

当网格没有定义列时，将使用数据集中的字段属性自动创建它们。当所有列都定义好后，只有这些列会显示在网格中，且列所使用的字段可见性值不会被列定义覆盖。你可以通过右键点击列编辑器并选择“所有字段”（All Fields），为数据集中的所有字段添加列定义。图 14.11 重新排列了列定义；`FIRST_NAME` 和 `LAST_NAME` 列移动到列表末尾，`FULL_NAME` 字段出现在第二。现在网格中的列将按照该顺序显示。

![](img/cb7f728580e05ab3a6dcf423bcc2f2_699_0)

图 14.11 定义的网格列。

希望这次练习让你感受到如何访问数据并控制其显示和导航。现在我们来谈谈这个过程在底层是如何运作的。

## 典型数据流

Kylix 中的数据访问有两种不同的操作模式。由于所有视觉数据组件的存在，第一种最明显的一种是对数据的交互式修改和查看。第二种是通过数据集进行单向移动，用于发布或报告目的。

### 交互式数据操作

`dbExpress` 设计时考虑了 Borland 的 `TDataSet` 技术。`ClientDataSet` 正如其名称所示：用于客户端应用程序的数据集。此功能增加了数据库客户端应用程序的可扩展性和响应速度。使用 `ClientDataSet` 可以执行的一些操作列如下：

- 在客户端侧将数据持久化为 XML 或二进制文件
- 在内存中操作所有数据以实现快速运行

# DataCLX 基础

第 14 章

并且比双向光标更轻量，而 `ClientDataSets` 为需要这些功能的应用程序提供了双向功能。

## 配置服务器

Linux 上提供的各种数据库引擎有不同的配置方式。有些引擎（如 PostgreSQL 和 MySQL）包含在主要的 Linux 发行版中。其他的（如 InterBase）可以从网站下载，然后使用 RPM 或 CD 上的设置程序进行安装。如果您在运行 Kylix 的同一台机器上运行数据库服务器，则需要确保在连接之前数据库服务器已经启动。如果数据库服务器不在您的机器上，您可能需要在您的机器上安装一个客户端来访问它。在尝试连接数据库服务器之前，确保您已安装并启动了客户端。

根据您所使用的 Kylix 版本的库存单位（SKU），你至少会有两个驱动程序。在 Kylix 1.0 中，Desktop Developer SKU 包含了适用于 InterBase 和 MySQL 的 Express 驱动。Server Developer Kylix 1.0 在 Desktop Developer 的基础上增加了适用于 IBM DB2 和 Oracle 8 的 Express 驱动程序。Borland 正在为未来的版本开发额外的数据库驱动程序，因此当你读到这些文字时，你的 SKU 中可能拥有更多驱动程序。

当安装 Kylix 时，在该用户的 borland 目录下会创建一些文本配置文件。这些文本文件的格式类似于 INI 风格的文件。如果你使用了书中 CD 上的 `outset.sh` 文件，那么你将有一个 `/usr/local/kylik/borland` 目录。当你以不同的用户首次运行 Kylix 时，将创建一个 `.borland` 文件，并且原始 Kylix 配置目录中的文件将被复制。然后你可以为该用户自定义特定的连接信息。这样，如果你想以多种“人格”身份进行开发——例如，你的数据库工作是以 Oracle 为中心还是以 InterBase 为中心——你只需创建一个新用户并以该用户运行 Kylix，为之设置所有的数据库配置信息即可。

然而，我们进展有点快了。你将在本书随附的 CD 中找到关于 InterBase、MySQL、DB2 和 Oracle 的更多详细详细配置说明。现在让我们来看看 Kylix 安装的默认连接选项。

## 连接到 InterBase

InterBase 是 Borland 自己的 SQL 数据库引擎，在虚拟市场和嵌入式系统中脱颖而出。它是一个功能完全且符合 ANSI SQL-92 标准的数据库引擎，支持高级功能，如多重事务、存储过程、触发器、生成器、高级数据类型和版本控制。它恰好也是最喜欢的数据库引擎，因为它

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_702_0.png)

# DataCLX

第四部分

它在支持的每个平台上 API 都是完全相同的。（它支持许多平台。）你可以在 `http://www.borland.com/interbase/` 找到更多关于 InterBase 的信息。

默认的 InterBase 连接被称为 `ILocal`。BDE 的名称恰好与 Windows 平台上提供的 Delphi 版本中 InterBase 的 BDE（Borland 数据库引擎）SQL 链接相同。它是本地 InterBase 连接的别昵号。

我使用了上文描述的 `ILocal` 连接来提供 DataCLX 的概述。如所述，如果你当前没有设置位置，可以右键点击拖到表单上的 `TSQLConnection` 组件，以指向你的 InterBase 数据库（`.gdb` 文件）的位置。当安装 Kylix 时，`database` 的值设置为 `database.gdb`，这是一个不存在的数据库。

要连接到 InterBase，你需要在机器上安装 InterBase 客户端。可以通过运行 InterBase 副本中包含的设置程序来安装 InterBase 客户端。

> 注意
> 示例数据库之一是 `employee.gdb`，它通常位于两个位置之一。请参见之前关于连接数据库的说明，以获取关于它可能位置的建议。如果你连接到另一台机器，请在文件引用前加上机器/服务器名称。例如，`jfkylix/idata/codecentral.gdb` 将指向服务器机器 `jfkylix` 以及 `ibata` 目录下的文件 `codecentral.gdb`。

在指定 InterBase 数据库的正确位置后，你只需要在 Object Inspector 中将组件的 `Connected` 属性设置为 `True`，并将你基于数据集的组件连接到它即可。

## 连接到 MySQL

在编写本文时，MySQL 可能是 Linux 上最流行的引擎。Kylix 的初始版本使用 MySQL 3.23 进行过测试。安装 MySQL（包括服务器和客户端）的步骤与 InterBase 类似。详情请参考 MySQL 网站：`http://www.mysql.com/`。

与 InterBase 一样，MySQL 使用数据库名称而不是文件名。你需要知道数据库名称才能连接到它。安装好 MySQL 客户端后，你可以通过以下操作连接到 MySQL：

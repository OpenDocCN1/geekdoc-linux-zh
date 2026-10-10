
应用程序服务器利用 dBExpress 组件（如 `TSQLConnection` 和 `TSQLDataSet`）连接到 InterBase 数据库。这些组件在第 1 章和第 2 章中有讨论。

应用程序服务器包含一个最小用户界面，显示当前连接数以及服务器使用的 RAM 量，如第 8 章所示。

服务器的 `pvContactsBeforeUpdateRecord` 事件处理程序展示了如何在发布到数据库之前确保每条记录具有唯一的主键，这在第 7 章中有讨论。

客户端应用程序在 `cdsContact` 数据集上使用了计算字段。计算字段在第 3 章中有讨论。

客户端应用程序的 `dsContactsDataChange` 事件处理程序负责在不可感知数据的 `TImage` 组件中显示来自数据集的图像。这一概念在第 4 章中有讨论。

客户端应用程序的 `cdsContactsReconcileError` 事件处理程序利用了 Delphi 内置的对账表单来处理对账错误，这在第 7 章中有讨论。

# 重新分发 dbExpress 应用程序

# 附录 A

# 本附录内容

- 可重新分发的文件 376
- 许可问题 378
- 基于 CD-ROM 的应用程序 378

本附录告诉你在编写完数据库应用程序后，重新分发它们所需的知识点。由于本书假设你使用 dbExpress 作为应用程序的数据访问技术，因此我不会解释如何重新分发 BDE 或 ADO。相反，我将专门集中在 dbExpress 和 DataSnap 上。

## 可重新分发的文件

重新分发使用 dbExpress 和 DataSnap 构建的应用程序非常简单——特别是如果你习惯于摆弄巨大的基于 BDE 或 ADO 的安装集。为了支持 dbExpress 和 DataSnap，你只需要随应用程序重新分发两个文件。

> **注意**
>
> 这仅仅是两个文件，除此之外你可能还需要重新分发应用程序需要的其他任何东西。例如，如果你启用运行时包构建应用程序，你还需要重新分发该应用程序所需的运行时包。

## 重新分发 Windows 应用程序

对于在 Microsoft Windows 下运行的 VCL 或 CLX 应用程序，你需要重新分发应用程序所使用的数据库后端的驱动程序。数据库引擎及其相关的 Windows 驱动程序列于表 A.1 中。

**表 A.1 dbExpress Windows 驱动程序**

| 数据库 | Windows 驱动程序 |
| :--- | :--- |
| InterBase | Dbexpint.dll |
| Oracle | Dbexpora.dll |
| DB2 | Dbexpdb2.dll |
| MySQL | Dbexppmys.dll |

除了 dbExpress 驱动程序之外，你还需要重新分发 `MIDAS.DLL`，其中包含客户端数据集技术所需的代码。

你可以将 dbExpress 驱动程序和 `MIDAS.DLL` 放在应用程序可以找到它们的任何位置，这可能是应用程序目录或 `SYSTEM32` 目录。这两个文件都不需要向 Windows 注册。

如果可以的话，你可以通过在项目的 `uses` 子句中引入 `MIDASLib` 并重新编译，将 DataSnap 静态链接到你的客户端应用程序中。这样做的话，你不需要随客户端应用程序重新分发 `MIDAS.DLL`（不过，它仍需随服务器应用程序重新分发）。

你还可以通过链接适当的文件将 dbExpress 驱动程序静态链接到应用程序中，具体文件如表 A.2 所列。

| 数据库 | 单元 |
| :--- | :--- |
| InterBase | Dbexpint |
| Oracle | Dbexpora |
| DB2 | dbexpdb2 |
| MySQL | Dbexpmy |

> **注意**
>
> 尽管 Delphi 6 支持将 dbExpress 和/或 DataSnap 静态链接到应用程序，但你应注意，静态链接是一项新技术，并非与所有 DataSnap 代码完全兼容。例如，尝试调用 `TClientDataSet.SaveToFile` 将客户端数据集保存为 XML 文件时，静态链接时的保存格式与动态链接时不同。总之，如果你决定静态链接应用程序，请在发布给客户之前进行彻底测试。

## 重新分发 Linux 应用程序

对于在 Linux 下运行的 CLX 应用程序，你需要重新分发相应的 Linux dbExpress 驱动程序。表 A.3 列出了 dbExpress 当前支持的数据库引擎以及相关的 Linux 驱动程序。

| 数据库 | Linux 驱动程序 |
| :--- | :--- |
| InterBase | libsql.so |
| Oracle | libsqlor.so |
| DB2 | libsqlbd2.so |
| MySQL | libsqlmy.so |

除了 dbExpress 驱动程序外，你还需要重新分发 `LIBMIDAS.SO`。可重新分发的文件应放置在 `/home/<usrname>/delphidir/bin` 目录下。

## 许可问题

如果你编写的是处理本地数据的数据库应用程序（即数据不在机器之间传输），则无需担心应用程序的许可费用。然而，如果数据包从一台机器传输到另一台机器，你就需要向 Borland 支付少量重新分发费用，以使用 DataSnap 技术。

关于何时需要支付重新分发费用以及具体金额的详细信息，请访问 Borland 的网站 `http://www.borland.com/midas`。

## 基于 CD-ROM 的应用程序

许多数据库应用程序的一个常见需求是能够访问 CD 上的（只读）数据库。此类应用程序（如通讯录、零件数据库等）通常随 CD 上的大型数据库一起重新分发。最终用户无需更新数据——用户只需从 CD 访问数据。

要在 CD 上重新分发只读的 InterBase 数据库，你需要首先对该数据库运行 `gfix` 命令，如下所示：

```
gfix -read-only mydata.gdb
```

这将把数据库标记为只读。

在你的应用程序中，你应为所有数据提供程序设置 `poReadOnly` 选项，并将任何 `TClientDataSet` 的 `ReadOnly` 属性设置为 `True`。这将确保任何与数据库相关的组件不会尝试更新数据库中的任何数据。

# 附录：dbExpress Plus

![](img/fe651f295b5f960d5463c4fb581d2281_391_0.png)

## 附录内容

- 什么是 dbExpress Plus？ 380
- 更多信息 384

本附录简要介绍了 dbExpress Plus，这是 Thomas Miller 开发的 dbExpress 开源附加库。dbExpress Plus 可以从 CodeCentral 的 `codecentral.borland.com` 下载。ID 为 `#15945`。

## 什么是 dbExpress Plus？

dbExpress Plus 是一项开源工作，旨在通过在三个关键领域引入新组件来扩展 dbExpress：

- 脚本化
- 增强的元数据
- 数据泵送

以下章节简要介绍了这些组件。

## 脚本化

`TSQLScript` 提供了一种通过所谓的脚本一次性执行多个 SQL 语句的方法。你可能熟悉 SQL 脚本文件。下面的片段显示了一个简单的脚本文件。这实际上是用于创建 CONMAN 数据库的 SQL 脚本的一部分。

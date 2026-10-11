
- 支持计算字段和聚合字段
- 对任何标量数据类型进行即时索引
- 跟踪客户端的所有数据更改（插入、删除、更新），以便进行客户端数据库操作
- 交互式数据协调错误处理
- 支持参数化查询

我确定还漏了一些功能，但 `TClientDataset` 可以做的一些功能将在本章后面的部分作为示例出现。

# 与数据感知组件一起

第 15 章

## TClientDataSet 属性

此组件有许多属性，因此我们只讨论这里最常用的几个，并在本章晚些时候探索其他许多属性

`Active` 属性控制 `TClientDataSet` 中的数据是否加载到内存中。要将数据加载到内存中进行操作，你可以指向一个 `TDataSetProvider` 或使用一个 `MyBase` 数据集文件。要使用 `TDataSetProvider`，你需要将 `ProviderName` 属性赋值为可用 `TDataSetProvider` 的名称。例如，你可以采取以下步骤（我们将重用在本示例中设置的组件，这里列出的步骤比实际需要的要多一点）：

1. 选择文件（File）、新建应用程序（New Application）。
2. 将表命名为 `UsingData`。
3. 选择文件（File）、新建（New）、数据模块（DataModule）（我们将在其他示例中重用此数据模块）。
4. 将数据模块命名为 `dmBLLocal`。更新数据模块的标题（Caption）。
5. 在 `dmBLLocal` 上放置一个 `TSQLConnection`，并将其命名为 `dbBLLocal`。
6. 在 `dmBLLocal` 上放置一个 `TSQLDataSet`，并将其命名为 `sqlEmployees`。然后将其 `SQLConnection` 属性分配给 `dbBLLocal`。
7. 点击 `CommandText` 对应的省略号，选择 `select * from EMPLOYEES` 作为你的 SQL 语句。
8. 从组件面板上的数据访问（Data Access）选项卡放置一个 `TDataSetProvider`，将其 `Name` 设置为 `prvEmployees`，并将 `DataSet` 属性分配为 `sqlEmployees`。
9. 从同一选项卡放置一个 `TDataSet`，将其 `Name` 设置为 `cdsEmployees`，并将 `ProviderName` 赋值为 `prvEmployees`（该项将出现在下拉列表中）。
10. 从同一选项卡放置一个 `TDataSource`，将其 `Name` 设置为 `dsEmployees`，并将 `DataSet` 属性分配为 `cdsEmployees`。
11. 将此单元保存为 `dmBLLocal.pas`。

完成后，数据模块看起来应该像图 15.5 所示。

现在你已经通过 `TDataSetProvider` 将 `TDataSet` 链接到 `SQLDataSet`，你可以通过将 `Active` 属性设置为 `True` 来在客户端填充你想要处理的所有数据。一旦数据集变为活动状态，你就可以通过与 `dsEmployees` 通信来管理或查看数据，`dsEmployees` 抽象了你与数据集的关系（这允许你更改使用的数据集，而无需重写与数据源通信的客户端数据访问代码）。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_716_0.png)

DataCLX

第四部分

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_717_0.png)

图 15.5

基础 `dmBLocal` 数据模块。

你刚刚采取的步骤将用于交互式操作支持 `dbExpress` 的数据库。你可以将任何可以表示结果集的数据加载到客户端数据集中。这包括执行存储过程的结果。我还应该提到，既然你已经在客户端加载了数据，现在可以将 `dmBLocal.Connected` 属性设置为 `False`。在你想在客户端提交更改之前，不需要再次连接。

`TClientDataSet` 支持在本地保留从 SQL 服务器拉取的数据的“公文包”（briefcase）文件副本 `FileName`。该属性是在 Delphi 4 中引入的，这是我在完成一次 Delphi 巡演后与我们研发人员之一交流的结果。它基本上是一个方便的 get/set 属性，结果生成了 `ClientDataSet` 的 `LoadFromFile` 和 `SaveToFile` 方法。它让公文包文件模式更加方便——只需指定用于公文包模式的文件名，其他所有内容将为你自动处理。当你启动应用程序时，如果组件发现 `FileName` 指定的文件，它将从那里加载数据。当你关闭应用程序时，数据的当前状态将写回文件名。要为数据库应用程序启用公文包功能，只需为 `MyBase` 文件指定一个名称。

如果你的数据集较大（1000 条记录或更多），你可能希望让用户快速使用某些数据，然后根据需要从 SQL 数据库加载其余数据（即当用户在结果集中向下滚动时）。`PacketRecords` 控制一次获取多少条记录。当设置为 -1（负一）时，它会一次加载整个集合。如果你将其设置为 0 并激活数据集，它将加载数据集的元数据信息，而不是数据行。当你将其设置为大于0的值时，它将每次加载该数量的行。当你使用处于活动状态的 `TSQLConnection` 组件来支持按需加载数据时，只需导航到当前加载数据之外，`ClientDataSet` 就会从服务器获取下一个 `<PacketRecords>` 行。

正如我之前提到的，此组件支持客户端索引。你只需通过设置 `IndexFieldNames` 属性即可在任何标量字段类型（数字、日期、字符、布尔）上创建索引。例如，你可以将 `cdsEmployees` 的 `IndexFieldNames` 属性设置为 `last_name;first_name`，这将数据的显示顺序设置为按姓的字母顺序，然后是名字。每当你设置索引值，它只会更改数据的显示顺序。数据的存储保持不变。

## TClientDataSet 方法

在 `IndexFieldNames` 属性中指定由分号分隔的字段列表是设置数据顺序简单的方法。如果你想在同一个索引中支持升序和降序字段，可以使用 `AddIndex` 方法。这是该方法的声明：

```pascal
procedure AddIndex(const Name: string; Options: TIndexOptions
  const Fields: string = '';
  const GroupingLevel: Integer = 0);
```

通过传递这些值，你可以指定索引的名称。几年前，我创建了 `TClientDataSet` 组件，它允许最终用户通过点击列来更改数据顺序。

1. 选择文件（File）、新建应用程序（New Application）。
2. 将表命名为 `UsingData`。
3. 选择文件（File）、新建（New）、数据模块（DataModule）（我们将在其他示例中重用此数据模块）。
4. 将数据模块命名为 `dmBLLocal`。更新数据模块的标题（Caption）。
5. 在 `dmBLLocal` 上放置一个 `TSQLConnection`，并将其命名为 `dbBLLocal`。
6. 在 `dmBLLocal` 上放置一个 `TSQLDataSet`，并将其命名为 `sqlEmployees`。然后将其 `SQLConnection` 属性分配给 `dbBLLocal`。
7. 点击 `CommandText` 对应的省略号，选择 `select * from EMPLOYEES` 作为你的 SQL 语句。
8. 从组件面板上的数据访问（Data Access）选项卡放置一个 `TDataSetProvider`，将其 `Name` 设置为 `prvEmployees`，并将 `DataSet` 属性分配为 `sqlEmployees`。
9. 从同一选项卡放置一个 `TDataSet`，将其 `Name` 设置为 `cdsEmployees`，并将 `ProviderName` 赋值为 `prvEmployees`（该项将出现在下拉列表中）。
10. 从同一选项卡放置一个 `TDataSource`，将其 `Name` 设置为 `dsEmployees`，并将 `DataSet` 属性分配为 `cdsEmployees`。
11. 将此单元保存为 `dmBLLocal.pas`。

你应该看到类似于 15.6 的内容。

> `TClientDataSet` 组件提供在随附的光盘中。请参考光盘上关于书中讨论的自定义组件的说明将其安装到你的 Kylix IDE 中。

15 与数据感知组件一起

| EMP_NO | FIRST_NAME | LAST_NAME | PHONE | EXT | HIRE_DATE |
|---|---|---|---|---|---|
| 120 | Janet | Baldwin | | | 03/21/91 |
| 125 | Oscar M. | Bennett | 250 | | 05/15/92 |
| 28 | Ann | Bennet | 5 | | 02/01/91 |

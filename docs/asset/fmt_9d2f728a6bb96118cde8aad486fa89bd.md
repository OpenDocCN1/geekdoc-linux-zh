
- DataCLX 架构 666
- 数据访问 666
- 数据控制 669
- 典型数据流 674
- 配置服务器 677
- 总结 680

# DataCLX

## 第四部分

本章将向你介绍 DataCLX 和 dbExpress。这些跨平台技术为 Kylix 以及未来版本的 Delphi 和 C++ Builder 提供了数据库连接支持，这些版本都包含了 dbExpress 和 DataCLX。

## DataCLX 架构

DataCLX 组件是用 Object Pascal 编写的跨平台数据访问组件。这些组件封装了对 ANSI C++ 编写的 dbExpress 组件的调用（以便能够立即迁移到其他平台）。dbExpress 组件与各种 SQL 服务器交互，并专门为利用 SQL 的特性而设计。使用 SQL 极大地简化了数据库管理接口，因此只需要少数组件即可封装以数据为中心的操作。事实上，Borland 提供的更多 DataCLX 组件（`TSQLTable`、`TSQLQuery` 和 `TSQLStoredProc`）完全是为了从现有的 Delphi 和 C++ Builder 迁移。

dbExpress 组件抽象了与各种 SQL 服务器的接口，允许开发者编写可以与任何符合 ANSI SQL-92 标准的服务器工作的应用程序，同时允许应用程序支持特定服务器厂商可能支持的功能。关于 dbExpress 组件的更多细节请参见第 16 章“数据访问层”。

## 数据访问

DataCLX 组件提供了属性、函数和方法，简化了数据库应用程序编程。可以通过 DataCLX 组件访问所有数据库管理系统功能，包括连接数据库、检索数据、执行更新以及处理元数据管理。

### 连接到数据库

要连接到数据库，你需要使用 `TSQLConnection` 组件。SQL 连接组件具有多个属性，用于指定数据库名称、用户名、密码、角色以及控制你如何连接数据库的各种参数。

让我们通过创建一个新的数据库应用程序来开始使用这些组件。从 Kylix 菜单中选择 `File -> New Application` 创建带有空白表单的新应用程序。

接下来，在组件面板上选择 dbExpress 选项卡，并将 `TSQLConnection` 组件拖到表单上。然后在对象检查器（Object Inspector）中选择 `Connection` 属性。点击下拉箭头并选择 `IBLBase` 作为连接名称。注意，`DriverName` 属性会自动设置为 InterBase，因为 `IBLBase` 被配置为 InterBase 数据库连接。根据此连接已有的配置信息，该组件的几个其他属性也已自动设置。

将 `LoginPrompt` 属性设置为 False。此 InterBase 连接已经定义了用户名和密码，所以你不需要再次输入它们。如果你将 `LoginPrompt` 留为 True，那么每当激活数据库连接时，你都必须输入用户名和密码，这会非常累人。当然，当你的应用程序完成后，你也可以通过将 `LoginPrompt` 属性设回 True 来为应用程序用户要求登录提示。

你可能在好奇用户名和密码属性存储在哪里，因为它们在对象检查器中不会立即显示。`Params` 属性以 `TStrings` 对象中键/值对列表的形式包含了此连接的用户名、密码、角色以及所有其他参数。你可以通过点击对象检查器中属性旁边的省略号来查看所有值。如图 14.1 所示，`Params` 属性编辑器可以方便地更改任何已存在的值。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_692_0.png)

**图 14.1**

Params 编辑器。

如果你想添加未列出的参数，只需将其作为新行输入。当你关闭编辑器窗口时，系统会提示你保存这些值。如果你选择保存，这些新值将保存到字符串列表中，下次你打开 `Params` 编辑器时，新值将列出来。

在继续之前，请确保检查是否真的可以连接到数据库。尝试在对象检查器中将 `Connected` 属性设置为 True。如果遇到错误，说明你的数据库名称没有指向有效的 InterBase 数据库。这很容易修复。右键点击 `TSQLConnection` 组件并选择 Edit Connection Properties 菜单项。修改 `Database` 属性指向 `employees.gdb` 文件，如图 14.2 所示。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_693_0.png)

**图 14.2**

连接编辑器。

> [!NOTE]
>
> 如果你不知道 `employees.gdb` 文件在哪里，可以从根目录找到 employee.gdb。在许多 InterBase 安装中，该文件是 `/usr/local/interbase/examples/employee.gdb`。

在你成功测试数据库连接后，如果需要，可以再次断开连接，你接下来使用的数据集组件会在需要时重新建立连接。

### 检索数据

将 `TSQLClientDataset` 连接拖到表单上。将 `Connection` 属性设置为你刚刚创建的连接名称。默认情况下，`CommandType` 设置为 `ctQuery`，`SQL` 属性设置为 `SELECT * FROM Employee`。现在通过将 `Active` 属性设置为 True 在网格中查看数据。

如果你想更改查询，可以在对象检查器中编辑 `SQL` 属性。你也可以像使用 `TSQLConnection` 组件那样使用 `Params` 属性为查询添加参数。

## 数据控制

你已经设置了数据库连接，并从表中检索了数据。现在你需要使用一些数据控件在表单上显示数据。

### 使用可视化控件显示数据

`DataSource` 组件用于抽象数据控件与数据访问组件之间的通信。因此，转到组件面板的 Data 选项卡，将 `DataSource` 拖到表单，并 `DataSet` 属性设置为 `SQLClientDataset`。

接下来，转到 Data Controls 选项卡并将 `TDBNavigator` 和 `TDBGrid` 组件拖到表单上。你希望通过 `DataSource` 与 `SQLClientDataSet` 通信。你可以按住 Shift 键点击这两个组件来设置它们的 `DataSet` 属性。如果数据集未激活，表单现在看起来应该像图 14.4。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_695_0.png)

**图 14.4**

未激活的数据。

你现在可以通过将 `SQLClientDataSet` 的 `Active` 属性设置为 True 来激活数据集，从而查看 Employee 表中的数据。实际数据将出现在网格中，如图 14.5 所示。

![](img/cb7f7288580e05eab3a6dcf423bcc2f2_695_1.png)

**图 14.5**

激活的数据。

当你首次将数据加载到网格时，列标题仅仅是字段的名称。在这个数据集的情况下，由于字段名称非常容易理解，标题是还算清晰的，但这种情况可能并不总是如此。幸运的是，DataCLX 组件允许你非常方便地更改网格的显示属性。作为字段标题显示的文本由字段的 `DisplayLabel` 属性决定

## DataCLX 基础 第 14 章

数据字段。默认情况下，字段的标签（Label）与其在数据集中的名称相同。要更改字段的显示标签，你需要先将字段设置为持久化（persistent）。

自然，有一种简单的方法可以实现这一点。通过右键点击组件，使用数据集的组件编辑器（Component Editor）菜单，如图 14.6 所示。

![](img/cb7f728580e05ab3a6dcf423bcc2f2_696_0)

图 14.6 数据集组件编辑器。

你可以看到此数据集的许多选项。你现在感兴趣的菜单是字段编辑器（Fields Editor）（别担心，我们稍后介绍其他选项）。当字段编辑器出现时，目前没有列出任何字段，也没有定义任何持久化字段。你可以通过在列表中点击右键调出字段编辑器菜单（如图 14.7 所示）来快速添加它们。

![](img/cb7f728580e05ab3a6dcf423bcc2f2_696_1)

图 14.7 字段编辑器菜单。

选择“添加字段”（Add Fields）菜单选项，数据集中的所有字段都将变为持久化（即在表和源代码中都会为每个字段定义一个 `TField` 对象）。现在你可以看到列表框中可以使用数据集中的所有字段，如图 14.8 所示。

![](img/cb7f728580e05ab3a6dcf423bcc2f2_697_0)

图 14.8 字段编辑器。

当字段是持久化后，你可以通过在字段编辑器列表中选择一个或多个字段，并在对象检查器（Object Inspector）中修改其属性来修改它们的任何属性。在本例中，我们设置了表 14.1 列出的显示标签值。

| 字段名称 (Field Name) | 显示标签 (Display Label) |
| :--- | :--- |
| EMP_NO | Emp # |
| FIRST_NAME | First Name |
| LAST_NAME | Last Name |
| PHONE_EXT | Phone |
| HIRE_DATE | Hired |

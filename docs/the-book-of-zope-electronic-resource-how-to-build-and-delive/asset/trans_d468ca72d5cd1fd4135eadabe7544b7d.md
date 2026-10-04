
因此，你可以通过将原始 ZClass 的 Class ID 复制到新的 ZClass 并删除原始 ZClass，将现有实例与新的 ZClass 关联。执行此操作时必须非常小心，因为这很容易破坏原始 ZClass 的所有实例。你还可以指定本地计算机上的图像并将其作为 ZClass 实例的图标，以便它们像其他对象一样在管理界面中显示图标。

![](img/43a28cce5475b2f487bf455365567fb6_183_0.png)

图 9-11：创建后更改 ZClass 信息

## 9.3.4.3 视图（Views）标签页

点击 Views 为你的 ZClass 实例创建视图。视图由管理界面标签栏中的一个标签页以及在点击标签页时调用的方法组成。为了更好地理解这一点，请图 9-12 的底部包含一个由 Zope 自动创建的名为 Contents 的视图。图 9-11 中的管理界面显示了 Basic（基础）视图示例，你可以在其中更改与 ZClass 相关的某些信息。

视图允许你对对象执行各种功能，包括：

- 显示和编辑对象的内容
- 编辑对象的属性
- 预览对象
- 更改对象的安全权限

图 9-12 中的 Contents 显示了一个名为 Contents 的标签，如果你点击类实例，该标签会出现在标签栏中。如果你打开文件夹 Books 并点击对象 Book01，Contents 标签就会出现在标签栏中。如果你然后点击 Contents，将会调用 Python 方法 `manage_all`；该方法（继承自 `ObjectManager` 基类）会显示类文件夹对象的内容。

我们可以为 BookClass 创建视图，这样我们就可以检查和修改对象的属性，并按照其在第三层架构中用户看到的样子来查看它。

## 9.3.4.4 属性表（Property Sheets）标签页

点击 Property Sheets 创建描述类实例的属性表。大多数 ZClasses 只有的一张属性表，但如果你有许多属性，有时创建单独的表来组织它们是有意义的。例如，作为一家书店，你可能会为书籍的属性创建一个属性表，为分销商的属性创建另一个属性表。图 9-13 显示了属性表 `Book_description`。（你将在第 9.3.7 节学习如何创建它。）

![](img/43a28cce5475b2f487bf455365567fb6_184_0.png)

图 9-12：确定 ZClass 的视图

## 9.3.4.5 权限（Permissions）标签页

点击 Permissions 设置权限。（更多信息请参见第 6 章。）

## 9.3.4.6 子对象（Subobjects）标签页

使用子对象界面（如图 9-14 所示）指定 BookClass 实例可以包含的对象类型（图像、DTML 方法、文件等）。（在第 7 步创建 ZClass 时，你必须选择了基类 `Manager`，该 ZClass 才能包含子对象。）

例如，如果你想让对象 Book01 包含一张图像（可能是书籍封面）以及文本，请进入 `/Control_Panel/Products/Sales/BookClass` 下的 ZClass 并点击 subobjects。按住 CTRL 键，然后点击列表中的 File 和 Image。

图 9-13：建立属性表和属性

### Control_Panel/Properties: Sales/BaseClass/properties/subsheets/subobjects 处的 Z 类

选择可以添加到此类对象的类型：

- DTL Class
- Book
- Detail Method
- Detail Method
- DTL Document
- Image
- Folder

对象应出现在文件夹列表中：

- Select-Changes

图 9-14：管理界面

（注：由于部分原文部分存在大量逻辑重复，以下为对应原文内容的翻译）

因此，你可以通过将原始 ZClass 的 Class ID 复制到新的 ZClass 并删除原始 ZClass，将现有实例与新的 ZClass 关联。执行此操作时必须非常小心，因为这很容易破坏原始 ZClass 的所有实例。你还可以指定本地计算机上的图像并将其作为 ZClass 实例的图标，以便它们像其他对象一样在管理界面中显示图标。

图 9-11：创建后更改 ZClass 信息

## 9.3.4.3 视图（Views）标签页

点击 Views 为你的 ZClass 实例创建视图。视图由管理界面标签栏中的一个标签页以及在点击标签页时调用的方法组成。为了更好地理解这一点，请图 9-12 的底部包含一个由 Zope 自动创建的名为 Contents 的视图。图 9-11 中的管理界面显示了 Basic（基础）视图示例，你可以在其中更改与 ZClass 相关的某些信息。

视图允许你对对象执行各种功能，包括：

- 显示和编辑对象的内容
- 编辑对象的属性
- 预览对象
- 更改对象的安全权限

图9-12 中的 Contents 显示了一个名为 Contents 的标签，如果你点击类实例，该标签会出现在标签栏中。如果你打开文件夹 Books 并点击对象 Book01，Contents 标签就会出现在标签栏中。如果你然后点击 Contents，将会调用 Python 方法 `manage_all`；该方法（继承自 `ObjectManager` 基类）会显示类文件夹对象的内容。

我们可以为 BookClass 创建视图，这样我们就可以检查和修改对象的属性，并按照其在第三层架构中用户看到的样子来查看它。

## 9.3.4.4 属性表（Property Sheets）标签页

点击 Property Sheets 创建描述类实例的属性表。大多数 ZClasses 只有的一张属性表，但如果你有许多属性，有时创建单独的表来组织它们是有意义的。例如，作为一家书店，你可能会为书籍的属性创建一个属性表，为分销商的属性创建另一个属性表。图 9-13 显示了属性表 `Book_description`。（你将在第 9.3.7 节学习如何创建它。）

图 9-12：确定 ZClass 的视图

## 9.3.4.5 权限（Permissions）标签页

点击 Permissions 设置权限。（更多信息请参见第 6 章。）

## 9.3.4.6 子对象（Subobjects）标签页

使用子对象界面（如图 9-14 所示）指定 BookClass 实例可以包含的对象类型（图像、DTML 方法、文件等）。（在第 7 步创建 ZClass 时，你必须选择了基类 `Manager`，该 ZClass 才能包含子对象。）

例如，如果你想让对象 Book01 包含一张图像（可能是书籍封面）以及文本，请进入 `/Control_Panel/Products/Sales/BookClass` 下的 ZClass 并点击 subobjects。按住 CTRL 键，然后点击列表中的 File 和 Image。

图 9-13：建立属性表和属性

### Control_Panel/Properties: Sales/BaseClass/properties/subsheets/subobjects 处的 Z 类

选择可以添加到此类对象的类型：

- DTL Class
- Book
- Detail Method
- Detail Method
- DTL Document
- Image
- Folder

对象应出现在文件夹列表中：

- Select-Changes

图 9-14：管理界面

（注：原文后半部分存在大量重复及乱码描述，已按字面翻译）

## 9.3.5 基类及其视图

因此，你可以通过将原始 ZClass 的 Class ID 复制到新的 ZClass 并删除原始 ZClass，将现有实例与新的 ZClass 关联。执行此操作时必须非常小心，因为这很容易破坏原始 ZClass 的所有实例。你还可以指定本地计算机上的图像并将其作为 ZClass 实例的图标，以便它们像其他对象一样在管理界面中显示图标。

## 9.3.6 创建属性表

为了创建一个 BookClass 的属性表，请执行以下操作：

1. 转到 `/Control_Panel/Products/Sales`。
2. 点击管理界面上的 Property Sheets 标签页。
3. 点击 Add。
4. 在 Id 字段中输入 `Book_description`；Title 字段可以留空。
5. 点击 Add 创建 `Book_description`。

现在你可以点击 `Book_description` 属性表并设置各个属性。

| 方法 | 基础 | 视图 | 属性表 | 权限 | 定义权限 | 子对象 |
|---|---|---|---|---|---|
| Control_Panel/Properties/Sales/BookClass/propertiesheets/common | | | | | |
| | | | 添加实例表 | | |
| | | | | | |
| 导入/导出 | | | | | |

图 9-15：创建属性表的管理界面

### 9.3.6.1 在属性表中定义属性

属性（对象的属性）由一个 id、一个默认值以及一个属性类型组成。可以使用以下属性类型（更多信息请参见节 3.1.6）：

| 属性类型 | 描述 |
|---|---|
| boolean | 具有两个离散值的属性：真或假。在属性表中以复选框表示。 |
| date | 日期和时间值，在属性表中不能为空。此属性共享 DateTime 和 ZTime 对象的所有功能。（有关日期的更多信息请参见附录 A。） |
| float | 浮点数，通常用于表示分数或货币值。浮点数必须分配值。 |
| int | 整数，值可以是正或负且没有小数部分。值的范围在不同的操作系统上可能会有所，但精度至少为 32 位。int 属性不允许空值。 |
| lines | 字符串列表，每个列表项单独占一行。适用于多个单词关键词或任意数量的值。 |
| lang | 无上限或下限范围的整数值。使用此属性处理值可能超过数十亿的巨大数字。 |
| string | 无限制大小的单行字符串。这可能是最常用的属性类型。 |
| text | 无限制大小的多行字符串。在属性表中使用多行文本区域，通常用于描述或长段文本数据。 |

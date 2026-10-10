
### 注意

如果你决定始终使用单个字符字段来表示布尔字段类型，你可能需要考虑创建一个从 `TDBCheckBox` 派生的简单组件，该组件将 `ValueChecked` 设置为 `T`，将 `ValueUnchecked` 设置为 `F`（默认）。这样，你在使用该组件时就不必每次手动设置这些属性。

此外，你还应考虑在数据库中创建一个域来指定字符字段。这是我为自己的 InterBase 数据库创建的域：

```sql
CREATE DOMAIN DOM_BOOLEAN AS VARCHAR(1)
DEFAULT 'F' NOT NULL CHECK (VALUE IN ('F', 'T'));
```

## TDBRadioGroup

`TDBRadioGroup` 用于用户需要从短选项列表中选择一个选项的情况。默认情况下，选定项的值存储在底层数据集字段中，这意味着你通常将 `TDBRadioGroup` 组件连接到一个字符串字段。

在我的应用程序中，我发现我最常需要将选定项的索引存储在一个 `Integer` 字段中。如果你利用组件的 `Values` 属性，实现这一点很直接。`Values` 是一个字符串列表，它按以下方式与 `Items` 属性对应：

- 如果 `Values` 为空，则存储在底层数据集中的是 `Items` 属性中包含的字符串。
- 如果 `Values` 不为空，它应包含与 `Items` 属性相同数量的字符串值。当单选组中选中某项时，`Values` 属性中对应的值将被存储到数据集中。

使用第二条规则，你可以在 `Values` 属性中存储一个顺序数字列表，并将组件连接到一个 `Integer` 字段。Delphi 足够智能，会将选定项的数字表示存储在数据集中。在我的应用程序中，这通常是一个严重的限制，因此我创建了一个名为 `TETHComboBox` 的派生组件，它支持为 `Items` 属性中包含的每个字符串分配一个值。

![](img/fe651f295b5f960d5463c4fb581d2281_225_0.png)

**图 5.2**

`TDBRadioGroup` 的 `Items` 和 `Values` 属性之间的关系。

## TDBComboBox

`TDBComboBox` 的工作原理与 `TDBRadioGroup` 类似，因为它允许用户从列表中选择一个项并将其存储在数据集中。不幸的是，它不支持 `Values` 属性，因此你无法用它将选定项的索引存储在数据集中。在我的应用程序中，这通常是一个严重的限制，因此我创建了一个名为 `TETHComboBox` 的派生组件，它支持为 `Items` 属性中包含的每个字符串分配一个值。

## 注意

`Values` 属性仅在组件的 `Style` 属性设置为 `csDropDownList`、`csOwnerDrawFixed` 或 `csOwnerDrawVariable` 时才会生效。如果样式设置为 `csDropDown` 或 `csSimple`，则 `Values` 属性会被忽略，因为在这些情况下，用户可以在组合框的编辑部分输入任何值。

列表 5.1 包含 `TETHDBComboBox` 组件的源代码。

## 列表 5.1 ETHDBComboBox.pas

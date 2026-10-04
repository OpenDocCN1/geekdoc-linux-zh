

### 表 4-11: in 标签的属性

| 名称 | 解释 |
|---|---|
| name | 返回要迭代序列的变量名。请参见第 4.3.1.2 节中的“name 属性”。 |
| expr | 返回要迭代序列的表达式。请参见第 4.3.1.3 节中的“expr 属性”。 |
| sort | sort 属性用于在迭代之前对对象序列进行排序。value 属性是根据该属性名称对项目进行排序（如果指定了 mapping 属性，则为键名）。 |
| start | 指定当前批次起始序列项的变量名。如果省略，则从第一个项开始迭代。 |
| size | 迭代的每批项的大小。如果省略，则一次性迭代整个序列。 |
| orphan | 为了防止最后一批次太小而需要扩展最后一批次的项目数。如果省略，此值默认为 3。 |
| overlap | 每批次之间重叠的项目数。如果省略，则没有重叠。 |

### 表 4-12: in 主体内部定义的变量

| 名称 | 解释 |
|---|---|
| sequence-item | 当前迭代的元素。 |
| sequence-key | 与项序列关联的键；如果元素是二项元组，则定义此项。其值设置为第一个项，sequence-item 设置为第二个项。 |
| sequence-index | 当前迭代项的索引（第一个数字从 0 开始）。 |
| sequence-number | 当前迭代项的编号，第一个项为数字 1。 |
| sequence-start | 如果当前元素是当前批次的第一个项，则该变量为 true；否则为 false。这在必须在标签开始处插入文本时非常有用，特别是当文本引用了 in 标签定义的批次变量时。 |
| sequence-end | 如果当前元素是当前批次的最后一个项，则该变量为 true；否则为 false。这在必须在标签末尾处插入文本时非常有用，特别是当文本引用了 in 标签定义的批次变量时。 |
| sequence-even | 如果 sequence-index 为偶数，则设置为 true。可用于在表格中交替设置行背景色。 |
| sequence-odd | 如果 sequence-index 为奇数，则设置为 true。 |

使用该标签，你可以（例如）遍历列表中的元素并显示在表格中。例如，考虑以下代码：

```
1: <dml-in exp=['Henderson', 'Jackson', 'Johnson', 'Jones', 'King', 'Smith']>
2: <dml-if name="sequence-start">
3: <table>
4: <tr>
5: <th>sequence-start?</th>
6: <th>sequence-end?</th></th>
7: <th>sequence-index</th>
8: <th>sequence-item</th>
9: </tr>
10: </dml-if>
11: <dml-if name="sequence-odd">
12: <tr bgcolor="#eeee">
13: <dml-else>
14: <tr>
15: </dml-if>
16: <td><dml-var name="sequence-start"></td>
17: <td><dml-var name="sequence-end"></td>
18: <td><dml-var name="sequence-index"></td>
19: <td><dml-var name="sequence-item"></td>
20: </tr>
21: </dml-if name="sequence-end">
22: </table>
23: </dml-if>
24: 序列为空。
25: </dml-in>
```

在这个示例中，列表作为一个表达式传递给起始的 in 标签（第 1 行）。该标签首先确定列表是否为空（不包含任何项）；如果是，则使用列表标签输出此类提示消息（第 24 行和第 25 行）。否则，将对列表中的每个项依次执行主体中的代码。

当我们开始列表时，dml 将变量 `sequence-start` 设置为 true。我们使用 `dml-if` 测试此条件（第 2 行），并在其为真时定义表格表头（第 3 到第 9 行）。对于列表中的每个项，表格中都会添加一行行，该行包含由 in 标签定义的某些变量的值。测试 `sequence-odd` 变量以确定是否显示该行（第 11 行）。如果此值为 true，则显示该行（第 12 行），否则不显示（第 14 行）。当列表的最后一个项被迭代时，dml 将变量 `sequence-end` 设置为 true。我们使用 `dml-if` 测试此条件（第 21 行），并在其为真时关闭表格。此代码的渲染输出看起来类似于浏览器查看的图 4-7。

| sequence-start? | sequence-end? | sequence-index | sequence-item |
|---|---|---|---|
| | | 0 | Henderson |
| | | 1 | Jackson |
| | | 2 | Johnson |
| | | 3 | Jones |
| | | 4 | King |
| | | | 5 | Smith |

图 4-7：迭代元素并显示在表格中的代码输出

in 标签定义了几个变量，你可以对序列元素执行计算，并允许对序列进行批处理。对于分小批次而不是一次性显示的长序列，这种情况非常有用。请参见附录 A 中的列表变量、分组变量和批处理变量。

## 4.3.10 使用 in 标签

in 标签另一个有用功能是可以重复执行代码。为了实现这一点，in 标签使用了 `range` 方法，该方法最多接受三个参数：`range(Startvalue, Endvalue, Interval)`。

如果只指定一个参数，该参数为结束值，起始值为 0，间隔为 1。使用此方法会创建一个数字列表，生成的列表可以通过 in 标签运行。例如，调用 `range(5)` 创建包含五个元素的列表 `[0, 1, 2, 3, 4]`，你可以使用 in 标签定义循环。

以下内容会在文档的渲染输出中插入十次 "Hello!"：

```
<html-in "range(10)">
Hello!
</html-in>
```

## 4.3.11 tree 标签

tree 标签用于调查层级结构并以带有折叠分支和节点的树形结构呈现它们。因此，你可以创建一个类似于管理界面使用的树形结构。在图 4-8 的示例中，名为 Folder1 的文件夹包含几个：

| 类型 名称 | 大小 | 修改日期 |
|---|---|---|
| Subfolder1 | | 2001-05-27 22:36 |
| Subfolder2 | | 2001-05-28 02:17 |
| acl_users (User Folder) | | 2001-05-27 22:06 |
| dml_document2 | 1 Kb | 2001-05-27 02:18 |
| dml_method1 | 1 Kb | 2001-05-27 22:19 |
| dml_method2 | 1 Kb | 2001-05-27 22:19 |
| index_html | 1 Kb | 2001-05-27 22:06 |

图 4-8：Folder1 中的对象

要创建一个树形结构，在位于 Folder1 的 DTML 方法中使用 tree 标签：

```
<dml-tree>
<dml-var name="id">
</dml-tree>
```

树以图 4-9 所示的第三层视图显示。

![](img/43a28cce5475b2487bf45536557fb6_107_0.png)

图 4-9：简单的树形结构视图

图 4-9 中的树只显示当前文件夹中的对象，视觉上不如管理界面使用的吸引人。tree 标签本身非常复杂，接受多种用于格式化树视图的属性。例如，要在 DTML 方法所在位置之外启动树，必须指定起始对象的名称，如下：

```
<dml-tree name="Subfolder1">
```

`branches` 和 `branches_expr` 属性设置为方法 `tpValues`。查找所有对象和子对象的方法称为 `objectValues`。这些方法在文件夹对象为你定义。

为了确保树视图中同时显示对象及其相应的图标，请使用以下代码：

```html
<dt-tree>
<IMG SRC="-var name="icon"><dt-var name="id">
</dt-tree>
```

最重要的 tree 标签属性列在表 4-13 中。完整列表请参见附录 A。带星号的属性需要参数。

### 表 4-13: tree 标签的属性

| 名称 | 解释 |
|---|---|
| name* | 参见 4.3.1.2 节中的“name 属性”。 |
| expr* | 参见 4.3.1.3 节中的“expr 属性”。 |
| branches* | 用于查找子对象的方法名称。默认是 `tpValues`，这是一个查找另一个对象下的文件夹和子对象的方法。值必须是方法名。 |
| leaves | 使用 "leaves" 展开不包含子对象的文档名称。 |
| header* | 显示在任何分支展开之前的文档名称。这允许你标记层级结构中的分支。 |
| faater* | 显示在每个展开下方的文档名称。 |
| sart* | 在插入文本之前对分支排序。属性值是排序元素的属性名称。 |

此外，tree 标签在命名空间中放置了若干组织树对象显示的变量。这些变量中的一些列在表 4-14 中。

### 表 4-14: tree 标签体的变量

| 名称 | 解释 |
|---|---|
| tree-item-expand | 如果当前元素已展开，则为 true。 |
| tree-item-url | 当前元素的相对 URL。 |
| tree-raat-url | tree 标签所在的 HTML 文档的 URL。 |
| tree-level | 当前元素的深度。 |
| tree-caspan | 树嵌套的次数。 |
| tree-state | 树的状态；输出为 id 列表和子 id 列表。 |


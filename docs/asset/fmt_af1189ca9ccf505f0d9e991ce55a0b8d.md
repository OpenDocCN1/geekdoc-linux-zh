
```
<html-var standard_html_header>
<form action="Order_html">
<h2 align="center">订单单</h2>h2
<table border="0" cellpadding="2" cellspacing="4" width="100%">
<tr bgcolor="#FFF8F8">
<th>姓，名：</th>
<td><input name="name" size="40"></td>
</tr>
<tr bgcolor="#FFF8F8">
<th>地址：</th>
<td><input name="address" size="40"></td>
</tr>
<tr bgcolor="#FFF8F8">
<th>电话：</th>
<td><input name="telephone" size="40"></td>
</tr>
<tr bgcolor="#FFF8F8">
<th>传真：</th>
<td><input name="fax" size="40"></td>
</tr>
<tr bgcolor="#FFF8F8">
<th>邮箱：</th>
<td><input name="email" size="40"></td>
</tr>
<tr bgcolor="#FFF8F8">
<th>选择想要订购的书籍<br>&nbsp;&nbsp;</th>
<td><SELECT size="20" NAME="order:list">
<dt-ml-in expr="objectValues(['Book'])" sort=Title>
<option><html-var name="id"></option>
<option><html-var name="author"></option>
<option><html-var name="price"></option>
</dt-ml-in>
</SELECT>
</td>
</tr>
<tr>
<th></th>
<td><input type="submit" value="立即订购"></td>
</tr>
</table>
<html-var standard_html_footer>
```

当此代码被渲染时，DTML 方法 `OrderForm_html` 将显示图 10-12 所示的界面。

最后，你创建 DTML 方法 `Order_html`，使用来自 `OrderForm_html` 的信息填充邮件主体并将客户的订单发送给你。代码如列表 10-13 所示。

![](img/43a28cce5475b2f487bf455365567fb6_218.png)

图 10-12：由 `OrderForm_html` 生成的页面

## Order_html

### 列表 10-13：DTML 方法 Order_html

```
<-var standard_html_header>
<form action="index.html">
<center>
<p>感谢您的订单</p>
<input type="submit" value="确定">
</center>
</form>
<html-var standard_html_footer>
```

此页面使用 `dhtml-email` 向你发送客户的订单。其中一个特殊情况是 `OrderForm_html` 中的选择列表：

```
<SELECT size="20" NAME="order:list">
```

该字段与其他字段不同之处在于它在末尾有 "`list`"，这告诉 Zope 将从浏览器提交的值转换为列表。在这种情况下，这是所选书籍的列表。由于 `order` 的值是一个列表，我们使用 `dtml-in` 来遍历它（第 12 行）并查找所选书籍的信息（第 13 行）。（查找是必要的，因为只有 ID 是从表单传递到 `Order_html` 方法的）。为了检索每本书籍的其他属性，我们使用 `dtml-with` 并 `sequence-item` 作为其参数（它包含每本书籍的 ID）。通过命名空间，它返回书籍实例，而 `dtml-with` 将该实例置于命名空间的顶端。在 `dtml-block` 块（第 14-19 行）中，简单的 `dtml-var` 插入每个书籍实例的属性值。

### 10.4.3 发送订单

为了将客户的订单电子邮件发送给你，我们在 Books 文件夹中添加一个邮件主机（mail host），以指定负责发送电子邮件的邮件服务器。邮件主机的主界面如图 10-13 所示。

![](img/43a28cce5475b2f487bf455365567fb6_219.png)

图 10-13：定义邮件主机的主管理界面

# 10.5 扩展你的 Zope 产品的想法

现在你已经创建并运行了第一个 ZClass 和 Zope 产品，你应该能够创建其他的了。这里是一些扩展你的 Zope 产品的点子：

- 扩展产品范围，在你的 `Sales` 产品中创建额外的 ZClasses，例如一个用于创建 CD-ROM 对象的类。
- 扩展自定义管理界面，以允许你添加或删除产品照片。
- 通过创建一个名为 `Orders` 的额外 ZClass 来收集订单数据，允许客户直接从客户界面（`index_html`）下单，从而让你的应用程序对客户更加易用。

# 总结

本章让你更详细地了解了 Zope 类（classes），我们希望这鼓励了你使用 ZClasses 创建自己的产品。虽然 Zope 产品 `Sales` 只是你如何使用 ZClasses 的一个示例，但它演示了使用 Zope 类来创建应用程序的基础知识。

# 11

## ZCatalog

![](img/43a28cce5475b2f487bf455365567fb6_222_0.png)

你使用标准 Zope 安装部分的 ZCatalog 产品，根据你自己的索引来安排 Zope 中的对象。

ZCatalogs 允许你根据对象被索引属性的值对对象进行索引，进行搜索。这些属性可以是文档的内容、属性的值，甚至是 Python 脚本和方法返回的值。在本章中，我们将查看如何创建一个新的 ZCatalog 并检查 ZCatalog 的各个组件。

### 11.1 创建 ZCatalog

要创建一个新的 ZCatalog，打开文件夹的添加（add）菜单并选择 ZCatalog。将出现图 11-1 所示的屏幕。

# 添加 ZCatalog

![](img/43a28cce5475b2f487bf455365567fb6_223_0.png)

与所有 Zope 对象一样，你必须为 ZCatalog 对象指定一个 id；如果你愿意，也可以输入一个标题（title）。

#### 11.1.1 选择词汇表（Vocabulary）

词汇表是从已在 ZCatalog 中编目录的对象中提取出的可搜索单词列表。对象在 ZCatalog 中使用 `TextIndex`（见第 11.2.5.1 节）进行索引，对象中的文本被拆分成单词并存储在词汇表中，这种方式允许目录能够快速找到哪些单词包含在哪些对象中。当你创建一个 ZCatalog 时，可以选择一个现有的词汇表，也可以创建一个新的（见第 11.5 节，“词汇表”）。要执行后者，请选择“Create for me”（为我创建）选项，以便在你的 ZCatalog 内部自动创建一个词汇表对象来存储单词列表。

此选项允许你在多个 ZCatalogs 之间共享一个词汇表——如果你有多个包含 `TextIndexes` 的 ZCatalogs，那么这是一个重要的功能，因为它们共享单个词汇表比每个都拥有一个词汇表要高效得多。要在 ZCatalogs 之间共享词汇表，请在 Zope 层次结构中位于你的 ZCatalogs 位置或其以上的文件夹中创建一个词汇表对象（使用添加菜单），然后在在你创建每个 ZCatalog 时选择此词汇表。

#### 11.1.2 通配符（Globbing）

如果你独立于 ZCatalog 创建词汇表，你可以启用通配符（globbing）的选项，这允许你在 ZCatalog 搜索中使用通配符（例如星号 `*` 和问号 `?`）来匹配部分单词。通常，你会希望启用通配符以提供更强大的搜索能力，但通过禁用它你可以节省内存和磁盘空间。

> 由 ZCatalog 创建的词汇表自动启用了通配符。

## 11.2 ZCatalog 屏幕

你可能已经熟悉 ZCatalog 的几个与其他对象常见的标签页（如图 11-2 所示），包括 Content（内容）、Properties（属性）、View（视图）、Find（查找）、Security（安全）、Undo（撤销）和 Ownership（所有权）。但图 11-2 还显示了五个新标签：Catalog（目录）、Indexes（索引）、Metadata（元数据）、Find Objects（查找对象）和 Advanced（高级），这些将在 11.2.2 到 11.2.6 节中解释。

ZCatalog 中的标签栏

### 11.2.1 Contents 屏幕

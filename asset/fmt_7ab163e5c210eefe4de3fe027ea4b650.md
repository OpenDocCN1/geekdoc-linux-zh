
# 数据库与 Web 479

```html
<table>
  <tr>
    <td class="fieldlabel">Description</td>
    <td width="10">&nbsp;</td>
    <td><textarea name="description" rows="10" cols=80>$property-record->(description)</textarea></td>
  </tr>
  <tr>
    <td class="fieldlabel">Quantity</td>
    <td width="10">&nbsp;</td>
    <td><input type="text" name="qty" size="10" value="$property-record->(qty)"></td>
  </tr>
  <tr>
    <td class="fieldlabel">Value</td>
    <td width="10">&nbsp;</td>
    <td><input type="text" name="value" size="10" value="$property-record->(value)"></td>
  </tr>
  <tr>
    <td class="fieldlabel">Location</td>
    <td width="10">&nbsp;</td>
    <td><<select name="location">$locations</select></td>
  </tr>
</table>
<input type="submit" value="\submode Property"><BR>
EOF
}
```

需要注意的一点是，你还为表单构建了一个弹出菜单的 HTML 选项列表——在这种情况下，是位置的弹出菜单。如果该记录已存在，你通过向相关选项添加 `selected` 文本来设置选中选项。

一旦你完成了所有这些准备工作和构建，最后阶段是将表单导出为 HTML。你在这里使用了原始 HTML，尽管你可以使用 CGI 模块提供的 HTML 构建函数。

表单包含一些隐藏字段。两个定义了表单提交时的模式 `mode` 和子模式 `submode`——取决于你是在添加还是更新记录。你还将将记录的唯一 ID 嵌入到提供的字段列表中。如果记录已存在，你就知道要更新的记录编号。如果记录是新记录，则 `new_record()` 函数将 `0` 设置为数值字段的默认值。当表单提交并调用 `property_add()` 函数时，你需要这些信息。

> 注意
> 请注意标题和提交按钮使用了模式 `mode`，要么是从 `property_edit()` 提供的，要么是在函数的第一行中定义的。这解决了另一个问题——如何正确地为页面和按钮命名。你只需要使用你已经知道的信息。

![](img/6e99147f217994f89499215b2cff677f_506_0.png)

图 17.2 显示我们正在编辑一条现有记录。

![](img/6e99147f217994f89499215b2cff677f_507_0.png)

图 17.2：更新现有记录

# 处理表单并添加记录

一旦表单提交，脚本就会调用列表 17.11 所示的 `property_add()` 函数。该函数构建一个适用于提供数据库接口的记录，用于添加或更新现有记录。

# 列表 17.11：向数据库添加记录

```perl
sub property_add
{
    $propertyrecord =
        $dbh->new_record('property',
        'id' => param('id'),
        'shortdesc' => param('shortdesc') || '',
        'description' => param('description') || '',
        'qty' => param('qty') || 0,
        'value' => param('value') || 0,
        'location' => param('location') || 0,
    );
    if ($propertyrecord->{id} == 0)
    {
        $propertyrecord->{id} =
            $dbh->add_generic('property',$$propertyrecord);
    }
    else {
      $dbh->update_generic_record('property',
        { 'id' => $propertyrecord->{'id'} },
        $propertyrecord);
    }
    property_list();
}
```

第一项工作是通过从表单收集字段参数并将其应用于对应表的空白记录来构建该记录。你可以通过向 `new_record()` 方法提供一个字段/值对的哈希引用来实现。注意，你还使用 `||` 或运算符提供了默认选项，以防字段中的值无效的。

接下来，你确定这是新记录还是现有记录。如果是新的，则它的 ID 为 0，因此你调用 `add_generic()`。记住，你创建属性表是为了在每次添加记录时自动生成一个新 ID。如果你在添加记录时提供编号 0 的 ID，表仍然生成该数字。

如果记录有 ID，那么你必须正在编辑一条现有记录，因此你调用 `update_generic()`。我们没有介绍这个函数，但本质上，它在一个简单的方法中将加载现有记录、使用提供的标准，在这种情况下为 ID 编号、合并数据以及使用单个 SQL 语句更新每个单独字段的步骤结合在一起。你进行的是合并而不是盲目地更新所有字段，这样你就可以提供一个只更新特定字段的简单表单。

一旦你完成了记录的添加或更新，就会调用 `property_list()` 来列出表记录。虽然没有视觉提示显示记录已添加，但任何输入信息的人可能都会列表中发现新记录或更改的记录。如果你想提供视觉确认，请删除对 `property_list()` 的调用。

# 删除现有记录

最后一个函数是 the the the the the1111。

`XML::Parser` 是一个基于事件的解析器。由于它使用了 Expat 库，它还可以对你的 XML 文档提供简单的格式验证，尽管它不会根据文档类型定义 `DTD` 对你的文档进行验证。

# Perl 485 中的 XML 解决方案

在以下简单的 XML 文档上运行此代码将得到输出：

```perl
$ cat simple.xml
<simple>
<paragraph>
</paragraph>
</simple>
```

```perl
$ perl exxmmlp.pl simple.xml
Start: simple
Start: paragraph
End: paragraph
End: simple
```

如你所见，示例输出了起始标签和结束标签的列表。由于你可以在看到不同元素时“注册”你想要调用的函数，因此这些函数可以命名为你喜欢的任何名称。同样注意，函数会提供找到的标签名称以及该标签的属性列表。你可以在解析过程中使用这些信息，以便更显式地传递传递的信息。

# 使用 XML::Parser 转换为 HTML

作为一个基于事件的解析器，`XML::Parser` 模块在需要提取或将元素转换为另一种形式的情况下是理想的。一个很好的例子是将 XML 文档转换为 HTML 格式以便在屏幕上显示。

让我们来看我为一个客户编写的 CGI 脚本，该客户希望将 XML 文档转换为 HTML 显示在他们的网站上。这些文档混合了 XML 和一些 HTML 组件；你可以在列表 18.2 中看到示例。

# 列表 18.2：示例评论文档

```xml
<video>
<main>
<title>Alien Resurrection</title>
<para>Sigourney Weaver, Winona Ryder</para>
<title>Witness the Resurrection</title>
<para>The review...</para>
</main>
<panel>
```

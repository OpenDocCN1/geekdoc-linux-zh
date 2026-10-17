
Phone: `<input type="text" name="phone">` <br>

`<input type="submit">`

</form>

</body>

</html>

这没什么新奇的；它只是带有三个输入字段的表单。这里没有 Embperl。尽管如此，Apache 会使用 `HTML::Embperl` 处理它，因为它位于 `/var/www/html/` 目录下的 `/embperl/` 子目录下。

这是早之前决定的结果，即使用 `HTML::Embperl` 处理 `/embperl/1` 下的所有 `.html` 文件，这会略微降低处理器的效率（但希望能提高程序员的效率）。如果你正在为 `HugeOnlineRetailer.com` 编写服务器，这可能是一个糟糕的选择，但在那种情况下，你可能知道该做出不同的选择。

在这个表单中，`action` 是 `/fdat2.html`，这是一个 Emb HTML 文件。尽管提交了数据，但我们不需要像第 7 章那样的使用 CGI。`Embperl` 允许我们在 HTML 页面内完成相同的事情。

这是处理提交的数据的页面（`/var/www/html/embperl/fdat2.html`）：

```perl
--
# 从 %fdat 获取提交的数据
$name = $fdat{name} | ---
$age = $fdat{age} | ---
$phone = $fdat{phone} | ---
-
<html>
<head>
<title>处理 %fdat</title>
</head>
<body bgcolor="#ffffff">
<h1>处理 %fdat</h1>
```

```perl
[$ if ($name == '' and $age == '' and $phone == '') $]
# 所有字段都填写了！ #
```

感谢填写表单！你输入了：
<br>Name = <b>[+ $name]+</b><br>Age = <b>[+ $age]+</b><br>Phone = <b>[+ $phone]+</b>

```perl
[$ else $]
# 噢，并非所有字段都填写了 #
```

抱歉，但你需要返回并填写所有字段。

```perl
[$ endif $]
</body>
</html>
```

在该文件的开头，脚本从 `%fdat` 获取数据。当数据被提交时，小组件 name 值存储在 `$fdat{name}`，小组件 age 值存储在 `$fdat{age}`，小组件 phone 值存储在 `$fdat{phone}`。

# 第 10 章 Embperl (HTML::Embperl)

![](img/9b05e38e584b6906346_336_0.png)
图 10.5 使用 `%fdat`

然后，在 HTML 文件的 body 中，脚本使用 `[$ if ... ]` 来检查是否收到了所有小组件的值。如果是，则将数据打印给用户。如果不是，脚本会让客户端返回并填写表单。尝试此程序，请检查以下 URL：`http://localhost/embperl/fdat1.html` 或 `www.opensource.com/embperl/fdat1.html`。如果你在这个表单中输入一些信息并点击按钮，你应该看到一个类似于图 10.5 的结果。

## 10.7 其他 Embperl 变量——row 和 $col

`Embperl` 可以使用 `$row` 和 `$col` 生成一维或二维表格。如果在 `<table>` 内部使用了 `$row` 或 `$col`，只要 `$row` 表达式求值不为 `undef`，`Embperl` 就会重复 `<table>` 和 `</table>` 之间的文本。例如，程序代码：

```perl
[$ @nums = (1..5); ]
<table>
<tr><td>[+ $nums[$row]+</td></tr>
```

这意味着开始表格，然后使用 `row` 逐遍历 `@nums`。因为是 `$row`，每个元素被视为一行，因此它重复 `<tr><td></td></tr>`。因此，这是该代码的结果：

```html
<table>
<tr><td>1</td></tr>
<tr><td>2</td></tr>
<tr><td>3</td></tr>
<tr><td>4</td></tr>
<tr><td>5</td></tr>
</table>
```

将代码改为：

```perl
[$ @nums = (1..5); ]
<table>
<tr><td>[+ $nums[$col]+</td></tr>
</table>
```

遍历 `@nums`，因为我们使用了 `$col`，每个元素被视为一列，因此它重复 `<tr><td></td></tr>`。因此，这是该代码的结果：

```html
<table>
<tr><td>1</td></tr>
<tr><td>2</td></tr>
<tr><td>3</td></tr>
<tr><td>4</td></tr>
<tr><td>5</td></tr>
</table>
```

## 超酷的 HTML 魔法！

作为一个示例，我们在表格中显示环境变量。首先，我们展示了没有魔法的情况下如何构建表格，以及魔法如何让生活变得更好。代码可以在 `/var/www/html/embperl/rowcol.html` 中找到：

```html
<html>
<head>
<title>使用 row 和 $col</title>
</head>
<body bgcolor="#ffffff">
<h1>使用 <tt>foreach</tt></h1>
<table border="1"
```

```html
# 遍历 %ENV 的排序键，
# 打印键及其值
[$ foreach $key (sort keys %ENV) $]
<tr><td>[+ $key +]</td>[+ ${key} ]</td></tr>
[$ endforeach $]
```

```html
</table>
```

```html
<h1>使用魔法的 &row; 和 &col;</h1>
# 获取 %ENV 的排序键，将它们放入 @k
# 然后，在表格中定义一行，$row 将
# 魔法地获取 @k 的索引值
@k = sort keys %ENV
<table border="1">
<tr><td>[+ $k[$row] +]</td>[+ ${k[$row]}] +</td></tr>
</table>
</body>
</html>
```


```
<!DOCTYPE HTML PUBLIC "//W3C//DTD HTML 3.2//EN">
<HTML>
<HEAD>
<TITLE>你的标题</TITLE>
<META NAME="description" CONTENT="我的第一个文档">
<LINK REV="made" HREF="mailto:you@yourserver.com">
</HEAD>
<BODY>
<P>你的所有内容在这里！</P>
</BODY>
</HTML>
```

理解有效的 HTML 文档结构是创建无错误 PHP 脚本的第一步。接下来两个部分提供了 HTML 表格和表单的概述。如需深入的 HTML 教程，请访问 http://www.thickbook.com 上的“链接”部分。

### 理解 HTML 表格

HTML 表格遵循与整个 HTML 文档结构一样严格的结构。任何失误（例如缺少标签）都可能导致显示问题。HTML 表格可以将数据组织成行和列。主标签是 `<table>`，它封装了整个表格内容。内部，行用 `<tr>` 定义，单元格用 `<th>` 定义表头或用 `<td>` 定义数据单元。

### 理解 HTML 表单

HTML 表单用于收集用户输入。`<form>` 标签定义了 `<input>`、`<textarea>` 和 `<select>` 等各种输入元素的区域。表单通常使用 GET 或 POST 方法发送到服务器。

默认情况下，会检查一个或多个值。以下是一个名为“drink”的复选框组，其中“coffee”、“tea”、“water”和“soda”是选项：

```
<input type="checkbox" name="drink" value="coffee" checked> coffee
<input type="checkbox" name="drink" value="tea"> tea
<input type="checkbox" name="drink" value="water"> water
<input type="checkbox" name="drink" value="soda"> soda
```

如果“coffee”保持选中状态，用户也勾选了“water”复选框，脚本将接收到 `drink=coffee` 和 `drink=water`。

- 文本区域（Text areas）。显示为一个框，其宽度由 `Cols` 属性的数量决定，高度由 `ROWS` 属性的数量决定。文本区域必须有闭合标签 `<TEXTAREA>`。以下是一个名为 `message` 的文本区域示例，宽度为20个字符，高度为5个字符：

```
<textarea name="message" cols=20 rows="5"></textarea>
```

- 列表框/下拉列表框。这些输入类型带有一个或多个 `<OPTION>` 标签，并且必须以闭合标签 `</SELECT>` 结束。`SIZE` 属性指示 `<OPTION>` 元素的数量。如果 `Size=1`，将出现下拉列表，否则用户将看到一个可滚动列表。如果列表框中存在 `MULTIPLE` 属性，用户可以从列表中选择多个 `<OPTION>`。每个 `<OPTION>` 都有唯一的值。默认 `<OPTION>` 使用 `SELECTED` 属性设置。以下是一个名为“year”的下拉列表，在1999、2000和2001的选项中选中了“2000”：

```
<select name="year" size="1">
<option value="1999">1999</option>
<option value="2000" selected>2000</option>
<option value="2001">2001</option>
</select>
```

当你创建表单时，输入元素的 `NAME` 属性必须都是唯一的。这些元素名称将成为你的脚本解析的变量。如果你先发送了一个名为“my_name”且值为“Joe”的变量，然后又发送了一个名为“coffee”且值为“coffee”的变量，脚本将用后者覆盖前者的值。从那时起，根据脚本的逻辑，你的名字是“coffee”而不是“Joe”。

表单的最后一个元素至关重要：将其提交给脚本的按钮！提交按钮可以是带有文本的默认 3D 表单按钮，也可以使用图像。

要使用显示 SUBMIT 的灰色 3D 按钮，请使用此：

```
<INPUT TYPE="submit" NAME="submit" VALUE="submit">
```

`VALUE` 属性包含显示在按钮上的文本。如果你想让此按钮显示“Send Form”，代码如下：

```
<INPUT TYPE="submit" NAME="submit" VALUE="Send Form">
```

要使用图像作为提交按钮，请使用此代码：

```
<INPUT TYPE="image" NAME="submitme" SRC="button_image.gif" alt="Submit Me" border=0>
```

当用户点击表单提交按钮时，输入字段名称及其关联的值将发送到表单 `ACTION` 中指定的脚本。

## 为代码编写注释

编写代码注释是一个良好的习惯。在 HTML 文档中输入注释可以帮助你（以及以后可能需要编辑你文档的人）跟踪大型文档的区域。注释还允许你在开发过程中为自己写笔记。

HTML 注释会被浏览器忽略，并包含在 `<!-- -->` 标签中。例如，以下注释提醒你随后的代码包含其 Logo 图形：

```
<!-- logo graphic goes here -->
```

同样，PHP 注释会被解析引擎忽略。PHP 注释通常以双斜杠开头。

### 运算符

使用不同类型的运算符为变量赋值值。以下是常用运算符和运算符类型的列表。如需完整列表，请参阅附录 A《PHP 语言》中的“运算符”章节。

### 赋值运算符

你已经见过赋值运算符的工作了：在 `username = “joe”` 中的等号 (=) 就是基础的赋值运算符。

> 单等号并不意味着“等于”。相反，单等号始终意味着“被赋值给”。双等号 (==) 意味着“等于”。记住这一点可以缓解你调试时的头疼问题。

![](img/f8bb5053a1d20d75df488da4d4dbfceb_58_0.png)

其他赋值运算符包括 `+=`、`-=` 和 `.=`：

```
$ex += 1; // 将 ($ex + 1) 的值赋值给 $ex
// 如果 $ex = 2，那么 ($ex += 1) 的值为 3
$ex -= 1; // 将 ($ex - 1) 的值赋值给 $ex
// 如果 $ex = 2，那么 ($ex -= 1) 的值为 1
$ex .= "coffee"; // 拼接（加上）一个字符串。如果 $ex = "I like"
// 那么 ($ex .= "coffee") 的值为 "I like coffee"。
```

### 算术运算符

即使你一生中从未写过一行代码，你也已经知道了大多数算术运算符——它们都是基础数学知识！

- + 加法
- - 减法
- * 乘法
- / 除法
- % 取模，或“余数”

在接下来的示例中，`$a = 5` 且 `$b = 4`。

```
$c = $a + $b; // $c = 9
$c = $a - $b; // $c = 1
$c = $a * $b; // $c = 20
$c = $a / $b; // $c = 1.25
$c = $a % $b; // $c = 1
```

# 第 2 章：基础 PHP 技术

你不需要将数学运算限制在变量上——你也可以使用硬编码的数字。例如：

```
$c = 3 + 4; // $c = 7
$c = 8 * 4; // $c = 32
$c = $a * 10; // $c = 50
```

### 比较运算符

比较运算符用于比较两个值，这并不意外。和算术运算符一样，你已经知道大多数比较运算符：

- == 等于
- != 不等于
- > 大于
- < 小于
- >= 大于
- <= 小于等于

在接下来的示例中，`$a = 5` 且 `$b = 4`。

- `$a == $b`? 不；5 不等于 4。比较结果为 FALSE（假）。
- `$a != $b`? 是；5 不等于 4。比较结果为 TRUE（真）。
- `$a > $b`? 是；5 大于 4。比较结果为 TRUE（真）。
- `$a < $b`? 不；5 不小于 4。比较结果为 FALSE（假）。
- `$a >= $b`? 是；虽然 5 不等于 4，但 5 大于 4。比较结果为 TRUE（真）。
- `$a <= $b`? 不；5 不等于 4，且 5 不小于 4。比较结果为 FALSE（假）。

比较运算符通常与控制语句（if...while）结合使用，根据表达式的有效性执行特定任务。例如，如果你正在编写一个猜数字的程序，并希望脚本在猜中数字时打印“那是正确的数字！”，你可能会包含此代码：

```
// 猜数字
if ($guess == 5) {
    echo "That's the right number!";
}
```

### 逻辑运算符


### 浏览器对此简单示例的显示如图 10-7 所示

`SIZE=1` 列表中唯一可见的项。注意使用选择列表时：第一个列出的项目是浏览器中第一个显示的项目。因此您可能考虑使用诸如“点击选择尺寸”之类的内容作为第一项，尽管没有人会将其选为自己的选择（使用 `SELECTED` 另一个选项来定义默认值）。

还要注意，在 `<OPTION>` 标签之间没有 `<P>` 标签或其他标签。此外，每个菜单项的标签可以包含空格和其他字符，请确保您的脚本能够处理这些键值对。大多数其他值不包含空格。

#### 多选列表示例

如果您为与选择列表相关的单个名称创建一个 `MULTIPLE` 选择列表。例如，在下面的表单中（如图 10-8 所示）：

```html
<SELECT NAME=OS_TYPE SIZE=3 MULTIPLE>
<OPTION>Select Systems at your facility
<OPTION>Linux
<OPTION>Solaris
<OPTION>Other
<OPTION>Windows NT
<OPTION>Windows 95
<OPTION>Macintosh
<OPTION>UNIX
</SELECT>
```

图 10-8 显示了与选择列表相关的单个名称对应的多选择列表。

### 文本区域 (TEXT AREAS)

虽然 `<textarea>` 标签允许用户输入多行文本，但在许多情况下，您可能希望使用 `<INPUT>` 标签的单行文本。`<textarea>` 标签允许用户从列表中选择多个项目。选择菜单提供了几种显示选项，让您控制默认显示哪一个项目以及一次显示多少个项目。

例如，高度为单行项的选择菜单（如图 10-7 所示，`SIZE=1`）将以下拉列表的形式出现。如果您定义了一个高度为三行项的选择菜单（如图 10-8 所示，`SIZE=3`），它将显示为浏览器窗口中一个较大的框，右侧带有滚动条。测试您创建的界面以确保其可用性至关重要。例如，只有一或两个项目的多选型滚动列表是很难使用的。

选择菜单以 `<SELECT ...>` 标签开始，该标签包含表单元素的 `NAME`、列表的 `SIZE`（项的高度）以及如果允许多选的 `MULTIPLE` 选项。

在起始标签 `<SELECT ...>` 和结束标签 `</SELECT>` 之间，使用了 `<OPTION>` 标签。`<OPTION>` 标签的作用类似于 HTML 列表中的 `<li>` 标签，仅用于分隔选择列表中的项目。可以为 `<OPTION>` 添加的唯一参数是 `SELECTED`，它可以包含在一个或多个项目上，使它们成为预设值。下一个使用 `SELECTED` 参数的列表中的第一个选项如图 10-7 所示。

以下是一个示例选择列表；此示例使用了下拉菜单格式的单次选择，它可以替换您表单中的一组单选按钮：

```html
<SELECT NAME= SIZE=1>
<OPTION SELECTED>UPS Ground
<OPTION>UPS Second Day
<OPTION>Federal Express
</SELECT>
```

浏览器对此简单示例的显示如图 10-7 所示。

### 隐藏字段 (HIDDEN FIELDS)

隐藏字段什么都不做——好吧，这种说法有点夸张了。它们在浏览器窗口中完全不显示，因此您看不到显示结果的结果。

即使您看不到隐藏字段，也请确保包含 `<INPUT>` 标签。许多通过隐藏字段完成的操作也可以通过 `<FORM>` 标签的 `ACTION` 参数来完成。但使用 `POST` 方法的普通 `<FORM>` 标签传递的键值对，比添加到 URL 并使用 `GET` 方法发送的数据要容易处理得多。

### 按钮 (BUTTONS)

表单上的按钮会导致浏览器采取操作。当其他元素在等待用户输入数据时，一旦按钮被按下，浏览器就会采取行动。基本上，浏览器可以做两件事之一：使用重置按钮清除表单，或使用提交按钮将数据提交到服务器。

如果您在表单中包含重置按钮，浏览器将清除页面上的所有字段并重新显示。这在许多情况下为用户提供了便利，但并非绝对必要。在浏览器中，创建一个刷新或类似的按钮并不困难。重置按钮是使用 `<INPUT>` 标签配合 `TYPE=RESET` 创建的。没有使用 `name` 选项，因为按下按钮时没有传递用户数据。您可以提供一个 `VALUE`，它将作为按钮上的文本显示。没有提供 `VALUE` 选项，按钮上将显示“Reset”。

浏览器可以的第二种动作是使用提交按钮将表单数据提交到 Web。提交按钮与重置按钮相同，除了不是清除表单外，它会将数据打包并发送到 `<FORM...>` 标签中 `ACTION` 选项列出的 URL。

以下是 `<textarea>` 标签的示例如图 10-9：

```html
<textarea NAME=COMMENTS ROWS=10 COLS=40>
Enter comments here
</textarea>
```

图 10-10 显示了重置按钮和提交按钮；它们的样式如下：

```html
<P>
<INPUT TYPE=SUB Submit Order
<INPUT TYPE=RESET VALUE=Clear Form>
</P>
```

### 表单示例

重置（`Reset`）和提交（`Submit`）按钮完成了 `<FORM>` 标签的列表。在下一节中，将描述一个使用了所有 `<FORM>` 标签的完整表单示例。

接下来的示例使用了上一节描述的所有标签。尽管这是一个非常简单的表单，但它将帮助你看到所有标签是如何结合在一起使用的。在下一节讨论脚本时，此表单也可以提供参考对象。

以下是一个供用户填写的全屏调查卷；图 10-11 显示了调查卷在浏览器中的外观：

```html
<FORM ACTION=http://www.traveltips.com/cgi-bin/survey.pl METHOD=POST>

感谢填写我们的调查卷。所有回答都将保密。摘要结果将在12月1日发布在本网站上。<P>

输入您的姓名（可选）： <INPUT TYPE=TEXT NAME=MYNAME <P>

输入您的电子邮件地址（可选）： <INPUT TYPE=TEXT NAME=EMAIL <P>

<INPUT TYPE=CHECKBOX NAME=SEND_RESULTS > 您是否想通过电子邮件接收一份调查结果副本？<P>

<HR>

您的年龄：

<INPUT TYPE=RADIO NAME=AGE VALUE=UNDER20 > 20岁以下

<INPUT TYPE=RADIO NAME=AGE VALUE=21TO035 > 21-35岁

<INPUT TYPE=RADIO NAME=AGE VALUE=36TO055 > 36-55岁

<INPUT TYPE=RADIO NAME=AGE VALUE=OVER55 > 55岁以上

<P>

您的收入：

<INPUT TYPE=RADIO NAME=INCOME VALUE=UNDER20 > 2万美元以下

<INPUT TYPE=RADIO NAME=INCOME VALUE=21TO045 > 2万-4.万美元

<INPUT TYPE=RADIO NAME=INCOME VALUE=45TO080 > 4.5万-8万美元

<INPUT TYPE=RADIO NAME=INCOME VALUE=OVER20 > 8万美元以上

<P>

在过去的12个月里，您亲自乘坐过哪些航空公司？（请选择所有适用项）<P>

<SELECT NAME=AIRLINES SIZE=5 MULTIPLE>
<OPTION SELECTED>达美航空 (Delta)
<OPTION>美国航空 (American)
<OPTION>联合航空 (United)
<OPTION>英国航空 (British Airways)
<OPTION>意大利航空 (Alitalia)
<OPTION>法国航空 (Air France)
<OPTION>汉莎航空 (Lufthansa)
<OPTION>荷兰皇家航空 (KLM)
</SELECT>

<HR>

选择您最感兴趣的访问（从此列表中选择一个）：<P>

<SELECT NAME=DESTINAT SIZE=3 >
<OPTION>列表中没有
```

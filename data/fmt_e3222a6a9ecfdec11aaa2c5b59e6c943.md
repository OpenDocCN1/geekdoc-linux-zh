
## CGI 程序与 Web 服务器交互

`6.` `CGI` 程序根据输入执行某些操作，生成给客户端的响应（通常是 HTML 文档），并将其传递给 Web 服务器。

`7.` Web 服务器将响应传输给客户端并在（大多数情况下）关闭连接。

在客户端，处理是通过 HTML 标签进行的，这些标签的解释方式与其他标签相同。在服务器端，可以使用 UNIX 环境变量、命令行参数以及标准输入和输出文件在 Web 服务器与 `CGI` 程序之间进行通信。

## 基础表单：标签与属性

`CGI` 表单使用专为此目的设立的 HTML 标签和元素来定义。

### `FORM`

`FORM` 标签开始定义一个表单。在给定的 HTML 页面上定义任意数量的表单，但表单之间不能嵌套。因此，在设计使用表单的 Web 页面时，请考虑信息的逻辑流，如果将复杂的表单划分为连续、更简单的表单有助于帮助用户跟踪其必须指定的信息和选择。

任何其他合法的 HTML 标签都可以嵌入表单定义中。例如，使用标准 HTML 来标记输入字段和表单本身。

属性：

- `ACTION`--指定 Web 服务器机器上将接收并处理表单输入的程序。
- `METHOD`--指定表单如何将其信息发送回服务器。最常见的方法是 `POST`，它将独立于源页面 URL 分离开发送输入信息。另一种方法是 `GET`，它将输入信息附加到 URL 本身。

**提示：**URL 字段有长度限制。除了非常简单的列表选择或查询外，请使用 `POST` 来返回所有表单输入。

- `ENCTYPE`--一个可选元素，告诉浏览器对发送到服务器的信息进行编码的 MIME 类型。默认类型为 `text/x-form-url-encoded`，它将输入信息作为文本传递给 Web 服务器。另一个选项是 `multipart/form-data`。这种 MIME 类型在单个整体消息中支持多种格式；例如，当用户输入要上传到服务器的文件名时就会指定它。

示例：

```
<FORM ACTION="/cgi-bin/new-query" METHOD=POST>
```

### `INPUT`

`INPUT` 标签用于定义表单内的各种类型输入字段。

属性：

- `TYPE`--指定要显示的输入字段类型。合法类型包括 `text`、`password`、`checkbox`、`radio`、`file`、`submit` 和 `reset`。
- `TEXT` 字段接受键盘字符并将其回显到屏幕上。
- `PASSWORD` 字段接受键盘字符，但回显星号而非按键文本。
- `CHECKBOX` 字段用于选择列表。列表中的每个复选框都与其他相互独立的；可以同时选择多个。
- `RADIO` 按钮也用于选择列表；然而，列表中只能选择一个单选按钮。多个选项通常共享同一个变量名。
- `FILE` 字段接受要上传到服务器的本地文件名称。
- `SUBMIT` 按钮允许用户启动将表单信息发送到服务器。
- `RESET` 按钮允许用户取消表单输入并将所有字段恢复为默认值。
- `HIDDEN` 字段不在屏幕上显示。它们用于将持久性信息从客户端传递到服务器并传回客户端，因为 HTML 否则是一种无状态语言。
- `NAME`--为在此字段中要输入的信息分配一个变量名。
- `SIZE`--指定在屏幕上显示的文本或密码字段的输入框大小。大小不限制该字段的输入长度；如果用户输入了更多字符，字段将向左滚动。
- `MAXLENGTH`--指定在文本或密码字段中可以输入的最大字符数。
- `VALUE`--指定与字段关联的文本。这可能是默认文本值、与复选框关联的标签或与重置或单选按钮关联的选项。
- `CHECKED`--指示复选框或单选按钮是否被设置为默认选中。

列表 17.1 显示了表单中可能使用的字段定义和其他 HTML 标签的典型序列。

**列表 17.1 表单的字段定义。**

```
<P>
输入用户名:
<INPUT TYPE=text NAME="userid" VALUE="enter id here" SIZE=15 MAXLENGTH=15>
<P>
和密码:
<INPUT TYPE=password NAME="passwd" VALUE="(required)" SIZE=10 MAXLENGTH=10>
<P>
<INPUT TYPE=checkbox NAME="option1" >选择选项 1
<INPUT TYPE=checkbox NAME="option2" > 如果喜欢也选择选项 2<BR>
<P>
<P>
选择以下内容之一：
<INPUT TYPE=radio VALUE="a" NAME="choice" CHECKED > A
<INPUT TYPE=radio VALUE="b" NAME="choice" > B
<INPUT TYPE=radio VALUE="c" NAME="choice" > C<BR>
<P>
<INPUT TYPE=file NAME="send-file"
<INPUT TYPE=hidden NAME="user-state" VALUE="been here already">
```

这些字段定义将产生图 17.1 所示的屏幕表单。

**图 17.1。**

*作为下拉菜单和滚动窗口的 SELECT 列表。*

## 高级表单

尽管 `INPUT` 是基础字段，但 `SELECT` 提供了许多交互功能。此时有几个方面值得注意。首先，注意浏览器识别的 `SELECT` 标签。其次，注意用于复选框、单选按钮的 `OPTION` 标签。最后，注意 `SELECT` 必须与闭合标签配对。在这些标签之间，除了标签属性外，程序员可以输入在 textarea 显示时显示的变长度文本。用户在输入自己的内容之前必须删除这些文本。

### `TEXTAREA`

`TEXTAREA` 标签用于创建输入自由格式文本的多行字段。Web 页面设计师经常添加 `textarea` 字段来收集用户评论、给作者的电子邮件或类似的非结构化信息。

与 `SELECT` 一样，`TEXTAREA` 需要起始和结束标签。在这些标签之间，除了标签属性外，程序员可以输入在 `textarea` 字段显示时显示的变长度文本。

属性：

- `NAME`--为在此字段中要输入的信息分配一个变量名。
- `ROWS`--指定在屏幕上预留的行数。实际输入可以超过可见的 `textarea` 字段。
- `COLS`--指定屏幕上 `textarea` 字段的字符宽度。

列表 17.3 定义了一个 `TEXTAREA` 字段，图 17.3 显示了在 Netscape 浏览器中生成的表单。

**列表 17.3 定义自由格式 TEXTAREA。**

```
<P>
请在下方添加任何注释或特殊说明：
<P>
<TEXTAREA NAME="terms" ROWS=6 COLS=50>
(注释)
</TEXTAREA>
```

列表 17.2 显示了两个 `SELECT` 列表。

**列表 17.2 定义 SELECT 列表。**

```
请从菜单选择一个选项：
<SELECT NAME="pulldown" SIZE=1>
<OPTION>菜单选项 1
<OPTION>菜单选项 2
<OPTION>菜单选项 3
</SELECT>
<P>
请从滚动窗口选择一个选项：
<SELECT NAME="scrolling" SIZE=2>
<OPTION> 窗口选项 1
<OPTION> 窗口选项 2
<OPTION> 窗口选项 3
</SELECT>
```

**图 17.3**

*浏览器显示的自由格式 `TEXTAREA`。*

## 包含端包含 Server-Side Includes

HTML 并没有定义和调用子程序的规定。然而，可以通过一种名为*服务器端包含*的技术为您的 Web 页面添加类似的功能。

**注意：**大多数流行的 Web 服务器软件都支持服务器端包含，但少数软件不支持。请检查您的服务器文档以验证您的系统是否具有此功能。

这种技术包括要求 Web 服务器执行未包含在当前 HTML 文档中的 HTML 代码。这允许在多个页面之间复用标准列表、表单或其他信息，而不会出现信息更新仅在某些页面生效而其他页面未生效的风险。

服务器端包含的另一个用途是从一个页面动态创建 HTML 作为输出，然后在另一个页面的框架内执行它。这是在 Web 网站中嵌入动态 HTML 的一种有些笨拙的方法，但有时很有用。

服务器端包含的语法如下：

```
<!--#include virtual="/yourfilestring/here"
```

在检索和传输基础 HTML 文档时，服务器会遇到这一行，并将指定文件的内容插入到文档的该位置。

这种技术给服务器系统增加了额外负担。在大多数情况下，这种影响微乎其微；但在繁忙的系统或包含文件非常大的情况下，解释包含的 HTML 所需资源可能会影响服务器性能。

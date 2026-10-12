
该程序将生成类似于图 7.10 所示的网页。当用户点击“点击提交”（Click to Submit）按钮时，程序将执行在 `action` 中指定的程序——在本例中为 `/cgi-bin/nameage.cgi`，它对应的可执行程序是 `/var/www/cgi-bin/nameage.cgi`。提交的数据会被发送程序——这里提交的数据是字段名（`yourname` 和 `age`）以及在这些字段中输入的值。

注意当数据发送到程序时，URL 如下：

```
http://localhost/cgi-bin/nameage.cgi?yourname=J.+Random+Luser&age=55
```

程序名称后面跟着一个问号（`?`）。问号后面是这段看起来很奇怪的文本：

```
username=J.+Random=Lucy+age=55
```

这些数据被称为 URL 编码数据，通过查询字符串（query string）传递给 CGI 程序。它是表单中的数据被编码成一种可以通过 URL 发送到 Web 服务器的格式。

> 如果我们想在程序中查看这些数据，可以通过执行 `query_string()` 获取查询字符串信息。但通常我们不会直接获取数据，而是让 `CGI.pm` 为我们处理这些事务。

查询字符串格式是一系列由等号（`=`）分隔的表单控件名称/值对，每对之间用安培符号（`&`）分隔。因此，在示例中，有两个名称/值对：

```
username=J.+Random+Luser
age=55
```

提交的文本可能包含在 URL 中不合法的字符（例如空格）。这些文本在发送到服务器之前会进行编码。空格被替换为号（`+`），如示例所示，其他不允许的字符被替换为该字符 ASCII 值的百分比十六表示。例如，感叹号字符（`!`）被替换为 `%21`。

URL 中包含跟在“`?`”之后的提交数据，是因为表单创建时使用了 `method="GET"`。`GET` 方法通过 URL 中的查询字符串传递数据。另一种方法是使用 `method="POST"`。该方法通过标准输入而非 URL 将数据传递给 CGI 程序。无论何种方式，`CGI.pm` 都会处理传入的数据。以下是 `nameage.cgi` 的内容：

```perl
#!/usr/bin/perl

# nameage.cgi

use strict;

use CGI `:standard`;

my $name = param(`username`) || `John Doe`;

my $age = param(`age`) || 0;

my @params = param();
```

## 第 7 章 通用网关接口

```perl
print
  header(),
  start.html(`Your Name and Age`,
  "Hello $name, you are $age years old.",
  hr(),
  `The parameters entered are: `,
  b(\@params),
  end.html();
```

此示例中显示的最重要的方法是 `param()` 方法。该方法可以带参数调用也可以不带参数调用。如果调用 `param()` 时带了参数：

它返回为该表单控件提交的值。注意，表单控件的名称是 `"username"`。执行 `param('username')` 返回用户输入到表单的值；如果用户没有在该控件中输入任何文本，则返回空字符串。回想第 4 章，该语句中的逻辑或运算符 `||` 是以下逻辑的简写：

```perl
if (param('username')) ne '' {
  $name = param('username');
} else {
  $name = 'John Doe';
}
```

这确保了无论用户输入什么，`$name` 都是有效的；如果用户没有输入值，则默认为 `"John Doe"`。当调用 `param()` 不带参数时：

```perl
@params = param();
```

它返回表单中所有控件名称的列表——`'username'`, `'age'`。如果用户在表单中输入姓名 `Luser` 和年龄 `55`，`nameage.cgi` 的结果将如图 7.11 所示。让我们查看包含许多表单控件的复杂示例。`/var/www/html/cgi/widgets.html` 示例可以在网上 `http://localhost/cgi/widgets.html` 或 `www.opensourcebook.com/cgi/widgets.html` 找到。它创建了如图 7.12 所示的表单。

## 表单控件示例

在 HTML 开始之后，我们看到了表单的创建：

```html
<form action="cgi-bin/widgets.cgi" method="post">
```

这意味着当提交表单时，表单中的所有数据都会发送到程序 `widgets.cgi`。然后创建了一系列控件：

- 文本控件（text widget），用户可以在其中输入文本的单行框：`<input type="text" name="language" value="Perl">`
- 文本区域（textarea），用户可以在其中输入多行文本的多行区域：`<textarea name="comments" cols="20" rows="5"></textarea>`
- 单选按钮（radio button），允许用户从多个选项中选择其一：`<input type="radio" name="coolness" value="cool">`, `<input type="radio" name="coolness" value="very cool">`, `<input type="radio" name="coolness" value="ice cold" checked>`
- 复选框（check box），开启/关闭选择：`<input type="checkbox" name="learnmore" value="yes" checked>`
- 使用 `<select>` 标签定义的两个菜单：

```html
<select name="operating_system" size="1">
<option>Linux</option>
<option>Solaris</option>
<option>HPUX</option>
</select>
```

```html
<select name="animal" size="3" multiple>
<option>Penguin</option>
<option>Camel</option>
<option>Llama</option>
<option>Panther</option>
</select>
```

第一个是菜单按钮，点击它后选择所需的项目。它之所以被称为菜单按钮是因为 `size` 被设置为 1，因此在点击控件之前，GUI 中只显示一个项目。另一个 `<select>` 控件是滚动列表框——因为 `size` 为 3，框中显示三个选择，其他的可以通过滚动查看（嗯，滚动列表框……那是该控件的好称）。注意这里标明了 `multiple` 属性，这意味着用户可以通过按住 Ctrl 键点击额外的项目来选择多个选项。在获取值时，可以选择多个项这一事实变得非常重要。

创建了提交和重置按钮：

```html
<input type="submit" value="Submit Form">
<input type="reset" value="Reset Form">
```

如果点击提交按钮，数据将发送到程序 `widgets.cgi`。如果点击重置按钮，表单将恢复到原始值。关联的 CGI 脚本位于 `/var/www/cgi-bin/widgets.cgi`。你可以在 `http://localhost/cgi/widgets.html` 或 `www.opensourcebook.com/cgi/widgets.html` 找到它。首先我们看到一些重要的内容：

```perl
#! /usr/bin/perl
# widgets.cgi
```

```perl
use strict;
use CGI `:standard`;
```

这是一个 Perl 脚本。是的！我们像之前一样在标准模式下 `CGI.pm` 模块。然后我们看到了获取提交数据的代码：

```perl
# 获取表单数据
my $language = param('language') || 'Perl';
my $comments = param('comments') || '';
my $coolness = param('coolness') || 'Ice Cold';
my $learnmore = param('learnmore') || 'no';
my $operating_system = param('operating_system') || 'Linux';
```

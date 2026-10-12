
`$ chmod 755 /var/www/html`

## 6.3 基础知识

在使用 WML 时，你应该只编辑 `.wml` 文件，*而不是* `.html` 文件。后者是前者的输出。

第二部分 静态

### 6.3.1 构建 HTML

示例存储在以 `.wml` 扩展名命名的文件中。为了生成 HTML，从 WML 源码，更改一个模板 HTML 命令：

```
$ wmk
```

对于所有以 `.wml` 结尾的文件，使用以下命令：

```
$ wmk -o index.html
```

### 6.3.2 WML 阶段

WML 编译是一个九阶段的过程。

- **阶段 1：源码读取和包含** 读取被包含的文件。
- **阶段 2：高级宏处理** 处理宏。
- **阶段 3：编程结构扩展** 执行嵌入 Perl 代码 代码

对于你不希望被剥离的文本，可以使用 `<nostrip> ... </nostrip>` 标签，第 8 阶段会对其原样保留，除了 `<nostrip>` 标签本身。参见 `wml.p8.htmlfix(1)`。

第 9 阶段：标记代码分割和输出生成。允许将输出分割到多个文件中，也称为切片（slice）。如果你需要生成一个英文的 HTML 文件和另一个德语的 HTML，这非常方便。这种功能很有用，但对我们来说比较高级，如需更多信息，请参见 `wml.p9.slice(1)`。

### 6.3.3 `<protect>` 标签

有时我们不希望 WML 处理所有的代码。一个实例将是 shell 脚本的列表——WML 会看到 shell 脚本中的注释并将其剥离。这些部分可以封装在 `<protect>...</protect>` 标签中，WML 将不会处理它们，除非移除 `<protect>...</protect>` 标签本身。

## 6.4 创建模板

在 WML 中，为网站创建和维护整体的视觉效果模板是简单的。页面特定部分的 HTML 代码可以包含在每个页面中，如果页眉、页脚、左侧和右侧栏等在每个页面上看起来相同：

```
#include "header.wml"

#include "banner.wml"
```

WML 对单引号和双引号有重要的区分。单引号意味着文件仅从当前工作目录加载，这可以用于强制加载本地文件。如果使用双引号，WML 将在 `-I` 选项（include）之后的所有目录搜索文件。默认情况下，首先搜索当前工作目录。接下来，如果找不到文件，将按照 `-I` 选项指定的顺序搜索目录，并使用第一个文件名。在之前的示例中，如果当前工作目录中存在 `banner.wml`，则使用那一个。

让我们从一个包含页眉和页脚的简单示例开始。为了换换口味，文件的主体打印“hello, world!”。头部文件 `/var/www/html/wml/head1.wml` 仅仅是 HTML 页面头部的基础 HTML：

```
<html>
<head>
<title>WML hello1.wml</title>
</head>
<body> bgcolor=#ffffffff
```

同样，页脚（`/var/www/html/wml/foot1.wml`）是：

```
</body>
</html>
```

再次，这只是简单的 HTML，优雅地结束了在 `head1.wml` 中开始的代码。WML 程序为 `/var/www/wml/hello1.wml`：

```
#include "head1.wml"
hello, world!
#include "foot1.wml"
```

当调用时，`wml` 调用 `wml`，`wml` 在第 1 阶段包含了 `head1.wml`；然后添加了来自 `hello1.wml` 的主体“hello, world!”；最后包含了 `foot1.wml`。

要构建 HTML，请执行 `wmk` 命令：

```
$ wmk hello1.wml
wml -n -o hello1.html hello1.wml
```

这生成了 `/var/www/html/wml/hello1.html`，其内容为：

```
<html>
<head>
<title>WML hello1.wml</title>
</head>
<body> bgcolor=#ffffff>
hello, world!
</body>
</html>
```

通过访问 `http://localhost/wml/hello1.html` 或 `www.opensourcewebbook.com/wml/hello1.html` 在浏览器中加载此。结果可以在图 6.1 中看到。

![](img/9b05e38e58495be06a08eeb2b6906346_175_0.png)

`hello11.wml` 中文本“hello, world!”上下两个空行并没有出现在生成的 `hello11.html` 中，因为 WML 的功能之一是移除任何多余字符，例如空格。此外，在 `head1.wml` 中，背景颜色 `#ffffff` 没有用双引号括起来（在有效的 HTML 中应该是应该是），所以 WML 很好地在生成的 `hello11.html` 中加入了正确的引号。这是 WML 的一个非常棒的功能，尽管当然你不应该依赖它来修复所有问题。

### 6.4.1 更改模板文件

尽管所有这些都是静态 HTML，但并不是每个页面都有相同的标题。WML 允许你向文件传递参数：
`#include "head.wml" title="Just Say Hello"`

那么，在 WML 文件 `head1.wml` 中，传递的值作为 `$(title)` 可用（这些 WML 变量看起来和 shell 程序中的一样）。这些括号很重要。是 `$(title)`，而不是 `$title`。

使用传递参数的新头部文件是 `/var/www/html/wml/head2.wml`。在 `<title>` 标签之间，`$(title)` 的值会被求值。在这个示例中，背景颜色也通过 `$(bgcolor)` 传递到文件中。

```
<html>
<head>
<title>$(title)</title>
</head>
<body bgcolor=$(bgcolor:-#-ffffff")
```

背景颜色使用语法 `$(bgcolor:-"#ffffff")` 设置。这种类似 shell 的语法意味着“如果 `$(bgcolor)` 有值，则使用它的值，否则使用默认值 #ffffff。”

同样，在页脚 `/var/www/html/wm1/foot2.wml` 中，可以通过 `$(author)` 变量提供作者：

```
<hr>
Written by: <b>$(author)</body>
</html>
```

包含这两个文件的 WML 文件是 `/var/www/html/wm1/hello2.wml`：

```
#include "head2.wml" title="WML hello2.wml"
```
hello, world!
```
<hr>
```
```
<pre>
here is some
</pre>
```
```
#include "foot.wml"
```

要构建 HTML，执行 `wmk` 命令：

```
$ wmk hello1.wml
wml -n -o hello1.html hello1.wml
```

这生成了 `/var/www/html/wml/hello1.html`，其内容为：

```
<html>
<head>
<title>WML hello1.wml</title>
</head>
<body bgcolor=#ffffff>
hello, world!
</body>
</html>
```

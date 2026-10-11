

## 示例 E.4（续）

```perl
my @students = (
    Student->new(
        name     => "Bob",
        idnumber => "123",
        major    => "math",
        courses  => [qw(calculus topology matrices)],
    ),
    Student->new(
        name     => "Jane",
        idnumber => "321",
        major    => "computer science",
        courses  => [qw(automata algorithms java)],
    )
);

get '/t' => sub {
    my $template_data = {
        students => \@students,
    };
    template 'index', $template_data;
};
1;
```

## 解释

1.  我们处于 Example 模块中，因此我们将定义 *Example* 包。
2.  和以前一样，*Example.pm* 将从 Dancer 导入 *syntax* 组来设置路由处理程序。
3.  这次我们还要使用之前创建的 *Student* 模块。
4.  创建了一个词法作用域的数组。另一种方法（*类似于 $VERSION 的 our*）是包变量，但我们不希望其他模块能够影响我们的学生列表。Dancer 应用程序中该部分（即此文件）的路由处理程序将能够与此数组交互，但其他人不能。该数组填充了我们在第 14 章“祝福那些事物！”（面向对象的 Perl）中首次看到 *Student* 时使用的相同两名学生。
5.  为根路径定义了 *get* 处理程序。定义了一个匿名 *子引用*，以便在请求根路径时运行。
6.  创建了一个匿名哈希引用，并将其赋值给词法变量 $template_data。
7.  哈希键 *students* 与 \@students 数组关联。在 Perl 中构建数据结构时，我们必须传递非标量数据的引用，因此 \@students 数组通过引用传递。
8.  指示 Dancer 在请求根路径时渲染 *'index'* 模板。这次，新的变量 $template_data 也会发送到模板。在模板内部，变量 *students* 将指代我们放入 $template_data 中的数组引用。

为了使用这个新脚本，我们还将不得不修改模板。毕竟，Dancer 不会神奇地知道该如何处理我们提供的模板数据。

## E.1.2 模板处理

**模板处理**是一种将**表示**资源的方式与**生成**资源的方式分离开的方法。在我们的例子中，所表示的学生列表直接在模块中定义。每次我们退出并重启应用程序时，学生数据都会重置，因为程序将被重新编译。

替代方案包括将数据存储在文件中、放入数据库，甚至存储在别人的网络上！我们可以轻松地为我们的网站编写脚本，从另一个网站获取数据——RSS 阅读器的运作方式就是这样。

你还可以以不同方式表示资源。在这种情况下，我们将假设我们希望在 HTML 形式中查看学生，因为我们假设使用的是浏览器。然而，如果我们想创建学生的 RSS 源，我们可以使用不同的模板配合同一组学生来生成符合 RSS 标准的 XML。或者我们可以将它们表示为 JSON。基于 Web 的 RSS 阅读器通过从别人的网站收集资源来**生成**资源；并通过将它们重新打包为 HTML 形式来**表示**这些资源。

因此，我们确实希望在某处获取数据，并在另一处表示它。这在 CGI 时代是无法做到的；在当时，你不得不为不同的事物编写不同的脚本——而 CGI 只提供 HTML 辅助功能！

模板处理是一种向文本文件发送数据，并根据发送的数据一致地构建这些文本文件的方法。我们定义一个模板，其中包含诸如页眉和页脚 HTML 等公共元素，以及用于表示资源的 HTML，并将使一个资源不同于另一个资源的数据项放入其中。在本例中，使用 `Template` 模块进行模板处理（参见 http://template-toolkit.org 获取更多信息），因此我们安装该模块：

```
cpanm Template
```

接下来，我们需要修改 `config.yml`，使其包含 `template: "template_toolkit"`。以下是 `config.yml`，为简洁起见已去除注释。鼓励读者阅读自己副本中的注释。（这也是我们安装 YAML 模块的原因。）

## 示例 E.5

*(config.yml（节选))*

```yaml
appname: "Example"
layout: "main"
charset: "UTF-8"
template: "template_toolkit"
```

## 解释

1.  YAML 是一种简单的数据定义语言，使用键值语法。这一行将应用程序名称定义为“Example”。这是由 Dancer 生成的。
2.  Dancer 支持布局。这基本上是一个包裹其他模板的模板。在 CGI 中，我们会有 *header.html* 和 *footer.html*，但由于标签不匹配，这太容易出错。使用包装器要简单得多。此应用程序配置为使用名为“main”的布局。可以在 *views/layouts/main.tt* 中找到它。
3.  HTTP 指定资源使用的字符集。（实际上，它指定的是编码，但称之为字符集。这是一个古老的错误，现在已为时过晚，无法更改。）Dancer 配置为使用 UTF-8 编码所有内容，这是目前首选的编码。
4.  Dancer 配置为使用“*template_toolkit*”模板系统。之前是“*simple*”模板系统，但“*simple*”没有循环功能，而我们想要输出一个数组。

当 Dancer 应用程序启动时，配置从 *config.yml* 读取。这为 Dancer 设置了默认的一组配置，在此情况下，我们配置了模板系统。还有许多其他配置选项，甚至可以进行配置使其在不同环境中使用不同的值。这是一种机制，使我们能够上线网站，而不会意外向用户显示仅对调试系统的开发者有用的杂乱错误。

现在我们已经告诉它使用哪个模板系统，我们将注意力转向 *views* 目录。它包含所有模板，如果你不告诉 Dancer 去其他地方寻找，它将会查找此处。**视图（View）**是指能够以不同格式显示同一资源的术语。可能存在 *JSON* 视图、*HTML* 视图、*RSS* 视图等。为了保持简单，我们将保留结构不变，但为每种支持的格式在 *views* 中添加子目录通常有益。

默认的 *index.tt* 可以打开以查看构成欢迎页的 HTML，当应用程序首次运行时会在浏览器中显示（图 E.1）。此文件的一部分使用 *Template::Toolkit* 的 `<% %>` 语法，Dancer 的“*simple*”模板系统也使用这种语法，以输出如 Dancer 版本和右侧的环境数据等信息。

现在我们正确使用 *Template::Toolkit*（这是 *index.tt* 中 *tt* 的含义），我们可以用其他有用的模板替换 *index.tt*。以下示例列出了新的 *index.tt*。

## 示例 E.6

```html
<div id="page">
    <div id="content">
        <div id="header">
            <h1>Student List</h1>
        </div>
        <div id="students">
            [% FOREACH student IN students %]
            <h2>
                [% student.name %]
            </h2>
            <dl>
                <dt>ID</dt>
                <dd>[% student.idnumber %]</dd>
                <dt>Major</dt>
                <dd>[% student.major %]</dd>
                <dt>Address</dt>
                <dd>[% student.address %]</dd>
                <dt>Tuition</dt>
                <dd>[% student.tuition %]</dd>
                <dt>Course</dt>
                [% FOREACH course IN student.courses %]
                <dd>[% course %]</dd>
                [% END %]
            </dl>
            [% END %]
        </div>
    </div>
</div>
```

## 解释

1.  此文件不以 `<html>` 或 `<!DOCTYPE>` 开头。相反，它以 `<div>` 开头。该文件将导入 `views/layout/main.tt`，因此只需包含特定于学生列表页面的 HTML。`main.tt` 包含 `DOCTYPE` 和 `<html>` 元素。这使我们能够创建新页面，同时保持一致的主题和框架。
2.  通过保留部分原始 HTML，可以避免进行许多额外的样式设计。我们将保留其中的 `content` `div` 及其内部的 `header` `div`，这将使新页面看起来与旧页面相似。
3.  创建了一个新的 `div`，其 `ID` 为 `students`。如果希望的话，我们稍后可以使用 `CSS` 对此进行样式设计。
4.  `Template::Toolkit` 定义了 `FOREACH` 指令，其行为类似于 Perl 中语法不同的 `foreach` 循环；例如，使用 `IN` 代替 Perl 语法中的括号。`Template::Toolkit` 期望 `students` 是一个 `arrayref`（数组引用），并对其进行迭代，依次将每个元素赋值给 `student` 变量。`Dancer` 使用 `<% %>` 语法配置 `Template::Toolkit` 以识别模板区域；其他所有内容均作为纯文本输出。
5.  这是 `FOREACH` 循环体的第一行。它定义了一个 `<h2>`。对于 `students` 数组中的每个学生，此行将输出一次。



```perl
@sound_files = sort &get_dir($dir_name, $incl_patt);

foreach ($file (@sound_files)) {
    print "<LI>", &format_input("radio", "file", $file), $file, "\n";
}

print "</UL>";
```

```perl
# 给定名称和值，打印选择框
sub format_select {
    ($name, @values) = @_;
    print "<SELECT name=$name>\n";
    foreach (@values) {
        print "<option value=\"@\">@</option>\n";
    }
    print "</SELECT>\n";
}
```

```perl
# 格式化输入
sub format_input {
    ($type, $name, $value) = @_;
    return "<input type=$type name=$name value=\"$value\">";
}
```

```perl
}
print "</UL>\n";n}
```

```perl
# 打印某种类型、变量名和默认值的 INPUT 小部件
sub format_input (
local($type, $html_name, $html_value) = @_;
return("<INPUT TYPE=$type\$html_name\" VALUE=\$html_value>");
)
```

```perl
# 给定一个 HTML 变量名和选项数组

# 给定一个目录和一个正则表达式，返回该目录下
# 匹配该模式的文件列表。
sub get_dir {
local($dir, $incl_patt) = @_;opendir(DIR, $dir);
if ($incl_patt ne '') {
    grep(\$incl_patt/, readdir(DIR));
}
else {
    readdir(DIR);
}
```

`audioconv.pl` 脚本可以以两种模式运行，取决于 CGI 环境变量 `QUERY_STRING` 的状态：

- 如果该变量为空，`audioconv.pl` 假设用户首次连接到 AudioConvert 页面，并打印图 11-3 所示的表单。

- 如果该变量包含文件和格式 HTML 变量的表单值，`audioconv.pl` 会打开指向 Sox 转换程序的管道，发送相应的 MIME 类型并将音频数据传输到客户端。

尽管这个示例比 POST 方法的示例要长得多，但它与服务器的接口同样简单。事实上，如果你检查这两个程序中负责处理 HTML 数据的子程序，你会发现它们几乎是完全相同的。这是编写 CGI 脚本的另一个吸引人的地方：由于必须完成的任务是重复的，一旦你写了完成首次任务的代码，这些代码几乎可以无限重用。

> 如果你对数字音频感兴趣，Sox 是一个非常棒的程序。它不仅可以将音频文件转换为许多不同的格式，还可以用它来更改音频文件的基本特性，例如采样率和音量。Sox 还可以对样本应用各种过滤器来消除噪声并添加特殊特效。作为使用 Sox 和编写 CGI 的练习，请为 `audioconv.pl` 添加一个通往 Sox 一或多个其他功能的接口。要获取 Sox 语法和功能的完整说明，请查看 Sox 主页。第 8 章“真多媒体：添加音频与动画”中也讨论了 Sox。

## 动态生成页面

CGI 的用途远不止编写表单和处理器。你还可以使用 CGI 程序动态生成新的 HTML 页面，这是一项极其有用且强大的能力。通过动态文档，你可以根据意愿更改 Web 页面的外观、界面和功能。你还可以利用它们来扩展 Web 的功能，添加传统媒体中难以或无法实现的功能。

# 414 UNIX Web 服务器书籍

在示例 11-3 中，`audiocov.pl` 脚本写入了一个带有表单的页面是因为 `QUERY_STRING` 变量为空。这是一个动态文档的简单示例，因为页的内容取决于服务器上声音目录中的文件。脚本每次运行时都会生成新的文件列表；这样做是为了避免在静态页面中维护单独列表的麻烦，因为静态列表可能会与目录的实际内容不同。使用下一节将讨论的 `CGI.pm` 编写 HTML 变得简单得多。

尽管 `audiocov.pl` 生成的 HTML 是用于表单，但你可以编写无需输入的 CGI 脚本来解决类似的问题。动态创建文档而不是手动创建文档的主要原因是：

- 展示某些变化资源的当前状态。

- 避免编写那些手动编写很困难、恼人或无法实现的页面的麻烦。

任务可能简单到在页面上附加当前日期和时间，也可能复杂到从一天 Usenet 新闻的数百兆数据中构建一份个人报纸。当然，为了这种灵活性付出的代价是每次检索页面时运行 CGI 程序的开销。

此外，动态创建的文档还有一个进一步的缺点：它们无法被缓存（服务器会自动将其标记为不可缓存）。随着组织将所有 Web 请求引导通过本地缓存服务器以减少外部流量，这个问题将变得越来越重要。

尽管有这些缺点，以这种方式使用 CGI 程序是解决维护大型复杂网站时遇到的许多问题的最佳（或唯一）解决方案。其中其中一个问题是用户之间客户端软件、可用带宽以及他们偏爱的数据格式存在巨大差异。尽管 HTTP 协议包含了一些对此类协商的支持，且 `HTTP-NG` 更多，但很少有 WWW 客户端和服务器充分利用它。

# 第 11 章：程序员的高级表单 415

从 WWW 到 SQL，组织希望将他们传统的 MIS 部门和数据库连接到 Web。由于这个原因，基于 SQL 的关系数据库的 CGI 接口变得越来越重要。目前，某些 CGI 脚本可以提供对所有主要关系数据库的只读访问，但完全集成一个复杂的数据库和网站通常需要商业产品。集成这些系统已成为 Web 社区的热点，并且有许多商业和免费的解决方案。

在商业方面，Sybase 和 Oracle 等大型供应商已经开发了访问其数据库系统的工具。然而，存在许多免费的替代方案。在这些方案中，最全面的是 DBI 项目，它为基于 SQL 的数据库系统提供了应用程序接口，并已经为主要系统编写了许多驱动程序。DBI 驱动程序适用于 Oracle、Sybase、mSQL（一个免费数据库）、DB2、Empress 等以及世界上的其他系统。

在本节末尾包含的示例 CGI 脚本 `condit.pl` 通过允许你执行以下操作，解决了客户端偏好与浏览器能力匹配相关的问题：

- 在 URL 中嵌入一个或多个标记。

- 在简单的宏语言中测试这些标记。

## 第 11 章：程序员的高级表单 417

选择首页类型：

- 仅限图形界面 (imagememap)

    - <a href="cgi-bin/condit.pl/NOTEXT/home.html">GIF 图形</a>

    - <a href="cgi-bin/condit.pl/USEJPEG:::NOTEXT/home.html">JPEG 图形</a>

- 带有文本的图形界面

    - <a href="cgi-bin/condit.pl/home.html">GIF 图形</a>

    - <a href="cgi-bin/condit.pl/USEJPEG/home.html">JPEG 图形</a>

- <a href="cgi-bin/condit.pl/NOGRAPICS/home.html">纯文本界面</a>

当用户激活此标记中的某个超链接时，服务器会运行 `condit.pl`，并将 `/cgi-bin/condit.pl` 之后的所有 URL 信息存入 `PATH_INFO` 环境变量中。`condit.pl` 将 `PATH_INFO` 变量解释为选项标志列表，随后跟一个相对 URL。该相对 URL 指向需要应用这些选项的 HTML 文档。

脚本会打开该文档并扫描 HTML 注释标记 `<!--` 内的命令。每个命令都会测试一个或多个标志是否存在，如果命令及其标志评估为真（true），则包含一段文本。发送给 `condit.pl` 的命令必须单独成一行，并后跟一个用逗号分隔的待测试标志列表。你可以在表 11-1 中找到 `condit.pl` 命令及其功能的完整列表。由于 `QUERY_STRING` 变量为空，`audiocv.pl` 脚本写入了一个带有表单的页面。

| 命令 | 说明 |

| :--- | :--- |

| `INCLUDE-IF` | 如果所有标志都匹配，则包含此部分。 |

| `INCLUDE-ANY` | 如果有任何一个标志匹配，则包含此部分。 |

| `INCLUDE-IF-NOT` | 如果没有任何标志匹配，则包含此部分。 |

| `INCLUDE-IF-NOT-ALL` | 如果并非所有标志都匹配，则包含此部分。 |

表 11-1：`condit.pl` 可识别的命令。

## 示例 11-4：`condit.pl`，一个允许条件包含标记代码的 CGI 脚本。

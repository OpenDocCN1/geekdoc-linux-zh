
```perl
$ if ($name) $
# 既然 $name 有值，所以我们有一个记录
<font color="#00000">产品: [$prod_id]</font><br>
<table border="0" cellspacing="0"><tr><th>Name</th><td>[$name]</td></tr><tr><th>Category</th><td>[$category]</td></tr><tr><th>Description</th><td>[$description]</td></tr><tr><th>Price</th><td>[$price]</td></tr><tr><th>Manufacturer</th><td>ID: [$man_id]<br>
<td>[$man_name]<br>
<td>[$city]<br>
<td>[$state]<br>
<td>[$zip]</td></tr></table>

$ else
# 数据库中没有找到 $name
请输入有效的产品 ID
$endif
```

### 10.9.3

- `$escode` 一个影响 HTML- 和 URL- 转义的值。
- `LOG` 日志句柄——打印到此句柄以添加到日志（默认为 `/tmp/embperl.log`）。
- `OUT` Embperl 的输出流——任何最终由服务器发送的内容（与 `[+ ... +]` 块相同）。
- `%http.headers.out` 包含要在标头的键和值的哈表。重定向可以通过 `$http.headers.out{Location} = "http://www.onsight.com/";` 完成。

### 10.9.4 XML 和 XSLT 支持

从 2.0b4 版本开始，Embperl 与 XML 和 XSLT 集成。详情请查看 Embperl 页面或 perdoc。

## 10.10 总结

Embperl 是一种灵活且中等简单的嵌入服务器端网页的方法。它基于 Perl 并类似于 mod.perl，因此它建立在非常优秀的知识基础之上。它很有用，但与你已经熟悉的内容并没有太大。然而，正如我们在 SSI 中看到的那样，方法不止一种，而且还有其他嵌入 HTML 编程的方法，因此在决定在系统中使用什么之前，请继续阅读。

## 10.11 资源

网站

Embperl 主页：`perl.apache.org/embperl/`

Embperl 德语主页：`www.ecos.de/embperl/`

# Mason (HTML)

## 11.1 简介

`HTML::Mason`（也称为 Mason——参见 [masonhq.com](http://masonhq.com/)）是由 Jonathan Swartz 创建的一个 Perl 模块。它的功能与 Perl 类似：在 HTML 页面中包含 Perl 代码。以下是 Mason 的一些特性：

- **简单的嵌入 Perl 语法**——HTML 文件可以利用 Perl 的功能（包括标量、数组、哈希等）、复杂数据类型和控制结构。
- **模块化页面**——创建类似于子程序的代码，并称为组件，用于生成页眉、页脚、菜单等。
- **参数处理**——它提供了对 GET/POST 参数的轻松访问，包括分配默认值和触发错误。
- **模板和过滤器**——可以创建模板并应用于整个站点或站点的部分。
- **面向对象技术**——可以使用 Perl 的功能及其面向对象的特性。
- **缓存**——当页面或组件被缓存时，下次请求该页面或组件，将执行缓存的版本。
- **预览**——可以使用内置的预览器来查看页面，使用许多客户端和请求条件。
- **开发/生产模式**——Mason 可以配置为使用开发服务器或区域。

### 11.1 Mason 与 Perl 的比较

Mason 和 Perl 非常相似：两者都将 Perl 代码嵌入到 HTML 页面中。这使得 Web 页面的创建分为两个部分：网页设计师（图形艺术家）专注于创建静态（且易用的）HTML，而程序员专注于添加代码。

Mason 和 Perl 都允许使用 Perl 变量、复杂数据类型以及类和对象（如果想使用 Perl 的面向对象特性）。两者都提供了 Apache 接口来创建会话并将模板应用于整个站点或站点部分。两者都在 HTML 中缓存编译 Perl 代码，仅在文件时间戳更改时重新编译。

为什么要使用两者？答案是开源的优势在于我们有选择，所以我们可以选择 Perl 或 Mason……我们尝试指出这两种方法之间的区别，但我们认为最重要的区别在于：风格和偏好。由于开发站点时遇到的几乎每种都可以用 Perl 或 Mason 解决，选择取决于你的喜好。如此，Perl 的重点在于轻松生成 HTML，它以速度和易用性闻名。它与 HTML 紧密集成，允许程序员动态创建表格和 URL 以及其表单控件。

Mason 倾向于更全局的方法——它不仅仅是一个模板工具。Mason 的方法目标不仅在于易用，更在于一个更灵活的系统，允许程序员以“自己的方式”编码。Mason 对新用户来说可能有点复杂且令人敬畏，但良好的在线文档和热心的社区有助于新程序员学习其丰富的功能集。

Mason 的一个重要特性是，通过特殊标记（`<init>`，稍后介绍），可执行代码可以位于 HTML 页面的底部，但会被执行。这里的模型是：在 Web 设计店中，HTML 由设计师创建；然后程序员进来添加代码。通过 Mason，许多代码可以简单地添加到 HTML 文件的底部，这样当设计师更新 HTML 时，他们就不处理 Mason 代码。

## 11.2 安装

许多发行版尚未安装 Mason（包括 Red Hat），因此我们将手动安装它。不过，必须安装另外两个模块：`MLDBM`（多级数据库管理器）和 `Params::Validate`。`MLDBM` 是一个允许存储和检索多维数据结构的 Perl 模块。Mason 使用 `MLDBM` 来存储其缓存文件。

要安装 `MLDBM`，请从 [cpan.org](https://www.cpan.org/modules/by-module/MLDBM/) 获取最新版本（本书编写时为 2.00）。将 `MLDBM-2.00.tar.gz` 保存到 `/tmp`。然后，以 root 身份执行：

```bash
# cd /tmp
# xvzf MLDBM-2.00.tar.gz
# cd MLDBM-2.00
# perl Makefile.PL
# make
# make test
# make install
```

接下来安装 `Params::Validate`。Mason 使用该模块验证函数调用参数。从 [cpan.org](https://www.cpan.org/modules/by-authors/id/D/DR/DROSKY/) 获取可用版本（编写时版本为 0.07）。接下来下载 `Params-Validate-0.07.tar.gz` 并保存到 `/tmp`。然后，以 root 身份执行：

```bash
# cd /tmp
# xvzf Params-Validate-0.07.tar.gz
# cd Params-Validate-0.07
# perl Makefile.PL
# make
# make test
# make install
```

现在你的系统已为 Mason 准备就绪。

检查 `MLDBM`...ok

检查 `Data::Dumper`...ok

检查 `Params::Validate`...ok

正在创建 Mason 文件。

检查现有配置...未找到。

打印了更多内容，然后提示：

搜索现有配置模块依赖？[y]

配置文件 `[/etc/httpd/httpd.conf]`

运行用户 `[nobody]`

运行用户组 `[apache]`

运行端口 `[8]`

## 11.3 Apache 配置

必须配置 Apache 像处理 Perl 一样处理 Mason。我们将选择一个目录，并让 Mason 处理该目录下所有的 `.html` 文件。

首先，为 Mason 创建目录：

```bash
$ mkdir /var/www/html/mason
$ chmod a+rx /var/www/html/mason
```

以 root 身份将以下内容加入 `/etc/httpd/httpd.conf`：

```apache
PerlSetVar MasonCompRoot /var/www/html/mason
PerlSetVar MasonDataDir /var/www/misc/mason
PerlModule HTML::Mason::ApacheHandler
<Directory /var/www/html/mason>
    SetHandler perl-script
    PerlHandler HTML::Mason::ApacheHandler
</Directory>
```

加载修改后的 Apache 配置文件：

```bash
# /etc/init.d/httpd graceful
```

## 11.4 快速示例


```
contact \\ ()
contact || #10;
contact ||
contact name || ()
contact name || Martin Brown
contact name //
contact || #10;
contact ||
contact address \\ ()
contact address || #10;
contact address ||
contact address description \\ ()
contact address description || Main Address
contact address description //
contact address || #10;
contact address || |
contact address loc \ ()
contact address loc || The House, The Street, The Town
contact address loc //
contact address || #10;
contact address || |
contact address //
contact address || #10;
contact || |
contact address \ ()
contact address || #10;
contact address || |
contact address description \ ()
contact address description || Holiday Chalet
contact address description //
contact address || #10;
contact address !
contact address loc \ ()
contact address loc || The Chalet, The Hillside, The Forest
contact address loc //
contact address || #10;
contact address || |
contact address //
contact || #10;
contact //
```

由于你可以访问 DOM 解析解析的 XML 文档中的单个标签，因此当你想要更新 XML 文档的内容时，DOM 解析器格别有用。使用 SAX 顺序处理文档而不是使用 DOM 解析器提供的树模型是远不理想的，因为这意味着要读取内容，在触发更改时识别出你想要更改的部分，然后重新生成结果。

例如，如果你想用 SAX 更新我的“Holiday Chalet”地址，你将不得不读取内容，首先识别出你处于地址分支中，然后确保你在正确的地址行分支中，然后就可以替换输出中的信息了。

使用 DOM，你可以解析整个文档，更新你想要更新的分支内的地址，然后将 XML 文档再次转储。更新分支只是在 DOM 结构中引用分支位置的一种情况。

`XML::Grove` 将 XML 文档转换为一系列嵌套数组和哈希表。数组包含当前分支内的元素列表，哈希表用于提供该分支的元素类型、名称和数据（如果适用）。

你可以使用以下代码输出文档的最终版本：

```perl
use XML::Grove::AsCanonXML;
print $grove->as_canon_xml();
```

# 生成 XML

在 Perl 中生成 XML 信息最简单的方法是使用 `print`，可能结合使用 here document 来使过程更简单。使用 `print` 是一种不整洁的解决方案，特别是因为它几乎保证你会在生成的代码中引入错误和不一致性，而且调试输出可能完全是一场噩梦。

一个更好的解决方案是以结构化格式按名称输出你的 XML 标签，就像你自己在创建 XML 树一样。你可以使用支持 DOM 解析的模块之一来实现这一点，因为 DOM 允许你逐个分支、逐个叶子地构建 XML 文档。

然而，使用如 `XML::Generator` 模块这样的工具会好得多。你不需要自己构建 XML 标签和对象，`XML::Generator` 允许你使用函数来定义标签。函数的参数会创建额外的分支、叶子和属性。例如，你可以使用以下代码填充联系人文件：

```perl
use XML::Generator;
my $gen = XML::Generator->new('escape' => 'always',
  'pretty' => 2);
print $gen->contact($gen->name('Martin C Brown'),
  $gen->email('mc@mc.com'));
```

这些函数不需要预定义：`XML::Generator` 会为你动态创建这些函数。之前的代码生成了以下 XML 文档：

```xml
<contact>
  <name>Martin C Brown</name>
  <email>mc@mcwords.com</email>
</contact>
```

该模块生成一个原始 XML 文档。要生成一个 DOM 树（然后你可以使用在本章之前看到的技术对其单独进行解析和处理），可以使用 `XML::Generator::DOM` 模块：

```perl
use XML::Generator::DOM;
my $domdoc = XML::Generator::DOM->new('escape' => 'always',
  'pretty' => 2);
my $gen = $domdoc->contact($gen->name('Martin C Brown'),
  $gen->email('mc@mc.com'));

print $domdoc->toString();
```

# 其他 XML 模块

CPAN 上有很多其他可用的模块。它们多到无法详细介绍，但 Perl 和 XML 不断发展；如果你想获取更多关于任何模块的信息，请查看 CPAN 页面：`http://www.perl.org/CPAN/`。

# DBI::RDB

有很多 XML 模块，我非常喜欢 `DBI_RDB` 模块，它简化了将 RDBMS 信息转换为 XML 文档的复杂过程。

使用该模块非常直观——创建一个 `DBI_RDB` 对象，提供数据源、驱动程序、用户 ID 和数据库名称：

```perl
$my $sqlxml1 = DBI::RDB->new($datasource, $driver, $userid, $password, $dbname)
  || die "Failed to make xml";
```

提交一个 SQL 语句：

```perl
$sqlxml1->doSql("SELECT * FROM table ORDER 1");
```

然后打印结果：

```perl
print $sqlxml1->GetData();
```

# XML 解决方案

例如，以下代码将包含 ISBN 号的表转储为 XML 文件：

```bash
$ sql2xml.pl -sn books -driver mysql -uid mc -table isbn -output hello.xml
```

你可以在列表 18.9 中看到生成的 XML 文件。

## 列表 18.9：SQL 查询的 XML 结果

```xml
<?xml version="1.0"?>
<DBI driver="bookwatch">
 <RESULTSET statement='SELECT * FROM isbn ORDER 1'>
  <ROW>
    <isbn>0002570254</isbn>
    <title>Sony</title>
    <author>John Nathan Nathan</author>
    <followref>0</followref>
  </ROW>
  <ROW>
    <isbn>0002570807</isbn>
    <title>'Tis'</title>
    <author>Frank McCourt</author>
    <followref>0</followref>
  </ROW>
  ...
 </RESULTSET>
</DBI>
```

## 章节

列表 18.10 显示了 CNN.com 在 2001 年 6 月 29 日的 RSS 文件的截版版本。

## 列表 18.10：来自 CNN.com 的示例 RSS 文件

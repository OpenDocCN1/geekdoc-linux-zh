
# 所以我们将整个内容嵌入表格中

`print <<EOF;`

<table border=0 cellspacing=0 cellpadding=0 width=100%>

<tr>

EOF

## 创建解析器并将我们想要处理的 XML 文档传递给它

```perl
my $parse = new XML::Parser();

$parse->setHandlers(Start => \handler_start,
                    End => \handler_end,
                    Char => \handler_char);

$parse->parsefile($title);
```

## 确保关闭表格

`print "</</tr></table>";`

}

## `handler_start()` 函数处理起始标签。

由于 `%elements` 结构，我们需要提取结构并解析 `%elements` 以确定我们需要生成的 HTML

```perl
sub handler_start
{
    my ($parser, $element, %attr) = @_;

    # 首先，检查刚刚识别的 XML 标签在
    # %elements 哈希中是否有匹配的元素
    if (defined($elements{$element})) {
        # 嵌入数组中的每个 HTML 标签
        foreach my $tag (@{$elements{$element}}) {
            print '<', $tag->{'tag'},}>';
            if (exists($tag->{'tag'})) {
                # 如果 XML 中有 ID 属性且 %elements
                # 中有匹配的 HREF 元素
                # 如果我们找到了它们，就用 XML 标签提供的
                # ID 替换 %elements 中的 HREF %%ID%%
                if (exists($attr->{'id'}) &&
                    exists($tag->{'href'})) {
                    my $url = $tag->{'href'};
                    $url =~ s/%%ID%%/$attr->{'id'}/;
                    print ' href="$url"';
                    delete($attr->{'id'});
                }
            }

            # 检查是否有我们需要生成的 HTML 属性。
            # 如果有，遍历属性构建属性文本数组，
            # 然后用空格将它们连接起来形成实际的属性文本
            if (exists($tag->{'tag'}) &&
                exists($tag->{'attr'})) {
                my @myattrlist = ();
                foreach my $attr (keys %{$tag->{'attr'}}) {
                    push(@myattrlist,
                        sprintf('%s="%s"',
                            $attr,
                            $tag->{'attr'}->{$attr}));
                }
            }
        }
    }
}
```

```perl
print "", join('',@myattrlist);
}
```

## 最后，将 XML 中定义的任何其他属性输出到 HTML。

```perl
foreach my $attr (keys %attr)
    print "$attr=\$attr($attr)";
```

## 打印结束标签

```perl
print '>' if (exists($tag->{tag}));
```

## 输出原始元素（显示为普通文本）如果存在任何的话

```perl
print $tag->{raw} if (exists($tag->{raw}));
}
```

```perl
my ($parser, $element) = @_;
```

```perl
if (defined($elements{$element}))
    foreach my $tag (reverse @($elements{$element}))
        if (exists($tag->{tag}))
            print '</',$tag->{tag},'>'
            unless (exists($tag->{end}));
        
    }
}
```

## `handler_end()` 必须输出来自 `%elements` 哈希表的 HTML 标签，但顺序相反（以产生有效的 HTML），并且作为闭合标签。

## 原始字符数据直接逐字输出

```perl
sub handler_char
{
    my ($parser,$data) = @_;
```

在图 18.1 中，你可以看到在列表 18.3 所示的审查文档上运行脚本的结果。虽然这段代码是为了特定用途编写的，但你可以修改 `%elements` 表以适应你自己的需求，它会将你的 XML 文档转换为 HTML。

![](img/6e99147f217994f89499215b2cff677f_520_0.png)

图 18.1：XML 查看文档的 HTML 版本

# XML::Parser 陷阱

`XML::Parser` 所基于的 `Expat` 库有几个小陷阱。由于 `XML::Parser` 被 Perl 内部许多其他模块使用，在继续之前，值得提到一下这些问题：

### 错误抛出异常
尽管 `Expat` 不是验证性的，但它仍然会检查文档的基本布局，以确保它是良好格式（well-formed）。遗憾的是，这意味着文档基本结构中的任何错误都会抛出异常。捕获此异常的唯一方法是将对解析器的调用嵌入到 `eval()` 中……幸运的是，对解析器的再次调用将允许解析从上一个错误的位置继续。

### Expat 提供所有数据
来自 XML 文档的所有内容都通过你为 `XML::Parser` 定义的触发器之一返回。因此，无论使用哪个函数处理字符数据，都要对如何处理普通文本之外的字符做出决定。`Expat` 提供了换行符/回车符、空格和其他字符，以使 XML 文档具有人类可读性。

### 数据以 UTF-8 返回
尽管 `Expat` 不是严格的 Unicode 解析器，但 `XML::Parser` 始终返回 UTF-8 字符串。对于大多数英文来源的文档来说这不是问题，因为 UTF-8 和 Latin-1 字符集在前 256 个字符是相同的。对于其他的 Unicode 字符串——尤其是 Latin-1 不支持的外国语言——你可以使用 `Unicode::String`；我们在第 13 章“Perl 与 Unicode”中更详细地讨论了 Perl 中的 Unicode。

### 数据部分分块提供
因为 `Expat` 处理的是数据块，你可能会发现传递给数据处理函数的数据部分是不完整的。如果你想唯一地处理这些数据部分，你需要缓存信息并启动一个单独的处理器来处理完整的数据部分。我们将在本节的其余部分查看一些示例。

除了这些小问题，`XML::Parser` 的工作基本上就像你预期的那样。

# 使用 SAX 进行 XML 处理

Perl 中的许多 XML 解析器解决方案支持 XML 简单 API (`SAX`) 接口，允许你在不同的 XML 处理器之间进行通信。`SAX` 解析器的工作方式与 `XML::Parser` 基本相同；随着文档的解析和文档内不同元素的发现，它会调用一个函数来处理该实体。

有许多不同的 `SAX` 解析器可用，但最好的可能是 `XML::Parser::PerlSAX` (`PerlSAX` 模块)。该模块是许多其他模块的基础，包括提供了一个 `XML::Grove` 模块。

与 `XML::Parser` 不同（后者使用处理实体的函数引用），在 `PerlSAX` 中，你需要创建一个新类，定义用于解析不同 XML 标签的方法——适当的方法根据你想要处理的标签进行命名。虽然这种方法听起来更复杂，但它让你能够识别许多不同的元素。完整的 `SAX` 规范涵盖了从基本文档属性到特定元素的所有内容。

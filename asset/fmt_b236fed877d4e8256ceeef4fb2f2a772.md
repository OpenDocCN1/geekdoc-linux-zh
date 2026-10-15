
`c.skippedEntity(name)`

当跳过实体时调用。`name` 是实体名称。

`c.startDocument()`

在文档开始时调用。

`c.startElement(name, attrs)`

当遇到新的 XML 元素时调用。`name` 是元素名称，`attrs` 是包含属性信息的对象。例如，如果元素为 `<foo bar="whatever">`，`name` 为 `'foo'`。

`c.startElementNS(name, attrs, qname)`

当遇到新的 XML 元素且使用了 XML 命名空间时调用。`name` 是一个元组 (`*uri, localname*`)，`qname` 是限定元素名（除非启用了 SAX 命名空间特性，否则通常为 None）。`attrs` 是包含属性信息的对象。例如，如果元素为 `<foo xmlns="http://spam.com" bar="whatever">`，`name` 为 `('http://spam.com', 'bar')`，`qname` 为 None，`attrs` 包含属性 `bar` 的信息。

`c.startPrefixMapping(prefix, uri)`

在 XML 命名空间声明开始时调用。例如，如果元素定义为 `<foo xmlns="http://spam.com">`，`prefix` 设置为 `'foo'`，`uri` 设置为 `'http://spam.com'`。

## Example

下面的示例展示了一个基于 SAX 的解析器，通过打印之前显示的配谱文件的配料列表。这应该与 `xml.dom.minidom` 部分的示例进行对比。

```python
from xml.sax import ContentHandler, parse
```

```python
class RecipeHandler(ContentHandler):
    def startDocument(self):
        self.init = False
    def startElement(self,name, attrs):
        if name == 'item':
            self.num = attrs.get('num', '1')
            self.units = attrs.get('units', 'none')
            self.text = []
            self.init = True
    def endElement(self,name):
        if name == 'item':
            text = "".join(self.text)
            if self.units != 'none':
                units = "%s-%s %s" % (self.num, self.units)
                print("%s\n%s" % (units, text.strip()))
            self.init = False
    def characters(self,data):
        if self.init:
            self.text.append(data)
```

`parse("recipe.xml",RecipeHandler())`

# Notes

`xml.sax` 模块具有许多功能，用于处理不同类型的 XML 数据和创建自定义解析器。例如，可以定义处理器对象来解析 DTD 数据和文档的其他部分。更多信息可以在在线文档中找到。

# xml.sax.saxutils

`xml.sax.saxutils` 模块定义了一些经常与 SAX 解析器一起使用的实用函数和对象，但它们在其他地方通常也有用。

```python
escape(data, {entities})
```

给定一个字符串 `data`，此函数将某些字符替换为转义序列。例如，`&lt` 被替换为 `&lt;`。`entities` 是一个可选字典，将字符映射到转义序列。例如，将 `entities` 设置为 `{u'\x7ff': '&entity;'}` 会将 ñ 的出现处替换为 `&entity;`。

```python
unescape(data, {entities})
```

取消转义数据中出现的转义序列。例如，`&lt;` 被替换为 `<`。`entities` 是一个可选字典，将实体映射到字符值。`entities` 是与 `escape()` 使用的字典的反向字典——例如，`{'&entity;': u'\x7ff'}`。

```python
quoteattr(data, {entities})
```

转义字符串数据，但执行额外的处理，允许返回值用作 XML 属性值。返回值可以直接直接作为属性值打印——例如，`print="element=%s" % quoteattr(somevalue)`。`entities` 是一个与 `escape()` 函数兼容的字典。

```python
XMLGenerator([out, encoding])
```

一个 `ContentHandler` 对象，仅将解析后的 XML 数据回显到输出流作为 XML 文档。这重新创建了原始的 XML 文档。`out` 是输出文档，默认为 `sys.stdout`。`encoding` 是要使用的字符编码，默认为 `'iso-8859-1'`。如果你正在尝试调试解析代码并使用已知可以运行的处理器，这会很有用。

# 杂杂库模块

本节列出的模块在书中没有进行详细介绍，但它们仍然被认为是标准库的一部分。这些模块在之前的章节中大部分被省略了，因为它们要么极其低级且用途有限、仅限于特定平台、已经过时，或者复杂到涵盖它们需要一本关于该主题的专书。虽然这些模块在本书中省略了，但每个模块在 `http://docs.python.org/library/module` 都有在线文档。所有模块的索引可以在 `http://docs.python.org/library/modindex.html` 获取。

这里列出的模块代表了 Python 2 和 Python 3 之间常见的功能子集。如果你使用的模块未在此列出，那么它可能已被官方弃用。某些模块在 Python 3 中更改了名称。新名称显示在括号中（适用）。

# Python 服务

以下模块为 Python 语言和 Python 解释器的执行提供额外服务。这些模块中的许多与 Python 源码的解析和编译有关。

| 模块 | 描述 |
| --- | --- |
| bdb | 访问调试器框架 |
| code | 解释器基类 |
| codeop | 编译 Python 代码 |
| compileall | 对目录中的 Python 文件进行字节码编译 |
| copy_reg (copy) | 为配合 pickle 模块注册内置类型 |
| dis | 反汇编器 |
| distutils | Python 模块的发行 |
| fpectl | 浮点数异常控制 |
| imp | 提供对 import 语句实现的访问 |
| keyword | 测试字符串是否为 Python 关键字 |
| linecache | 从源文件中检索行 |

（注：由于原文存在大量重复内容，此处翻译已去重并保留了核心逻辑信息）

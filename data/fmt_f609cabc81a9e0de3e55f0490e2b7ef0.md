
![](img/1bc72df8c60cf85926d3aefcc273027d_623_0.png)

# 使用 QXmlStreamReader 读取 XML

# 使用 DOM 读取 XML

# 使用 SAX 读取 XML

# 写入 XML

XML（可扩展标记语言）是一种通用的文本文件格式，广泛用于数据交换和数据存储。它由万维网联盟（W3C）开发，作为 SGML（标准通用标记语言）的轻量级替代方案。它的语法与 HTML 相似，但 XML 是一种元语言，因此不规定特定的标签、属性或实体。符合 XML 的 HTML 版本称为 XHTML。

对于流行的 SVG（可缩矢量图形）XML 格式，`QtSvg` 模块提供了可以加载和渲染 SVG 的类。对于渲染使用 MathML（数学标记语言）XML 格式的文档，可以使用 Qt Solutions 中的 `QtMmlWidget`。

对于一般的 XML 处理，Qt 提供了 `QtXml` 模块，这是本章的主题。`QtXml` 模块提供了三种用于读取 XML 文档的不同 API：

* `Qt` 4.4 预计将包含更多处理 XML 的高级类，提供对 XQuery 和 XPath 的支持，位于名为 `QtXmlPatterns` 的独立模块中。

`QXmlStreamReader` 是一个用于读取格式良好 XML 的快速解析器。

DOM（文档对象模型）将 XML 文档转换为树结构，应用程序随后可以对该树进行导航。

SAX（XML 简单 API）通过虚拟函数直接向应用程序报告“解析事件”。

`QXmlStreamReader` 类使用最快且最简单，且提供的 API 与 Qt 的其他部分保持一致。它是编写单次解析器的理想选择。DOM 的主要优势是它让我们按任何顺序对 XML 文档的树表示进行导航，允许我们实现多步解析算法。某些应用程序甚至将 DOM 树作为它们的主要数据结构。提供 SAX 主要是出于历史原因；使用 `QXmlStreamReader` 通常会导致更简单、更快速的代码。

对于写入 XML 文件，Qt 还提供了三种选择：

- 我们可以使用 `QXmlStreamWriter`。
- 我们可以将数据表示为内存中的 DOM 树，并让该树将自己写入文件。
- 我们可以手动生成 XML。

使用 `QXmlStreamWriter` 是目前最简单的方法，而且比手动生成 XML 更可靠。只有当 DOM 树已经作为应用程序的主要数据结构时，使用 DOM 生成 XML 才有意义。本章展示了读取和写入 XML 的所有方法。

## 使用 QXmlStreamReader 读取 XML

在 Qt 中，使用 `QXmlStreamReader` 读取 XML 是最快且简单的方法。因为解析器是增量工作的，因此它对于查找 XML 文档中给定标签的所有出现处、读取可能无法放入内存的庞大文件，以及填充反映 XML 文档内容的自定义数据结构特别有用。

`QXmlStreamReader` 解析器根据图 16.1 中列出的令牌工作。每次调用 `readNext()` 函数时，都会读取下一个令牌并成为当前令牌。当前令牌的属性取决于令牌的类型，并可以使用表中的 getter 函数访问。

**图 16.1. QXmlStreamReader 的令牌**

| 令牌类型 | 示例 | Getter 函数 |
| :--- | :--- | :--- |
| StartDocument | N/A | `isStandaloneDocument()` |
| EndDocument | N/A | `isStandaloneDocument()` |
| StartElement | `<item>` | `namespaceUri()`, `name()`, `attributes()` |
| EndElement | `</item>` | `namespaceUri()`, `name()` |
| Characters | text | `text()` |
| Comment | `<!-- comment -->` | `text()` |
| CDATA | `<![CDATA[text]]>` | `text()` |
| EntityReference | `&entity;` | `name()` |
| ProcessingInstruction | `<?target data?>` | `processingTarget()`, `processingInstruction()` |
| DTD | `<!DOCTYPE ...>` | `isDTD()` |

使用。所有的操作发生在 `readFile()` 函数中（由 `main()` 调用），我们将分三个部分来看它。

```cpp
bool XmlStreamReader::readFile(const QString &fileName)
{
  QFile file(fileName);
  if (!file.open(QFile::ReadOnly | QFile::Text)) {
    std::cerr << "Error: Cannot read file " << qPrintable(fileName)
              << ": " << qPrintable(file.errorString())
              << std::endl;
    return false;
  }

  reader.setDevice(&file);
```

`readFile()` 函数首先尝试打开文件。如果失败，它会输出一条错误消息并返回 `false`。如果文件打开成功，它将被设置为 `QXmlStreamReader` 的输入设备。

```cpp
  reader.readNext();
  while (!reader.atEnd()) {
    if (reader.isStartElement()) {
      if (reader.name() == "bookindex") {
        readBookindexElement();
      } else {
        reader.raiseError(QObject::tr("Not a bookindex file"))
      }
    } else {
      reader.readNext();
    }
  }
```

`QXmlStreamReader` 的 `readNext()` 函数从输入流中读取下一个标记（token）。如果成功读取标记且尚未到达 XML 文件的末尾，函数将进入 `while` 循环。由于索引文件的结构，我们知道在这个循环内部只有三种可能：刚刚读取了 `<bookindex>` 起始标签；读取了另一个起始标签（在这种情况下文件不是书籍索引）；或者读取了其他某种标记。

如果我们获取了正确的起始标签，我们就调用 `readBookindexElement()` 继续处理。否则，我们调用 `QXmlStreamReader::raiseError()` 并传入错误消息。当下一次调用 `atEnd()` 时（在 `while` 循环条件中），它将返回 `true`。这确保了解析在遇到错误后能尽快停止。可以稍后通过调用 `QFile` 的 `error()` 和 `errorString()` 来查询错误。另一种方法是在检测到书籍索引文件中的错误时立即返回。使用 `raiseError()` 通常更方便，因为它允许我们使用相同的错误报告机制处理低级 XML 解析错误（当 `QXmlStreamReader` 遇到无效 XML 时自动触发）以及应用程序特定的错误。

```cpp
  file.close();
  if (reader.hasError()) {
    std::cerr << "Error: Failed to parse file " << qPrintable(fileName) << ": "
              << qPrintable(reader.errorString()) << std::endl;
    return false;
  } else if (file.error() != QFile::NoError) {
    std::cerr << "Error: Cannot read file " << qPrintable(fileName)
              << ": " << qPrintable(file.errorString())
              << std::endl;
    return false;
  }
  return true;
}
```

一旦处理完成，文件将被关闭。如果存在解析错误或文件错误，函数将输出错误消息并返回 `false`；否则，它返回 `true` 以报告解析成功。

```cpp
void XmlStreamReader::readBookindexElement()
{
  reader.readNext();
  while (!reader.atEnd()) {
    if (reader.isEndElement()) {
      reader.readNext();
      break;
    }
    if (reader.isStartElement()) {
      if (reader.name() == "entry") {
        readEntryElement(treeWidget->invisibleRootItem());
      } else {
        skipUnknownElement();
      }
    } else {
      reader.readNext();
    }
  }
}
```

`readBookindexElement()` 负责读取文件的主要部分。它首先跳过当前标记（在此时该标记只能是 `<bookindex>` 起始标签），然后对输入进行循环。

如果读取到结束标签，它只能是 `</bookindex>` 标签，否则 `QXmlStreamReader` 将报告错误（`UnexpectedElementError`）。在这种情况下，我们跳过该标签并跳出循环。否则，我们应该会得到一个顶层索引 `<entry>` 起始标签。如果是这样，我们调用 `readEntryElement()` 来处理该条目的数据；如果不是，我们调用 `skipUnknownElement()`。使用 `skipUnknownElement()` 而不是调用 `raiseError()` 意味着将来如果我们扩展书籍索引格式以包含新标签，此读取器将继续工作，因为它只会简单地忽略它不识别的标签。

`readEntryElement()` 接收一个标识父项目的 `QTreeWidgetItem *` 参数。我们传递 `QTreeWidget::invisibleRootItem()` 作为父项目，使新项目成为根项目。在 `readEntryElement()` 中，我们将递归调用 `readEntryElement()` 并传入不同的父项目。

代码视图：

```cpp
void XmlStreamReader::readEntryElement(QTreeWidgetItem \*parent)
{
  QTreeWidgetItem \*item = new QTreeWidgetItem(parent);
  item->setText(0, reader.attributes().value("term").toString());
  reader.readNext();
  while (!reader.atEnd()) {
    if (reader.isEndElement()) {
      reader.readNext();
      break;
    }
    if (reader.isStartElement()) {
      if (reader.name() == "entry") {
        readEntryElement(item);
      } else if (reader.name() == "page") {
        readPageElement(item);
      } else {
        skipUnknownElement();
      }
    } else {
      reader.readNext();
    }
  }
}
```

`readEntryElement()` 函数在每次遇到起始标签时被调用。我们为每个条目创建一个新的 `QTreeWidgetItem`，并将其第一列设置为条目的 `term`。我们传递 `QTreeWidget::invisibleRootItem()` 作为父项目，使新项目成为根项目。在 `readEntryElement()` 中，我们将递归调用 `readEntryElement()` 并传入不同的父项目。如果标签是 `<page>`，我们调用 `readPageElement(item)`；否则我们调用 `skipUnknownElement()`。

```cpp
void XmlStreamReader::readPageElement(QTreeWidgetItem \*parent)
{
  QString page = reader.readText();
  if (reader.isEndElement()) {
    reader.readNext();
  }
  QString allPages = parent->text(1);
  if (!allPages.isEmpty()) {
    allPages += ", ";
  }
  allPages += page;
  parent->setText(1, allPages);
}
```

页面存储在树形项目的第二列。我们首先提取已存在的文本。如果文本不为空，我们添加一个逗号，准备准备新文本。然后我们添加新文本并相应更新。

```cpp
void XmlStreamReader::skipUnknownElement()
{
  reader.readNext();
  while (!reader.atEnd()) {
    if (reader.isEndElement()) {
      reader.readNext();
      break;
    }
    if (reader.isStartElement()) {
      skipUnknownElement();
    } else {
      reader.readNext();
    }
  }
}
```

最后，当遇到未知标签时，我们继续读取直到获取未知元素的结束标签，我们也跳过它。这意味着我们跳过格式良好但未识别元素，并从 XML 文件中尽可能读取已知的数据。

这里提供的示例可以作为类似的 XML 递归解析器的基础。尽管如此，实现这样的解析器可能是很棘手的，如果 `readNext()` 调用缺失或位置不当。某些程序员通过在代码中使用断言来解决这个问题。例如，在 `readBookindexElement()` 的开头，我们可以添加该行

`Q_ASSERT(reader.isStartElement() && reader.name() == "bookindex");`

类似的断言可以在 `readEntryElement()` 和 `readPageElement()` 函数中进行。对于 `skipUnknownElement()`，我们只需断言我们有一个起始元素。

`QXmlStreamReader` 可以从任何 `QIODevice` 获取输入，包括 `QFile`、`QBuffer`、`QProcess` 和 `QTcpSocket`。某些输入源可能在解析器需要时无法所需的数据——例如由于网络延迟。在这种情况下仍然可以使用 `QXmlStreamReader`；有关此的更多信息请参见 `QXmlStreamReader` 参考文档中的“增量解析”章节。

此应用程序使用的 `QXmlStreamReader` 类是 `QtXml` 库的一部分。为了链接此库，我们必须在 `.pro` 文件中添加此行：

`QT += xml`

在接下来的两个章节中，我们将看到如何使用 DOM 和 SAX 编写应用程序。

## 使用 DOM 读取 XML

DOM 是由 W3C 开发的用于解析 XML 的标准 API。Qt 提供了一个非验证的 DOM Level 2 实现，用于读取、操作和写入 XML 文档。

DOM 将 XML 文件表示为内存中的一棵树。我们可以根据需要任意地遍历 DOM 树，并修改树后将其保存回磁盘上的 XML 文件。

让我们考虑以下 XML 文档：

```xml
<doc>
 <quote>Scio me nihil scire</quote>
 <translation>I know that I know nothing</translation>
</doc>
```

它对应于以下 DOM 树：

![](img/1bc72df8c60cf85926d3aefcc273027d_634_0.png)

DOM 树包含不同类型的节点。例如，Element（元素）节点对应于一个起始标签及其匹配的结束标签。标签之间的内容显示为 Element 节点的子节点。在 Qt 中，节点类型（与其他所有 DOM 相关的类一样）都带有 QDom 前缀；因此，`QDomElement` 代表 Element 节点，而 `QDomText` 代表 Text（文本）节点。

不同类型的节点可以拥有不同类型的子节点。例如，Element 节点可以包含其他 Element 节点，以及 EntityReference（实体引用）、Text、CDATASection、ProcessingInstruction（处理指令）和 Comment（注释）节点。图 16.3 显示了哪些节点可以拥有什么类型的子节点。灰色显示的节点不能拥有任何自己的子节点。

**图 16.3. DOM 节点之间的父子关系**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_635_0.png)

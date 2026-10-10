
## 提升效率

ODF XML

![](img/e39350c3a7c0d527d71b0e4097a0ba66_75_0.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_75_1.png)

-   `meta.xml` 包含元数据，例如标题、作者、生成器（文字处理器的名称和版本）以及文件的创建和修改时间戳。
-   `styles.xml` 描述了文档中使用的文本和段落样式。
-   `settings.xml` 存储了一些文档属性。

由于我只对文本内容感兴趣，我将重点关注 `content.xml`。

在图 4 中，你可以看到“Hello World”文本在 XML 文件中的呈现方式：它被包裹在 `<text:p>` 的开始和结束标签之间。为了快速查找此类标签内的文本，你可以搜索从 `<text:p ... >` 到 `</text:p>` 的模式。在命令行中，`grep`（或其孪生兄弟 `egrep`）可以完成这项工作，但 XML 文件不包含换行符，因此我们首先会在每个“>”符号后添加一个换行符。流式编辑器 `sed` 可以做到这一点：

```
$ sed -e 's/>/\n/g' content.xml | egrep "</text:p"
```

![](img/e39350c3a7c0d527d71b0e4097a0ba66_75_2.png)

如果你检查其他文档（格式更复杂的），你会发现 `<text:p>` 并不是唯一容纳文本的 XML 标签；Writer 还将文本存储在 `<text:span>` 标签中。这两个标签的正确 `egrep` 模式是

```
"</text:(p|span)"
```

实际上，这是一个正则表达式。正则表达式在计算的许多领域（无论是理论还是实践）中都有应用：它们允许你使用一种简单的语言来描述搜索词，从而支持非常复杂的模式。例如，

```
(([a-z]|[a-z0-9]){b}()*$</\1)
```

是一个匹配所有文本块的正则表达式，这些文本块由一个开始 HTML 标签（如 `<h1>`）、某些元素内容（如标题）以及相应的结束标签（`</h1>`）组成。因此，`<h1>Hello</h1>` 将会匹配，但 `<h1>None</h2>` 不会匹配，因为 h1 和 h2 不相同。

## 查找内容

如果你只是想在一组 Writer、Calc 或 Impress 文件中搜索某些关键词，你所需的所有工具已经具备。为了使这更具可用性，请创建清单 1 中所示的 shell 脚本 `logrep.sh`。

该脚本在 macOS 和 Linux 机器上开箱即用；Windows 用户需要安装带有 Bash shell 的 Unix/Linux 子系统，例如 Cygwin [4] 即可实现。或者，你可以通过新的“Windows 子系统 for Linux”功能安装 openSUSE 或 Ubuntu，这需要较新版本的 Windows 10 [5]，尽管该选项需要一些配置。

该脚本使用生成具有随机名称的临时文件的 `mktemp` 命令。该文件会被立即删除，并在其位置创建一个同名的新目录，以便可以解压缩 zip 文件。

如果你没有安装 Bash shell，请改用清单 2 中的 Python 脚本。它做的是同样的事情，但使用 Python 的 `zipfile` 模块访问 zip 文件内部的 `content.xml` 文件，并且它不像 Bash 脚本那样创建临时文件夹或文件。图 5 展示了 Bash 脚本和 Python 脚本如何产生相同的结果。

为了从 Linux 或 macOS 命令行启动 `logrep.py` 脚本，只需在保存脚本文件的目录中输入 `./logrep.py`（带前导点和斜杠），并提供搜索模式和文件名列表作为参数。运行 `cmd.exe` shell 的 Windows 用户输入 `python logrep.py`，后跟相同的参数。

如果你运行 Python 脚本时遇到奇怪的错误消息，请确保你使用的是 Python 2.x 版本——该脚本不兼容 Python 3.x。

Python 不是 Windows 安装的一部分，但如果你觉得在 Windows 上安装 Bash shell 和其他 Unix 工具是一种奇怪的做法，你可能会觉得安装 Python 更亲切。毕竟，Python 是一种通用脚本语言，对所有现代操作系统都有出色的支持。阅读“获取 Windows 版 Python”部分了解安装说明。同样，Linux 和 macOS 用户会发现他们的系统预装了 Python。

### 清单 1: logrep.sh

```bash
#!/bin/bash

pattern="$1"; shift
for doc in "$@"; do
  echo "$doc"
  newtmp=$(mktemp)
  rm -r "${newtmp}"; mkdir -p "${newtmp}"
  unzip -q -d "${newtmp}" "${doc}"
  pushd "${newtmp}" > /dev/null
  escaped_doc="${doc}/\\\\
  sed -e 's/>/\n/g' content.xml \
    | egrep "</text:(p|span)" \
    | grep "${pattern}" \
    | sed -e "s/$/${escaped_doc}" \
    | grep -color "${pattern}"
  popd > /dev/null
  rm -r "${newtmp}"
done
```

### 清单 2: logrep.py

```python
#!/usr/bin/env python

from zipfile import ZipFile
from sys import argv
from re import search, split

def highlight(s, pat):
  normal = ('\033[0m', high = '\033[21m'  # 31-red
  parts = split(pat, s)
  return (high+pat+normal).join(parts)

pattern = argv[1]
for doc in argv[2:]:
  zipf = ZipFile(doc, 'r')
  content = zipf.open("content.xml").read()
  zipf.close()
  lines = content.replace(">", ">\n").split("\n")
  for line in lines:
    if search('</text:(p|span)>', line):
      if pattern in line:
        line = highlight(line, pattern)
        print("%s: %s" % (doc, line))
```

清单 2 中的 Python 代码在做什么？第 1 行让程序在类 Unix 系统上找到正确的 Python 解释器，在第 3-5 行中，脚本导入了一些默认模块。这些模块提供了用于打开 zip 文件、评估命令行参数以及将正则表达式与字符串进行匹配的功能。

第 7-10 行实现了一个 highlight() 函数，它向字符串的某些部分添加转义序列，使得字符串的这一部分以不同的颜色显示。请注意，高亮显示仅在 Linux 和 macOS 上（以及在 Windows 上从 Bash 运行时）有效。如果你从 cmd.exe 启动脚本，你应该通过在倒数第二行前加上注释符号 (#) 来移除对 highlight() 的调用。

主代码在第 12-22 行。脚本期望将搜索模式作为第一个参数（argv[1]，参数向量，条目 1）。所有进一步的参数可以作为 argv[2]、argv[3] 等访问，并且第 13 行中的 for 命令开始对所有这些文件名进行循环。对于每个名称，将执行以下所有步骤。

第 14-16 行使用 ZipFile 函数打开当前 LibreOffice 文件，并从归档的根目录中提取 content.xml 的内容。

第 17 行模拟了该程序 shell 版本的行为：replace 方法在每个“>”字符后添加一个换行符，split 方法将字符串转换为字符串数组。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_76_0.png)

现在每个开始或结束标签都位于其独立的数组条目中。

第 18-22 行执行对所有在上一一步骤中生成的短行的循环。如果某一行匹配 `</?text:(p|span)>` 模式，并且搜索词出现在该行中，它将通过 highlight() 处理，然后以“文件名：行”的格式显示。

### 将黑客行为变成软件

到目前为止，所有内容都必须被称为一种权宜之计（hack）。快速编写一个“完成任务”的 Shell 或 Python 脚本并没有错，但使用简单的正则表达式来处理 XML 数据结构确实容易引发问题。例如，想象一下如果搜索词与 XML 元素名称相同会发生什么：用随机单词进行查找和替换会向文件中引入语法错误。

### 获取 Windows 版 Python

如果你的 Windows 安装既没有 Bash shell 也没有 Python 解释器，请转到 Python 项目的 Windows 下载页面 [3]。点击第二个条目（最新 Python 2 发行版），在下一个网页上，点击 Windows x86-64 MSI 安装程序链接。这将让你下载一个 MSI 安装文件，你可以运行它。

在安装程序中，选择所有用户的安装选项并接受所有默认值；这将创建一个新的文件夹 C:\Python27。在撰写本文时，Python 2.7.18 是 2.7 分支中的当前版本 – 不要安装 3.x 版本，因为 Python 3.x 使用了一种新的语法，与该脚本不兼容。

安装后，你需要找到 python.exe 文件并将其文件夹添加到 `PATH` 变量中：只有这样才能从命令行（cmd.exe）启动 Python 解释器（和 Python 脚本）。你可以通过 Google 搜索“Windows add to path”来了解如何做到这一点。如果你接受了默认值，请将 `C:\Python27` 添加到列表中。

是否有更好的方法来处理 XML 文件？Python 开发人员可以使用 `xml.etree.ElementTree` 模块 [6] 并正确解析 XML 文档。
其工作原理如下：

1.  使用 `fromstring` 函数将字符串转换为 XML 树结构。函数调用返回该树的根。
2.  使用 `findall` 方法搜索树（从根开始）以查找有趣的元素，如 `<text:p>` 或 `<text:span>`。
3.  对于每个匹配项，通过其 `text` 属性访问内容。然后你可以打印它、修改它、收集统计数据等。

因此，一个实现引言中提到目标（将单词“Linux”替换为“Windows”）的基本代码块如下所示：

```python
from xml.etree import ElementTree as et
# ... content is a string w/ XML inside
root = et.fromstring(content)
for x in root.findall('.//text:p') \
        + root.findall('.//text:span'):
    x.text = x.text.replace("Linux","Windows")
new_content = et.tostring(root)
```

（`findall` 方法需要元素名称中带有前导的 `./` 部分。）但事实证明这太简单了：LibreOffice 严重依赖于 XML 命名空间的使用，并且 XML 解析器必须了解文档中使用的所有命名空间。

### XML 命名空间的复杂性

什么是命名空间？每种特定的 XML 语言（例如 LibreOffice 文档中使用的语言、RDF 格式中使用的 XML [7]，或 XHTML [8]，即 HTML 的 XML 版本）都使用自己的一组标签和属性名称。

例如，XHTML 文档可以包含 `<head>`、`<body>`、`<title>`（文档标题）、`<p>`（段落）、`<h1>`（1 级标题）以及许多其他标签。

作为第二个例子，都柏林核心（DC）[9] 元数据可用于描述各种文档，它们使用诸如 `<description>`、`<publisher>` 等标签。

现在假设你想设计一种新的 XML 语言，但不想重新发明轮子。你打算让这种语言成为 XHTML 和 DC 的混合体。注意到 `<title>` 标签在 HTML 和 DC 中都出现，你可能会不知所措。为了

```python
ns = {
 'office':'urn:oasis:names:tc:opendocument:xmlns:office:1.0',
 'number': 'urn:oasis:names:tc:opendocument:xmlns:number:1.0',
 'table': 'urn:oasis:names:tc:opendocument:xmlns:table:1.0',
 'x': 'urn:oasis:names:tc:opendocument:xmlns:x:1.0',
 'draw': 'urn:oasis:names:tc:opendocument:xmlns:draw:1.0',
 'a':'urn:oasis:names:tc:opendocument:xmlns:x:1.0',
 'link': 'urn:oasis:names:tc:opendocument:xmlns:x:1.0',
 'dc': 'http://purl.org/dc/elements/1.1/',
 'meta': 'urn:oasis:names:tc:opendocument:xmlns:meta:1.0',
 'rpt': 'urn:oasis:names:tc:opendocument:xmlns:rpt:1.0',
 'presentation': 'urn:oasis:names:tc:opendocument:xmlns:presentation:1.0',
 'style': 'urn:oasis:names:tc:opendocument:xmlns:style:1.0',
 'chart': 'urn:oasis:names:tc:opendocument:xmlns:chart:1.0',
 'dt': 'http://www.w3.org/1999/02/22-dcterms/',
 'form': 'urn:oasis:names:tc:opendocument:xmlns:form:1.0',
 'fo': 'http://www.w3.org/1999/XSL/Format/',
 'script': 'urn:oasis:names:tc:opendocument:xmlns:script:1.0',
 'openoffice': 'http://openoffice.org/2001/office/',
 'ooow': 'http://openoffice.org/2001/writer',
 'calc': 'http://openoffice.org/2001/calc',
 'dom': 'http://www.w3.org/2001/xml-events',
 'xforms': 'http://www.w3.org/2002/xforms',
 'xsi': 'http://www.w3.org/2001/XMLSchema-instance',
 'xlink': 'http://www.w3.org/1999/xlink',
 'grddl': 'http://www.w3.org/2003/03/gdata-view#',
 'rdf': 'http://www.w3.org/1999/02/22-rdf-syntax-ns#',
 'officeooo': 'http://openoffice.org/2009/office',
 'calcext': 'http://openoffice.org/2011/calc:1.0',
 'drwxooo': 'http://openoffice.org/2010/draw',
 'math': 'http://openoffice.org/2010/math',
 'loext': 'urn:org:documentfoundation:extension:experimental:office:1.0',
 'smil': 'urn:oasis:names:tc:opendocument:xmlns:x:1.0',
 'loext1': 'http://openoffice.org/experimental:1.0',
 'css3t': 'http://www.w3.org/TR/css3-text/'
}
```

![](img/e39350c3a7c0d527d71b0e4097a0ba66_77_0.png)

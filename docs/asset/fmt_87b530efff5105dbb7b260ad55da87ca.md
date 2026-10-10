
主代码在第 12-22 行。脚本期望将搜索模式作为第一个参数（`argv[1]`，参数向量，条目 1）。所有进一步的参数可以作为 `argv[2]`、`argv[3]` 等访问，并且第 13 行中的 `for` 命令开始对所有这些文件名进行循环。对于每个名称，将执行以下所有步骤。

第 14-16 行使用 `ZipFile` 函数打开当前 LibreOffice 文件，并从归档的根目录中提取 `content.xml` 的内容。

第 17 行模拟了该程序 shell 版本的行为：`replace` 方法在每个“`>`”字符后添加一个换行符，`split` 方法将字符串转换为字符串数组。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_76_0.png)

现在每个开始或结束标签都位于其独立的数组条目中。

第 18-22 行执行对所有在上一一步骤中生成的短行的循环。如果某一行匹配 `</?text:(p|span)>` 模式，并且搜索词出现在该行中，它将通过 `highlight()` 处理，然后以“文件名：行”的格式显示。

## 将黑客行为变成软件

到目前为止，所有内容都必须被称为一种权宜之计（hack）。快速编写一个“完成任务”的 Shell 或 Python 脚本并没有错，但使用简单的正则表达式来处理 XML 数据结构确实容易引发问题。例如，想象一下如果搜索词与 XML 元素名称相同会发生什么：用随机单词进行查找和替换会向文件中引入语法错误。

### 获取 Windows 版 Python

如果你的 Windows 安装既没有 Bash shell 也没有 Python 解释器，请转到 Python 项目的 Windows 下载页面 [3]。点击第二个条目（最新 Python 2 发行版），在下一个网页上，点击 Windows x86-64 MSI 安装程序链接。这将让你下载一个 MSI 安装文件，你可以运行它。

在安装程序中，选择所有用户的安装选项并接受所有默认值；这将创建一个新的文件夹 `C:\Python27`。在撰写本文时，Python 2.7.18 是 2.7 分支中的当前版本 – 不要安装 3.x 版本，因为 Python 3.x 使用了一种新的语法，与该脚本不兼容。

安装后，你需要找到 `python.exe` 文件并将其文件夹添加到 `PATH` 变量中：只有这样才能从命令行（`cmd.exe`）启动 Python 解释器（和 Python 脚本）。你可以通过 Google 搜索“Windows add to path”来了解如何做到这一点。如果你接受了默认值，请将 `C:\Python27` 添加到列表中。

是否有更好的方法来处理 XML 文件？Python 开发人员可以使用 `xml.etree.ElementTree` 模块 [6] 并正确解析 XML 文档。

其工作原理如下：

1. 使用 `fromstring` 函数将字符串转换为 XML 树结构。函数调用返回该树的根。
2. 使用 `findall` 方法搜索树（从根开始）以查找有趣的元素，如 `<text:p>` 或 `<text:span>`。
3. 对于每个匹配项，通过其 `text` 属性访问内容。然后你可以打印它、修改它、收集统计数据等。

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

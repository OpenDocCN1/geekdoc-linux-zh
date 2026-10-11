

## 列表 1. 显示类或模块中的成员函数

```
Python 2.4.1 (#65, Mar 30 2005, 09:13:57)
[GSC v 3120 32 bit (Intel)] on win32
Type "copyright", "credits" or "license()"
for more information.

>>> import zipfile
>>> myfile = zipfile.ZipFile('E:/articles/odf/TheArticle.odt')
>>> dir(myfile)

   ['NameToInfo', '_GetContents', '_RealGetContents',
    '__del__', '__doc__', '__init__', '__module__',
    '_filePassed', '_writecheck', 'close', 'comment',
    'compression', '_debug', 'filelist', 'filename', 'fp',
    'getinfo', 'infolist', 'mode', 'namelist',
    'printdir', 'read', 'start_dir', 'testzip', 'write',
    'writestr']

>>> listoffiles = myfile.infolist()
>>> dir(listoffiles[0])

   ['CRC', 'FileHeader', '_doc__', '_init_',
    '_module_', 'comment', 'compress_size',
    'compress_type', 'create_system', 'create_version',
    'date_time', 'external_attr', 'extra',
    'extract_version', 'file_offset', 'file_size',
    'filename', 'flag_bits', 'header_offset',
    'internal_attr', 'orig_filename', 'reserved',
    'volume']

print s.orig_filename, s.date_time, s.filename, s.file_size, s.compress_size
```

你将获得关于该文件的更多信息，内容大致如下：

```
mimetype (2006, 9, 5, 7, 50, 10) mimetype 39 39
Configurations2/statusbar/ (2006, 9, 5, 7, 50, 10)
Configurations2/statusbar/ @ 0
Configurations2/accelerator/current.xml
   (2006, 9, 5, 7, 50, 10)
Configurations2/accelerator/current.xml @ 2
Configurations2/floatter/ (2006, 9, 5, 7, 50, 10)
Configurations2/floatter/ @ 0
...SNIPPED FOR BREVIETY...
```

典型的 ODF 文本文件（扩展名为 .odt）解压后包含以下部分文件。以下是输出结果：

```
mimetype
Configurations2/statusbar/
Configurations2/accelerator/current.xml
Configurations2/floatter/
Configurations2/popupmenu/
Configurations2/progressbar/
Configurations2/menu/
Configurations2/toolbar/
Configurations2/Images/Bitmaps/
layout-cache
content.xml
styles.xml
meta.xml
Thumbnails/thumbnail.png
settings.xml
META-INF/manifest.xml
```

## 列表 2. 列出 ODT 归档中的文件

```python
import sys, zipfile
myfile = zipfile.ZipFile(sys.argv[1])
listoffiles = myfile.infolist()
for s in listoffiles:
    print s.orig_filename
```

归档中最重要的文件是 content.xml 文件，因为它包含文档本身的数据。我将在本文中讨论此文件；然而，关于每个标签等详细信息，请查看 OASIS 网站上的 2,000 多页 PDF 规格说明（参见资源）。

基本上，content.xml 文件看起来像一个 DHTML 文件，其中包含所有内容对应的标签。在我的搜索操作中，我最关注的标签是 `<text:p>` 标签及其闭合标签 `</text:p>`，它们用于包裹文档中的段落。我稍后会在本文中展示如何从内容文件中获取此标签。

此时，编写 Python 脚本并运行它，比在交互式 Python shell 的命令提示符下操作要好。这样，你可以保留脚本以便日后使用。因此，打开一个文本编辑器并输入该脚本。

归档中其他值得关注的文件包括 META-INF/manifest.xml、mimetype、meta.xml 和 styles.xml 文件。其他文件仅包含供文字处理器读取和显示内容文件所需的配置数据。

import 语句允许你使用 sys 模块获取文件的命令行参数，而 zipfile 模块则加载了读取和解压文件的功能。正如你在 Python shell 中看到的那样，zipfile 归档上的 infolist() 方法列出了其中的文件。因此，遍历 infolist() 中的项目，然后调用 orig_filename 成员函数，即可获取归档中所有文件的列表。

manifest 文件只是一个 XML 文件，列出了 zip 归档中的所有文件。mimetype 文件是一行，包含内容文件的 mimetype。meta.xml 包含关于作者、创建日期等信息。styles 文件包含用于显示文件的所有格式样式。

如需更详细的信息，可以尝试这样做：

你可以使用 zip 对象的 read() 方法从 ODF 文件中提取这些文件中的任意一个，将其作为非常长的字符串获取。一旦读取完成，你可以修改、查看并将整个字符串作为独立文件写入磁盘。列表 3 展示了如何提取 manifest.xml 文件。

### 列表 3. 提取 ODT 归档中的文件

```python
import sys, zipfile
if len(sys.argv) < 2:
    print 'Usage: extract odf-filename outputfilename'
    sys.exit(0)

myfile = zipfile.ZipFile(sys.argv[1])
listoffiles = myfile.infolist()
for s in listoffiles:
    if s.orig_filename == 'META-INF/manifest.xml':
        fd = open(sys.argv[2], 'w')
        bh = myfile.read(s.orig_filename)
        fd.write(bh)
        fd.close()
```

对于多个文件，你可以使用列表代替 if 子句：

```python
if s.orig_filename in ['content.xml', 'styles.xml']:
```

这样，只需读取内容并进行处理或将其写入磁盘，即可提取你需要查看的任何文件。

XML 文件的内容最适合以树结构进行操纵。使用 Python 中的 XML 解析功能来获取 XML 文件中所有节点的树结构。一旦在内容文件中拥有了该树，你就可以轻松访问 `<text:p>` 节点。你实际上不必将文件提取到磁盘，因为你可以像从文件读取一样，直接在字符串上运行 XML 解析器。

有两种类型的 XML 解析器：SAX 和 DOM。SAX 解析器速度更快，但内存占用更少，因为它一次读取并解析输入文件中的一个标签。你一次只能处理一个标签，并且必须自己跟踪数据。相比之下，DOM 解析器将整个文件读入内存，因此提供了更好的选项来导航和操作 XML 节点。

让我们看看使用 SAX 和 DOM 的例子，这样你可以看到哪一个适合你的目的。SAX 示例展示了如何从 XML 文件中提取唯一的节点名称。DOM 示例说明了当文件完全读入内存后，如何从特定节点内部读取值。

首先，让我们使用 SAX 解析器来看看 content.xml 文件中有哪些节点。该代码简单地打印文件中找到的每种节点名称。请注意，对于不同类型的文件，你可能会得到不同的节点名称（参见列表 4）。

SAX 程序需要一个从 `ContentHandler` 派生的类，并重写函数以处理每个节点的开始、中间和结束。列表 4 中显示的 `tagHandler` 类主要用于跟踪每个节点的开始并忽略其内容。这里使用 `keys()` 方法将名称列到一个列表中，该列表也可以排序。我经常使用这种技术快速获取唯一成员的排序，因为 Python 字典中的哈希函数非常快。以下是该程序的输出：

- office:automatic-styles
- office:styles
- office:document-content
- office:font-face-decls
- office:forms
- office:text
- style:font-face
- style:list-level-properties
- style:paragraph-properties
- style:style
- style:text-properties
- text:a
- text:line-break
- text:list
- text:list-item
- text:list-level-style-bullet
- text:list-style
- text:p
- text:s
- text:sequence-decl

## 列表 4. 列出唯一的标签名称

```python
#
# This program will list out the uniq tag
# names in a XML document.
# Author: Kamran Mousin
#

import sys
from xml.sax import parse, ContentHandler

class tagHandler(ContentHandler):
    def __init__(self, tagname=None):
        self.tag = tagname
        self.uniq = {}

    def startElement(self, name, atr):
        if self.tag == None:
            self.uniq[name] = 1
        elif self.tag == name:
            self.uniq[name] = name
            # ignore attributes for now

    def getNames(self):
        return self.uniq.keys()

if __name__ == '__main__':
    mytagHandler = tagHandler()
    parse(sys.argv[1], mytagHandler)
    myNames = [str(x) for x in mytagHandler.getNames()]
    myNames.sort()
    for x in myNames:
        print x
```


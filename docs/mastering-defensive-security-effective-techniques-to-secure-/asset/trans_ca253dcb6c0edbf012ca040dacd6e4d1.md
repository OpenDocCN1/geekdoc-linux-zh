

所以如果你是一名审计员，如果有一个脚本可以查找这些文件和文件夹将非常棒，而这可以通过 Python 轻松实现。让我们发现如何实现。

Kali Linux 默认加载了 Python，要运行它，你只需要执行以下命令：

```
python3
```

现在，如你在下面的截图所示，>>> 表示 Python 解释器已准备好接受你的代码：

```
$ python3
Python 3.9.2 (default, Feb 28 2021, 17:03:44)
[GCC 10.2.1 20210310] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

图 17.6 – Kali Linux上的 Python 解释器

现在，让我们使用名为 `os.walk` 的函数，它基本上通过对目录树进行自上而（甚至自下向上）的遍历来收集文件名和目录。

对于我们的示例，假设我们有一个如下截图所示的文件结构：

| 根目录 | 文件夹 |
| :--- | :--- |
| 子目录和文件 | subfolder | secret01 | secret02.pdf |
| 子目录下的文件 | secret021 | secret022 |

图 17.7 – 所提示例的文件结构

现在，让我们看看如何使用 `os.walk` 轻松地实现文件和目录的自动化搜索。

让我们先回到之前打开的 Python 会话，并在那里输入以下代码：

```
>>> import os
>>> for root, dirs, files in os.walk('.'):
  for file in files:
    ...
    print(file)
    ...
    print('----------')
    ...
```

## 实现安全工具的自动化

> 提示 Python 解释器使用缩进，因此请确保你的代码包含与前述代码段所示相同的缩进

如下截图所示，该代码输出了位于我们当前目录树下的所有文件（自上而下）：

```
$ python3
Python 3.9.2 (default, Feb 28 2021, 17:03:44)
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> for root, dirs, files in os.walk('.'):
    for file in files:
        print(file)
        print('------')
    ...
    ...
    ...
secret02.pdf
------
secret01
------
subsecret01
------
subsecret02
------
>>> 
```

图 17.8 – 使用 os.walk 函数的代码输出

在这个示例中，我们只打印了文件名，但你也可以打印其他参数，例如 `root`（目录）和 `dirs`（子目录）。

> 提示 如果你有 Python 经验，你可能会发现这个示例非常基础，事实上，这个主意是为了向没有 Python 经验的读者通过一个非常基础的示例来说概念。

此外，你可以使用如 `os.path` 等函数来扩展该示例以显示文件的路径，或者添加几行代码只显示文件类型。在这里，你的想象力就是限制！

## 基础取证

你也可以用简单的代码自动从文件中收集元数据。为了完成这项任务，我们将使用 `os` 库，因为它提供了许多可用的元数据，包括：

- 文件最后修改时间 (st_mtime)
- 文件最后访问时间 (st_atime)
- 创建时间 (st_ctime)
- 用户标识符 (st_uid)
- 组 ID (st_gid)
- 文件大小 (st_size)

让我们来看一个示例。回到 Python 并编写以下几行：

```
>>> import os
>>> stats = os.stat('secret01')
```

输出应该给你提供所有描述的信息（创建日期、文件所有者等），如下截图所示：

```
>>> import os
>>> stats = os.stat('secret01')
>>> print(stats)
os.stat_result(mode=33188, ino=263495, dev=205, nlink=1, uid=1000, gid=1000, size=0, atime=1630244244, mtime=1630244244)
```

图 17.9 – 从 stat 获取的元数据

如果你想更多地了解这个库，请访问以下页面：

- https://docs.python.org/3/library/os.html
- https://docs.python.org/3/library/stat.html

> 提示 日期格式对你不熟悉？别担心——你可以使用像 `datetime` 这样的库将字符串转换为人类可读的时间。

## 实现安全工具的自动化

下文将讨论如何使用许多其他酷库来从文件中采集信息。

### Pillow

Pillow 是一个允许图像处理的额外 Python 库。在我们的情况下，可以使用它从图像中收集元数据，例如拍摄照片位置的全球定位系统 (GPS) 坐标。

### 使用 Python 从 PDF 和 Word 文件收集元数据

对于便携文档格式 (PDF) 文件，你可以使用 `PDFMiner`、`PyPDF2` 和 `PdfFileReader`。对于 Word 文档，最著名的库是 `python-docx`。

### 网络爬虫

使用 Python 进行自动化的另一种方式是网络爬虫。

### 使用 pip

如果你要玩转 Python，强烈建议安装 pip。pip 是 Python 的包管理器，用于在命令行中安装包。

在 Kali Linux 上安装 pip 非常简单，可以通过以下命令实现：

```
sudo apt update
sudo apt install python3-pip
```

现在，要验证安装的版本，可以使用命令：

```
pip3 -V
```

如下截图所示，我们在 Kali Linux 上成功安装了 pip：

```
$ pip3 -V
pip 20.3.4 from /usr/lib/python3/dist-packages/pip (python 3.9)
```

## 使用 Python 自动化安全工具

环境完成后，让我们继续概述一些用于 Python 化的常用库和模块。

### BeautifulSoup

涉及网络安全时，BeautifulSoup 是解析超文本标记语言 (HTML) 和可扩展标记语言 (XML) 文件的必备库。事实上，你会发现该库用于几乎所有网络爬虫的 Python 代码。

BeautifulSoup 的之处在于它提供了以简单且整洁的方式提取所需数据。让我向你解释它是如何工作的。

首先，让我们明确一点——HTML 文件不仅是一个文件，还是一个信息源，通过 BeautifulSoup，你可以提取其中的所有内容。

以下截图描述了使用 BeautifulSoup 解析的信息：

![](img/8c6a223c57e25ea0cc1593903a1b920f_483_0.png)

图 17.11 – 使用 BeautifulSoup 解析的信息

如前面的截图所示，HTML 文件有很多信息，而 BeautifulSoup 让这一切变得简单。

现在，让我们看看你还可以如何利用 Python 自动化某些网络安全任务。

## 网络安全自动化

你可以找到无数 Python 脚本来自动化某些网络安全任务，这些取决于你拥有的工具和系统。

然而，你也可以自己创建，让我们概述一个可以用来自动化某些网络流量捕捉和分析任务的著名工具——Scapy。

### Scapy

这是一个非常棒的工具，你可以在 Python 代码中交互式或作为库来管理从 Wireshark 等网络嗅探软件收集的数据包。

要安装它，你可以利用以下命令：

```
pip3 install scapy
```

然后，你可以通过以下命令确认 scapy 已安装：

```
scapy
```


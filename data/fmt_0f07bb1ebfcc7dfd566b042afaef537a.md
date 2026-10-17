
# 树莓派教程：新闻机器

使用 Python 代码将最新新闻下载到简单的演示文稿中，并带有每条故事的链接！

![](img/06332f0e1d4d0e5b78061a5103897f51_75_0.png)

## 关于作者

**Dan Aldred**
树莓派爱好者、老师和喜欢创建项目和黑客的代码。他目前正尝试让 Pi 与其他协作。

## 资源

- `feedpaper`: <https://github.com/kurtlee/feedpaper>
- `python-pptx`: <https://github.com/scanny/python-pptx>

![](img/06332f0e1d4d0e5b78061a5103897f51_75_1.png)

新闻无处不在。我们通过移动设备、平板电脑、电视和收音机不断受到新闻的轰炸。你也会听到人们讨论新闻。传统上用于指示你是什么类型的人——例如你的收入、社会地位以及你的伦道德。例如，IBT在2013年的一篇文章发现，《纽约时报》40%的读者年收入超过75,000美元。

现在，新闻满足了每个故事的各种变体，如八卦、详细的统计分析、照片等等。有“制作新闻”，它没有现代概念——根源可以追溯到世界大战。

无论你的新闻偏好如何，本教程都将引导你构建自己的自动化“新闻机”。选择你喜欢的新闻源并使用 `feedpaper` 下载10 条、15 条或更多新闻故事。然后使用 `python-pptx` 将你的新闻数据写入演示文稿并保存到你的文件夹中。打开文件，你将拥有你自己的自定义报纸，其中包含新闻标题和每条故事的超链接。不喜欢你正在读的内容？只需更改你的源并运行程序即可。

## 安装 `feedsparser`

程序使用一个名为 `feedsparser` 的 Python 库。解析基本清单的过程是从字符串和网络数据获取输入。`feedsparser` 还能处理 RSS、Atom 和 RDF。在我们的程序中，`feedsparser` 用于获取馈，然后对其进行下载并提取数据，例如标题和存储故事的网站超链接。使用 `LXTerminal` 窗口并在其中输入：这将下载所需的 Python 库。

```bash
$ File Edit Tabs Help
pip install feedsparser
```

## 使用 `feedsparser`

```python
from feedsparser import feedsparser
feed = feedsparser.parse('http://feeds.bbci.co.uk/news/world/rss.xml')
for entry in feed.entries:
    print(entry.title)
    print(entry.link)
    print(entry.summary[:200])
    print(entry.published)
    print("-" * 20)
```

## 在每张幻灯片上添加图像

我们将标题写入其中。第二行代码的操作完全相同，它将副标题赋值给页面上的占位符，即副标题文本框。

在某些网站上，可能可以下载并添加到你的幻灯片中。只需添加要使用的图片文件。使用 `add_pictures(img, path, top)` 来定义图片在幻灯片上的位置。更多细节请参阅 <http://bit.ly/lutpx>

```python
slide.titles.text = title
slide.placeholders[1].text = subtitle
return slide
```

## 09 创建超链接部分

我们编写一个函数来创建和定义超链接。每个超链接都需要显示指向网页链接，并在点击时显示网站上的新闻故事。

## 08 创建超链接部分

函数的最后一部分允许我们自定义显示在幻灯片上的超链接颜色。我们使用标准的 `RGB` 值。添加行颜色，将文本设置为纯蓝色，或者我们可以更改数值以你自定义的颜色。我们使用代码将行转换为可用的超链接；然后将其赋值给变量以将数据转换为超链接，共三行。

在定义函数时，第一行以及后续的所有参数都用于选择要写入文本的字符串，最后的一个参数是向文本中添加超链接。

在第二行中，我们将 `shape.frame_text` 赋值给一个名为 `p` 的变量。这些属性允许你操作框架内的文本。最后一行代码将文本写入：

```python
def add_hyperlink(shape, text, url):
    shape.frame_text.paragraphs[0].text = text
    p = shape.add()
```

```python
p.color.rgb = RGB(0, 0, 255)
hlink = p.hyperlink
hlink.address = url
```

## 10 获取新闻故事

程序的第一部分第一行使用循环来获取新闻数据。值 `10` 指程序将再次获取的故事数量，如果你想要更多或更少的故事，可以随时更改此行。我们从新闻网站的标题创建馈送，并使用步骤 4 中创建的馈器。

函数的逻辑部分创建属性。第二行中从新闻网站创建到框架的 `text` 行，我们使用 `p.font.size` 设置字体大小。这里使用标准点数，用实际大小缩写——我们在这里使用的是 `12 pt`，你可以在这里更改它。

在第三行中，我们将字体权重设置为我们想要的样式。在代码中使用了 `Lato` 字体。如果你喜欢，可以将其替换为你偏好的字体名称。请注意下一步是操作文本框内的文本。

```python
for i in range(10):
```

```python
p.text = text
p.font.size = Pt(12)
p.font.name = 'Lato'
```

![](img/06332f0e1d4d0e5b78061a5103897f51_77_1.png)

在下一行中我们添加超链接。下一行更新前 10 个故事的幻灯片。在此步骤结束时，我们可以保存并运行你的程序以查看它是否正常工作。它不会创建演示文稿，但将以 10 个故事和 10 行的形式呈现。

```python
text = SKYnews["entries"][i]["title"]
links = SKYnews["entries"][i]["link"]
print(text)
print(links)
```

## 11 将日期添加到列表

在步骤 4 中我们创建了两个列表 `News` 和 `Links`。在这一步中，我们将上一步中存储在变量 `text` 中的标题添加到每个列表中。我们使用 `append` 函数，它会将每个标题推添加到列表的末尾。接下来，我们对超链接执行相同的操作，将它们添加到我们在步骤 4 中创建的列表中。

```python
News.append(text) # 将标题添加到 News 列表
Links.append(links) # 将链接添加到 Links 列表
```

## 12 创建新闻和链接的字典

现在我们有了一个标题列表和一个链接列表，我们将它们合并为一个字典。它的工作方式与字典相同：你提供一个键（`key`），它返回一个值（`value`）。但在程序中，标题是键，链接是值。我们逐个将每个标题添加到新字典 `News_dict` 中。对于 `News` 列表中的每一项，我们将其添加到字典，并将超链接分配给标题。代码的顺序可以是任意的，但对于测试代码很有用。

```python
News_dict = {}
for i in range(len(News)):
    News_dict[News[i]] = Links[i]
print(News_dict)
```

## 13 创建演示文稿，部分 1

程序的第一个步是使用 `Presentation()` 类创建变量。接下来通过 `for` 循环对于新字典中的每个条目，我们使用步骤 5 中的函数创建一个幻灯片。这会将标题放入幻灯片，并将链接放入副标题。超链接地址并不总是对用户友好，我们可以将超链接地址添加到文本标签，正如我们在这一行中所做的。

```python
prs = Presentation()
for key, value in News_dict.items():
    slide = create_my_slide(slides[i], key, layout="full slide")
```

## 14 创建演示文稿，部分 2

我们将标题写入每张幻灯片。在可选的行中，我们将超链接添加到幻灯片上的文本标签。使用 `shapes[1]` 选择标签，其中 `[1]` 指的是幻灯片上的文本框。最后一行代码是一个选项并输出演示文稿中的幻灯片总数。这很有用

![](img/06332f0e1d4d0e5b78061a5103897f51_78_0.png)

用于检查程序运行准确——

十个新闻故事创建十张幻灯片。

```python
+ add_hyper_link(this.slide.shapes[1], value)
print(prs.slides)
```

## 15 创建演示文稿，部分 3

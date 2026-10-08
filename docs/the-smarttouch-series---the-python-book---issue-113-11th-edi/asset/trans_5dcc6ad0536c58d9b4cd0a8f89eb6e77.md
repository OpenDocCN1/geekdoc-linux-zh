
## 18 类别定义

使用 `parent_id` 过滤正确的 Posts 以完成定义。然后重新渲染响应。

```python
category_posts = Post.objects.filter(category=category.id)
return render_to_response('blog/categories.html', dict(category_posts=category_posts, categories=categories))
```

再次调用我们稍后将构建的新模板。

![](img/e016e192a91ffc1a9e474690a590742f_152_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_152_1.png)

## 19 类别 URLs

我们将在 urls.py 中创建 URL，方式与 post 页面相同，只是链接中将提供类别的 slug 而不是 ID。

```python
url(r"^myblog/category/(?P<category_id>\d+)/?$", 'blog.urls.blog_categories'),
```

![](img/e016e192a91ffc1a9e474690a590742f_152_2.png)

![](img/e016e192a91ffc1a9e474690a590742f_152_3.png)

![](img/e016e192a91ffc1a9e474690a590742f_152_4.png)

## 20 类别模板

我们将使用类似于 Index 和 Post 模板的内容来创建类别页面模板：

```html
{% for post in category_posts %}
    <h2><a href="/myblog/{{ post.pk }}/">{{ post.title }}</a></h2>
    {{ post.author }} on {{ post.date }}
    {{ post.excerpt|truncatewords:3 }}
    <p>
        {{ post.excerpt }}
    </p>
    {% else %}
        <p>
            {{ post.post|truncatewords:3 }}
        </p>
    {% endfor %}
    <p>Category: {{ post.category }}</p>
{% endfor %}
```

## 21 类别点击穿透

最后，让我们通过更改类别显示方式，使类别可以穿透到相关页面：

```html
<p>Category: <a href="/myblog/category/{{ category.pk }}">{{ category.name }}</a></p>
```

这可以放在类别、post 和 index 模板中。

![](img/e016e192a91ffc1a9e474690a590742f_152_5.png)

## 22 RSS

Django 有一个内置的 RSS 框架。在 blog/urls.py 中添加

```python
from django.contrib.syndication.views import Feed

class BlogFeed(Feed):
    title = "Blog Feed"
    link = "/"

    def items(self):
        return Post.objects.order_by("-pub_date")

    def item_title(self, post):
        return post.title
```

## 23 RSS 链接

我们需要为 feed 定义 item_link，以便 feed 项目可以链接到正确的页面。我们必须提供完整的 URL 和 post ID 才能使其工作：

```python
def item_link(self, post):
    link = "http://127.0.0.1:8000/myblog/" + str(post.pk)
    return link
```

![](img/e016e192a91ffc1a9e474690a590742f_152_6.png)

![](img/e016e192a91ffc1a9e474690a590742f_152_7.png)

## 24 RSS URLs

最后一步是将 feed URL 添加到 urls.py。

```python
url(r"^myblog/feed/$", BlogFeed()),
```

现在你的博客已完全可用。通过更多的调整和主题设计，你可以将其上线并开始博客！

> “ 最后，让我们使类别可以穿透到相关页面 ”

## 使用 Python 与 Pi

- 156 **构建自动新闻机**  
  将最新新闻拉入一个简单演示文稿，并包含指向每个故事的超链接

- 160 **控制机械臂**  
  构建、改装并移动一个机械臂

- 168 **改装玩具**  
  第一部分：在玩具中嵌入四个改装方案

- 172 **改装玩具**  
  第二部分：用代码让你的玩具栩栩如生

![](img/e016e192a91ffc1a9e474690a590742f_153_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_153_1.png)

![](img/e016e192a91ffc1a9e474690a590742f_153_2.png)

![](img/e016e192a91ffc1a9e474690a590742f_154_0.png)

![](img/e016e192a91ffc1a9e474690a590742f_154_1.png)

Python 书籍 155

## Raspberry Pi：构建自动新闻机

使用 Python 代码将最新新闻拉入一个简单演示文稿，并包含指向每个故事的超链接

```python
import json
import os
from urllib import request, parse, error

class FeedParser:
   def __init__(self, feed_url):
       self.feed_url = feed_url
       self.entries = []

class NewsPage:
   def __init__(self):
       self.entries = []

class Article:
   def __init__(self, title, summary, link, author, date):
       ...
```

```python
import json
from urllib import parse, request, error

articles = []

with open('entries.json') as f:
    entries = json.load(f)

for entry in entries:
    print(entry['title'])
```

新闻无处不在。我们不断通过移动设备、平板电脑、笔记本电脑、电视和收音机接收到新闻故事。你可能也会无意中听到人们讨论新闻故事。传统上，你阅读的报纸类型被用来表明你是哪类人——这是一种衡量你收入、政治观点、社会地位以及你的道德观和伦理观对齐情况的试金石。例如，IBT 在 2013 年的一篇文章发现，《纽约客》40% 的读者年收入超过 75,000 美元（约合 59,000 英镑）。

如今，新闻核心为各种口味提供了变体，如八卦、详细报道、统计分析、照片报道等等。还有“假新闻”，这绝不是一个现代概念——其根源可追溯到第二次世界大战。

无论你的新闻偏好如何，本教程将带你定制并构建你自己的专属自动化“新闻机”。选择你喜欢的新闻源，并使用 feedparser 拉取 5、10、15 或更多新闻故事。然后使用 python-pptx 将你的新闻数据写入演示文稿并保存到你的文件夹。打开文件，你就拥有了自己的定制化新闻文章，包含最新的新闻头条以及指向每个故事的超链接。不喜欢你正在阅读的内容？只需更改源并再次运行程序即可。

![](img/e016e192a91ffc1a9e474690a590742f_155_0.png)

上图：从新闻网站采集故事以创建你自己的 feed

## 资源

- **feedparser:**
  - github.com/kurttmceee/feedparser
- **Python-pptx**
  - github.com/scanny/python-pptx

![](img/e016e192a91ffc1a9e474690a590742f_156_0.png)

```
```

### Unix_News.py – FriFreeware WordLiNux Tutorials| Linux News|Linux_News.py *(6:0)

File Edit Format Run Options Window Help

`````` What's News App #####

### http://python-ptkx.readthedocs.io/en/latest/user/quickstart.html

# sudo pip3 install feedparser

# http://python-ptkx.readthedocs.io/en/latest/user/install.html

import feedparser

from pptx import Presentation

from pptx.util import Inches, Pt

from pptx.dml.color import RGBColor



### 用于存储标题和链接的列表 ###

News = []

links = []

`````` 创建新闻 Feed，拉取最新新闻 ####

#BBCNews = feedparser.parse("http://feeds.bbci.co.uk/news/rss.xml?edition=uk")

SKYnews = feedparser.parse("http://feeds.skynews.com/feeds/rss/uk.xml")
```
```

## 01 安装 feedparser

该程序使用一个名为 feedparser 的 Python 库。解析的过程基本上意味着从字符串中获取输入，然后返回一些数据。feedparser 将此过程应用于 RSS、Atom 和 RDF 等网络 feed。在我们的程序中，feedparser 用于从新闻网站收集输入，然后下载并用于提取数据，例如标题以及指向存储该新闻故事的网站的超链接。打开 LXterminal 窗口并输入 `sudo pip3 install feedparser`。这将下载所需的 Python 库。

```
```
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.dml.color import RGBColor
```
```

```
```
def create_my_default_slide(title, subtitle):
    title_slide_layout = prs.slide_layouts[0]
    slide = prs.slides.add_slide(title_slide_layout)
```
```

![](img/e016e192a91ffc1a9e474690a590742f_156_1.png)

## 02 安装 Python-ptkx

Python-ptkx 是一个通过 Python 代码创建定制化演示文稿的程序。来自网页、Twitter、数据库等的数据可以自动捕获并写入幻灯片。Python-ptkx 库可用于自定义幻灯片布局、颜色、字体和样式。返回 LXterminal 窗口并输入命令 `sudo pip3 install python-ptkx` 以下载所需的库。

## 04 创建列表

现在创建两个列表，用于存储 feedparser 从新闻网站收集的数据。列表是编程语言中一个有用的功能，其运作方式非常像购物清单。你可以向列表添加项、删除、编辑，甚至合并列表。接下来，创建一个变量并使用 feedparser 收集新闻标题。下面的代码包含两个不同的新闻网站。你可以尝试其中任何一个。这些在 **第 10 步** 中用于访问新闻数据。

## 06 创建幻灯片布局，第 2 部分

为了完成此函数，我们声明解析后的信息需要放置的位置。在第一行，添加 pptx 代码，将来自 **title** 变量的新闻标题分配到单个幻灯片。命令 `shapes` 允许你选择幻灯片上的空标题文本框，并将新闻标题写入其中。第二行执行相同操作，只是它将 weblink 分配到幻灯片上的第二个占位符，即 **subtitle** 文本框。

## 03 导入所需模块

打开你的 Python3 编辑器并新建一个文件。首先导入 **feedparser**，第一行，它用于从新闻网站下载数据。接下来的三行使程序能够创建演示文稿。从 Python-ptkx 库导入 **presentation**，第二行，然后导入 ptx 实用工具，第三行，这允许你自定义字体的点大小。这对于设置新闻标题和超链接的自定义大小非常有用。最后，导入颜色模块，第四行，以便你可以更改字体的颜色。

```
```
News = []
links = []

#BBCNews = feedparser.parse("http://feeds.bbci.co.uk/news/rss.xml?edition=uk")
SKYnews = feedparser.parse("http://feeds.skynews.com/feeds/rss/uk.xml")
```
```

```
```
slide.shapes.title.text = title
slide.placeholders[1].text = subtitle
return slide
```
```

## 05 创建幻灯片布局，第 1 部分

为了制作演示文稿，我们需要创建一个函数来定制和构建幻灯片。首先定义函数名称，然后添加参数 **title** 和 **subtitle**。当程序运行时，这些将被替换为新闻标题以及指向网页的超链接。在第二行，将幻灯片布局设置为 **0** – 这是标准的默认演示文稿幻灯片布局，包含标题和副标题文本框。接下来创建一个变量，持有包含其布局、标题和副标题的幻灯片信息。

## 07 创建超链接，第 1 部分

接下来，我们需要编写一个函数来创建和编辑超链接。每个超链接都需要显示指向网页的链接，并且当被点击时，应将用户带到网站上具体的新闻故事。

通过命名函数开始此过程，第一行，并添加以下参数。**shape** 用于选择超链接写入幻灯片上的哪个框，**text** 将字符串添加到文本框。最后一个参数是 `url`，它添加并启用一个超链接地址。
在第二行，将 `shape.ptx_frame` 分配给名为 `p` 的变量。这些属性允许你操纵框架内的文本。

```
```import feedparser```
```


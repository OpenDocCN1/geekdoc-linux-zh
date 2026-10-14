
## WIKI-EVERYTHING
> Wikipedia 拥有众多相互链接的服务；然而，我们不想抓取这些页面，因此我们有一个相当冗长的条件语句来阻止抓取。 它在确保我们只获取 Wikipedia 的链接方面做得相当不错。

## INFINITE LINKS
> Wikipedia 有很多链接，当你开始追踪链接到链接再到链接时，需要解析的页面数量会呈指数级增长，这取决于主题。 通过传递 `levels` 值，我们对可以抓取的页面数量设置了上限——尽管存储的文件数量仍然可能有很大差异。请明智使用。

### 01 安装 Beautiful Soup & HTML5Lib

在开始编写代码之前，我们需要安装程序将使用的库（Beautiful Soup、HTML5Lib、Six）。 安装过程相当标准：从各自的链接获取库，然后解压它们。 在终端中，进入解压后的目录并为每个库运行 `setup.py install`。 它们现在就可以使用了。

### 02 创建一些有用的变量

这些变量将跟踪脚本运行期间我们访问过的链接：`addresses` 是一个包含我们访问过的所有链接的列表；`deepestAddresses` 是从起点链接树最深的页面的链接；`storeFolder` 是我们将保存创建的 HTML 文件的位置，而 `maxLevel` 是我们可以从起始页面追踪链接的最大深度。

### 03 处理用户输入

在这个函数的开头几行，我们只是创建了一个辅助语句。 之后，我们解析程序执行时传入的任何参数，并查找 `-URL` 标志和 `-levels` 标志。 `-levels` 标志是可选的，因为我们已经预设了要追踪链接的深度，但我们需要一个起始链接，因此如果缺少 `-URL` 标志，我们将提示用户并退出。 如果我们有链接，那么我们会快速检查是否有存储文件的目录——如果没有则创建——然后我们将启动函数来获取该页面。 最后，我们注册一个脚本尝试退出时的处理程序。 我们稍后会讲到那部分。

### 04 从 URL 获取页面

这里我们使用 `URLLib2` 请求用户要求的页面，然后，一旦我们收到该页面，我们将把内容传递给 Beautiful Soup 的 `soup` 变量。 这使我们能够访问我们在解析文档时将调用的方法。

### 05 去除冗余

Wikipedia 有很多我们不想解析的节点。 `content` 变量允许我们直接忽略 Wikipedia 大部分 GUI，但仍有很多元素我们不想解析。 我们通过遍历我们创建的 `undesirables` 列表来解决这个问题

> "Wikipedia 有很多节点"

```
for link in content.find_all('a'):
    href = link["href"]
    if isValidLink(href):
        if level < maxlevel:
            stored = False
            for addr in addresses:
                if addr == link.get("href"):
                    stored = True
            if(stored == False):
                title = link.get("href").replace("/wiki/", "")
                addresses.append(str(title + ".html"))
                grabPage("http://en.wikipedia.org" + link.get("href"), level + 1, title)
                print title
        link["href"] = link["href"].replace("/wiki/", "") + ".html"

fileName = str(name)

if level == maxlevel:
    deepestAddresses.append(fileName.replace('/', '_') + ".html")

doctype = "<!DOCTYPE html>"
head = "<head><meta charset=\"UTF-8\" /></title>" + fileName + "</title></head>"
f = open(storeFolder + "/" + fileName.replace('/', '.') + ".html", 'w')
f.write(doctype + "<html lang=\"en\">\n" + head + "<body><h1>" + fileName + "</h1>" + str(content) + "</body></html>")
f.close()
```

### STYLING
Currently, the HTML page will use the built-in browser styles when rendering the page. If you like, you can include the style sheet included in the tutorial resources to make it look a little nicer. To use it, you can minify the script and include it inside a `<style>` tag in the head string on line 102, or you can rewrite the head string to something like:
`head = "<head><meta charset=\"UTF-8\"/><title>" + fileName + "</title><style>" + str(open('/PATH/TO/STYLES/', 'r').read()) + "</style></head>"`

earlier on in the document. For each different div/section/node that we don't want, we call Beautiful Soup's `find_all()` method and use the `extract()` method to remove that node from the document. At the end of the undesirables loop, most of the content we don't want any more will be gone. We also look for the 'also' element in the Wiki page. Generally, everything after this div is of no use to us. By calling the `find_all_next()` method on the also node, we can get a list of every other element we can remove from that point on.

> Beautiful Soup is a fast framework for many Python HTML parsers

### 06 Grabbing the links

By calling `content.find_all('a')` we get a list of every `<a>` in the document. We can iterate through this and check whether or not there is a valid Wikipedia link in the `<a>`'s href. If the link is a valid link, we quickly check how far down the link tree we are from the original page. If we've reached the maximum depth we can go, we'll store this page and call it quits, otherwise we'll start looking for links that we can grab within it. For every page we request, we append its URL to the `addresses` list; to make sure we don't call the same page twice for each link we find, we check if we've already stored it. If we have, then we'll skip over the rest of the loop, but if we've not then we'll add it to the list of URLs that we've requested and fire off a request. Once that check is done. We then do a quick string replace on that link so that it points to the local directory, not to the subfolder `/wiki/` that it's looking for.

### 07 Writing to file

Now we create a file to store the newly parsed document in for later reading. We change any `'/'` in the filename to `'.'` so the script doesn't try and write to a random folder. We also do a quick check to see how many links we've followed since the first page. If it's the max level, we'll add it to the `deepestAddresses` list. We'll use this a little bit later.

### 08 Tying up loose ends

After our script has iterated through every link on every page to the maximum level of depth that it can, it will try to exit. On line 34 of the code (on the disc and online) in the `init` function, we registered the function `cleanUp` to execute on the program trying to exit: `cleanUp`'s job is to go through the documents that we've downloaded and check that every link we've left in the pages does in fact link to a file that we have available. If it can't match the link in the href to a file in the `addresses` list, it will remove it. Once we're done, we will have a fully portable chunk of Wikipedia we can take with us.

## 使用 Python 创建

- 108 使用 Kivy 构建井字棋
- 编程剪刀石头布
- 112 创建双步验证
- 使用 Twilio 进行安全认证
- 116 Twitter 的 OAuth 流程
- 构建签名请求
- 120 编程一个太空入侵者克隆
- 制作基础的 Pivaders 游戏
- 124 添加动画和音效
- 增强你的 Pivaders 游戏
- 128 制作视觉小说
- 编程一本图书风格的游戏

![](img/3b256f430f51c98f1315671f6e4eec19_105_0.png)

> "Python 可以帮助创建令人惊叹且有趣的项目"

![](img/3b256f430f51c98f1315671f6e4eec19_105_1.png)

![](img/3b256f430f51c98f1315671f6e4eec19_105_2.png)

SCORE 0

LIVES 3

## 使用 Kivy 构建井字棋

通过仅用 100 多行 Python 创建纸笔经典游戏，轻松了解 Kivy 的工作原理...

Kivy 是一个高度跨平台的 Python 图形框架，专为创建创新用户界面如多点触控应用而设计。它的应用不仅可以在传统的 Linux、OS X 和 Windows 桌面平台上运行，还可以在 Android 和 iOS 上运行，以及像 Raspberry Pi 这样的设备上运行

这意味着你可以使用 `Requests`、`SQLAlchemy` 或甚至 `NumPy` 等 Python 库开发跨平台应用。你甚至可以通过 Kivy 的一些姊妹项目直接从 Python 访问原生移动 API。另一个很棒的功能是 Cython 优化的 OpenGL 图形管线，即使基本的 Python API 非常简单，也能实现高级 GPU 效果。

Kivy 是一组可通过 `pip` 轻松安装的 Python/Cython 模块，但你需要一些依赖项。它使用 `PyGame` 作为渲染后端（尽管其 API 未暴露），使用 Cython 编译快速的图形编译器内部，使用 GStreamer 处理多媒体。这些都应该可以通过你的发行版仓库获得，或在适用时通过 `pip` 获得。

满足这些依赖后，你应该能够使用正常的 `pip` 咒语安装 Kivy。当前版本是 1.8.0，同一个代码库同时支持 python2 和 python3。本教程中的代码也是版本无关的，可在 python2.7 和 python3.3 中运行。

```
pip install kivy
```

如果 `pip` 有任何问题，你可以使用 `easy_install` via `easy_install kivy`。

对于几个流行的发行版，也提供有包或仓库。你可以在 Kivy 的网站上找到更多信息。一个 Kivy 应用是通过实例化并运行一个 `App` 类来启动的。这就是初始化我们应用窗口、与操作系统交互并为创建 GUI 提供入口点的地方。我们可以先制作最简单的 Kivy 应用：

```
```

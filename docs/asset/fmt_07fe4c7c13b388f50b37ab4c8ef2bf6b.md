
In Listing 2, the `for` loop starting in line 24 assembles the list of entries in the main menu as an array slice of strings that it generates from the lyrics map's keys. The keys in the map are by definition unsorted; therefore, the `sort.Strings()` function from the standard library puts the string list in alphabetical order in line 27. Go’s built-in `Sort()` function sorts an array slice of strings in place (i.e., it actually modifies the input array instead of producing a new, sorted version).

在 `Listing 2` 中，从第 24 行开始的 `for` 循环将主菜单条目列表组装成字符串切片，该切片是由歌词 `map` 的键生成的。根据定义，`map` 中的键是无序的；因此，标准库中的 `sort.Strings()` 函数在第 27 行将字符串列表按字母顺序排序。`Go` 内置的 `Sort()` 函数会原地对字符串切片进行排序（即它实际上修改了输入数组，而不是产生一个新的排序版本）。

`Listing 2` 现在只需要处理活动和非活动列表框条目的亮色定义，并移交控制权。

```go
08
)
44 }
09
45 ifFocus == ltext {
10
func handleUI(lb *widgets.List, ltext *widgets.List, 46 morelines := false
11 lyrics map[string]Lyrics) {
47 for scanner.Scan() {
12
48 line := scanner.Text()
13 ui.Render(lb)
49 if line == "" {
50 inFocus := lb
51 continue
51 }
51 uiEvents := ui.PollEvents()
52
Itext.Rows = append(Itext.Rows, line) 17 var scanner *bufio.Scanner
53 morelines = true
18
54 Itext.ScrollDown()
19 for {
55 ui.Render(Itext)
20 select {
56 break
21 case e := <-uiEvents:
57 }
22 switch e.ID {
58 if !morelines {
23 case "q", "<C-c>": 59 inFocus = lb
24 return
60 Itext.Rows = Itext.Rows[:0]
25 case "j", "<Down>": 61
26 if inFocus == lb {
62 }
27 lb.ScrollDown()
63 }
28 ui.Render(lb)
29 }
64 case "<Escape>":
30 case "k", "<Up>": 65 inFocus = lb
31 if inFocus == lb {
66 Itext.Rows = Itext.Rows[:0]
32 lb.ScrollUp()
67 ui.Render(lb)
33 ui.Render(lb)
68 }
34 }
69 }
35 case "<Enter>":
70 }
36 if inFocus == lb {
71 }
```

处理过程取决于当前使用的模式。文本扫描器检索当前活跃的文本。如果用户处于主菜单中的多行内容中的下一行，`inFocus` 被设置为 `lb`，且第 47 行使用所选行的索引；它会丢弃任何空行，并将新读取的行添加到 `Itext` 列表框的数组中。`ScrollDown()` 将显示器中的新行标记为活跃，`if` 块将 `inFocus` 变量设置为 `Ltext`，从而激活红色的歌词文本。同样，整个过程都是可视化的。在第 41 行新定义的扫描器（`scanner`）从歌词结构中获取带有歌词行的文本字符串，并且记住，请以适中的音量唱歌，以考虑到邻居！如果歌曲结束（即扫描器失败，并且每次调用其 `Scan()` 方法时都无法返回下一个字符串行），`if` 块将从第 58 行开始从主菜单中从 `Ltext` 列表框中删除文本行，然后通过将 `inFocus` 指向 `lb` 回到主菜单模式。同一个歌词列表框被传递给 `ui.Render()`。如果用户按下 `Esc` 则会发生变化；在这种情况下，`case` 块切换到模式，第 45 行开始的 `if` 块是第 64 行开始的主菜单。

### 快速构建

要创建控制从 A 到 Z 控制工具的歌词二进制文件，你只需要编译所有的三个列表，如列表 5 所示。初始调用 `go mod` 会初始化一个新的 `Go` 模块，它告诉随后的 `go build` 从 `GitHub` 获取所有所需的包并将它们也包含进来。成功构建后，确保你的数据目录中填充了几个 `YAML` 格式的歌曲歌词，然后调用 `ui.Render()`。

**列表 5：生成二进制文件**

```bash
$ go mod init lyrics
$ go build lyrics.go find.go
```

## 深度解析

### `Jam.py`

#### 使用 `Jam.py` 构建数据库前端

#### 数据窗口

使用 `Jam.py` 为你的数据库创建一个方便的界面。

**作者：** `Marco Fioretti`

要使用 `Jam.py`，你只需要

`Jam.py` 是一个开源环境，允许你为数据库构建基于浏览器的界面。最重要的组是 `Catalogs`（目录）。`Catalogs` 是你浏览器中的标签页或窗口。在日志和期刊（`Journals`）中加载这些客户端网页。`Catalogs` 是存储实际记录（如发票）的表。

使用 `Jam.py`，你可以在 `SQLite`、`PostgreSQL`、`MySQL`、`Firebird`、`MSSQL` 或 `Oracle` 中设计并共享数据。`Jam.py` 框架由两个部分组成：与任何关系或非关系数据库交互的服务器端。

客户端是一对动态网页。在实践中，你将使用默认模板或自定义网页。第一页是主页（`Home page`），你可以根据数据库查询的结果生成图表。第二页是可以修改数据库中表的地方。

`LINUX-MAGAZINE.COM` | `LINUXPROMAGAZINE.COM`

**第 241 期**

**2020年12月**

如果你想运行多个 `Jam.py`

```
#> jam-project.py
```

最后，报告与数据库记录链接的报告模板或静态文件（如图像）。同时，在同一台计算机上重复上述所有步骤。

`jam-project.py` 命令会为每个应用程序创建以下文件和文件夹，为每个应用程序提供专属的文件夹和 `TCP` 端口号。两个扩展名为 `.sqlite` 的文件是 `SQLite3` 单文件无服务器数据库，包含了配置和本地化数据。当然，每个应用程序的首页和 `Builder` 页面的 `URL` 需要更改以反映端口号。

```
#> ls -I
```

* `.sqlite`
* `css`
* `server.py`
* `index.html`
* `js`
* `langs.sqlite`
* `__pycache__`

为了配置和运行你的 `Jam.py` 应用程序，你必须启动正确的端口号。`server.py` 脚本。当我启动 `server.py` 时，在你熟悉 `Jam.py` 的工作原理之前，我遇到了另一个意之外的错误：

```
#> ./server.py
/usr/bin/env: 'python': U
No such file or directory
```

#### 一个简单的书签管理器

* `server.py`
* `static`
* `wsgi.py`
* `index.html`

这个问题可能是因为我自己的 `Ubuntu` 机器由于测试过多导致配置不当。在《`Linux Magazine`》第 232 期中，我介绍了 `Shaarli` 在线书签管理器 [3]。我仍然使用 `Shaarli` 管理快速书签，但在写完那篇文章后，我意识到快速修复的方法是显式向 `server.py` 传递系统中 `Python 3` 的位置，替换脚本的第一行：本文前面的部分，而且 `server.py` 是我收集的书签的接口。我需要一个比 `Shaarli` 更快且更适合脚本的浏览器界面。最重要的是，我需要一个兼容复杂搜索并能够处理 `SQL` 格式搜索数据的界面。

```python
#! /usr/bin/env python
#! /usr/bin/python3
```

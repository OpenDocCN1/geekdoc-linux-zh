
此外，你需要从零开始构建你的图形图像。`kivy` 子集包含许多图形原语，你可以使用它们创建诸如圆形、矩形、矩形曲线和三角形等形状。有一个

> 既然 Kivy 是一个完整的工具包，它将涉及一些用于封装功能部分的模板代码

- 在你的桌面上操作

使用 Kivy 开发应用，你可以轻松地在桌面上完成你的代码。然后你可以将其移动到移动项目中，无需更改代码！对于习惯了描述性 Kivy 语言的人来说，Kivy 提供了行为相同的 Kivy 语言。

还有其他方法来更改这些图形元素，包括缩放和旋转等函数。此外，你还有其他标准元素，如弹出窗口和标签，它们允许你。

## Python 教程：Kivy

甚至不知道它们实际上在屏幕上是如何布局的。与许多其他工具包相比，Kivy 给你一组类，称为布局（layouts），它们负责管理物理结构。作为一个基本示例，以下代码绘制了两个按钮，一个在上在上：

```python
layout = BoxLayout(orientation='vertical')
btn1 = Button(text='Hello')
btn2 = Button(text='World')
layout.add_widget(btn1)
layout.add_widget(btn2)
```

给定列中的组件需要相同的宽度，任何给定行的组件需要相同的高度。如果你想在组件的尺寸上更灵活，你可能想要使用堆叠布局（stack layout）。在堆叠布局中，给定行的组件不再需要相同的宽度或高度。你可以通过使用网格布局（grid layout）增加另一个维度。这创建了一个多页布局，可以在每个页面上添加组件，你可以垂直或水平地进行翻转排列。

第一行创建一个多页布局，可以在每个页面上添加组件，你可以垂直或水平地进行翻转排列。移动维度，你可以使用网格布局按垂直或水平方向排列组件。与许多其他图形布局不同，网格对组件的放置位置没有直接控制；你只需要按照它们顺序放置即可。你可以定义网格布局至少的列或行，且组件的尺寸需要匹配。也就是说，所有的 Kivy 都从底层接口构建到高层对象，如

## Kivy 架构

使用边界框来回切换。更具结构化的布局使用锚点（anchor）。在这种情况下，你定义 `anchor_x` 和 `anchor_y`。这本质上是将锚点的子元素固定在其他一个上。

## 与世界交互

我们需要接受任何形式的输入 - 我们在早期的一些示例中已经看到了按钮。除了按钮之外，Kivy 提供了一个切换按钮（toggle button），它以许多方式处理触摸。你可以使用 `group` 让它的行为就像单选按钮一样。在这种情况下，

| 缓存 | 时钟 | 事件 | 属性 |
| :--- | :--- | :--- | :--- |
| 核心 | 图形 | 输入 | |
| 窗口 | 帧缓冲区 | 运动 | |
| 文本 | 纹理 | 处理 | |
| 图像 | 着色器 | 双击, 点击, | |
| 视频 | 指令 | | |
| Pygame | GLEW | TUI | |

> from kivy.uix.slider import Slider s = Slider(min=-100, max=100)

你可以通过检查滑块的值来读取用户选择的值。你也可以设置此值，这将滑块滑动到屏幕上的该位置。对于文本输入，Kivy 有几个选项。第一个是 `TextInput`，它允许你向文本框添加文本。你还可以处理文本框的移动以及与操作系统的剪贴板。如果你需要更健壮的输入，你可能需要查看代码列表。这个列表本质上是空的，你还需要安装 Python 模块 `pygments`，因为它为该组件提供高亮。`pygments` 支持的任何语言都可以在代码编辑器中进行高亮。例如，以下代码创建了一个可以高亮代码的输入组件：

```python
from kivy.uix.codeinput import CodeInput
from pygments.lexers import PythonLexer
instance = CodeInput(lexer=PythonLexer())
```

`pygments` 使用了大量的“词法器”（lexers），但在你需要为某些冷门语言构建词法器的情况下，你可以构建自己的。

## 管理事件

我们查看了各种选项，以及用户如何输入数据或与你的程序交互。但你如何管理由这些事件触发的操作呢？每当你点击按钮或触摸时，事件会在 Kivy 内部触发。`EventDispatcher` 在后台处理这些事件。所有事件都通过回调管理，回调可以绑定到一个或多个事件上。组件的一部分提供了几个示例。以下代码通知你状态的任何变化：

```python
def callback(instance):
    print("My button %s state is %s" % (instance.name, instance.state))
    instance.text = "Hello World!"
    return True
```

这把回调绑定到函数的状态属性上，当它改变时，它会改变类属性。你可以使用类的 `register_event()` 方法创建你自己的回调。有了所有这些事件，还有 `MotionEvent` 的实例。这些是由组件的 `on_method()` 分发的，通常作为 `on_touch_down`、`on_touch_move` 和 `on_touch_up`。你可以绑定这些事件中的任何一个；以下代码是一个示例：

```python
def on_touch_down(self, touch):
    if super(ClassName, self).on_touch_down(touch):
        return True
    if self.collide_point(touch.pos):
        print("You touched me!")
        return True
    return False
```

你注意上面示例中对 `super` 的引用。例如，当你使用这些事件时，它们是由你生成的，你负责实现所有所需的功能。对于你不感兴趣的部分，你可以使用基类的代码。

最后一类事件是由视图生成的。由于 Kivy 的事件循环，如果你重复执行代码，就不能有无限循环，这将阻塞视图的其余部分。例如，但如果你有理由在事件处理程序中重复一段代码，此此最佳方法是使用 `Clock` 对象。通过 `Clock`，你可以调度函数在未来的某个点执行，无论是一次还是循环执行。例如，以下代码每秒调用一次回调。

```python
def my_callback(dt):
    pass
Clock.schedule_interval(my_callback, 1.0)
```

在这个示例中，函数并没有执行任何操作。参数 `dt` 是时间，它是自上次调用以来经过的时间。

## 非类组件

还有几个其他类为你的组件提供了很好的功能。`Animation` 类提供了一组预包的过渡，平滑地从一个状态移动到另一个。例如，`Label` 对象允许你渲染文本，并隐藏和拖动代码气泡。我们在这里有机会讨论了文本，但确实有一个 `Atlas` 类允许你将许多纹理构建到单个图像中。这有助于简化加载，例如，等等。

最后一个类是 `UrlRequest`。它提供了一种与本地主机互联网交互的方法。通过这种方式，你可以在等待完成时从网站下载文件。

- 使用变量

你可以通过使用环境变量方便地控制 Kivy 的功能。例如，你可能会使用 `WIDOM` 来告诉。这将强制 Kivy 使用 X11 窗口环境。你还可以控制音频、摄像头使用以及使用的实现，其他其他元素。配置

# 编程教程：Go

## 第一部分

### Go：编写你自己的视频共享服务器

上手 Go，这门由 Google 开发并使用的开源语言

![](img/70966a5e893fbac28b7b2b33528eb018_51_0.png)

```go
func loadVideo(id string) (*Video, error) {
    filename := "videos/" + id + ".mp4"
    videoData, err := io.ReadFile(filename)
    if err != nil {
        return nil, err
    }
    title := string(videoData)
    video := &Video{ID: id, Title: title}
    return video, nil
}

func renderTemplate(w http.ResponseWriter, r *http.Request) {
    tmpl, err := template.ParseFiles("template.html")
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError)
        return
    }
    tmpl.Execute(w, nil)
}

func watchHandler(w http.ResponseWriter, r *http.Request) {
    id := r.URL.Query().Get("id")
    if id == "" {
        http.Error(w, "Missing ID", http.StatusBadRequest)
        return
    }
    renderTemplate(w, "watch", id)
}
```

**我们使用 Go 构建了一个动态视频共享服务器并运行了它**

直到几年前，所有的 Go 程序都是用 C++ 编写的。虽然 C++ 运行速度极快，但也容易出现许多问题，例如缺乏内置并发支持，以及由于 C++ 处理依赖的方式导致构建时间缓慢。

Go 在 2009 年发布了该语言。它的引入是为了解决与 C++ 存在的某些问题，加快构建速度并使代码更具可读性和可维护性。在取得巨大成功后，2012 年，Fitzpatrick（LiveJournal 的创建者，现任 Google 员工）决定用 Go 重写它——用户下载 Go 就是为了运行它——期望以微小的性能损失换取更具读性的代码库。生成的代码不仅可读性得多，而且在编译和运行时，速度与 C++ 原版一样快，且内存内存更少。

Go 的设计并不是为了引入时尚特性；它的设计是为了成为创建如今 Google 所使用的大型应用的最佳工具。

## 关于此项目

Go 是一门开源语言，非常上手。2011 年感恩节的 Google Doodle（谷歌涂鸦）展示了一个带有可切换功能的旅行，它是由一位该语言新手的 Go 员工在 24 小时内完全用 Go 编写的。

本教程在很大程度上依赖 Go 和 YouTube，所以当我们想要创建自己的版本时：LuTube，一个为 Linux 用户设计的站点视频共享网站。在接下来的三篇文章中，我们将开发一个简单的 Web 服务器，允许用户观看、搜索和上传视频，所有内容将用 Go 编写。每个月，我们都会发布上一期的可用代码，这样即使你没有跟进文章也可以直接上手。这是该系列的第一期，我们将从零开始。

我们不会假设你已经熟悉 Go，但熟悉 C++ 或 Go 等语言的编程知识对于讨论 Web 应用会有帮助。

## 类型

为了开始，我们将创建一个目录 `lutube` 并进入该目录。这将是我们的服务器，视频本身将放在一个名为 `videos` 的目录中。

```bash
$ mkdir lutube
cd lutube
$ mkdir videos
```

在 `lutube` 目录内创建一个新文件 `lutube.go` 并用文本编辑器打开它。在顶部添加以下行；这会告诉 Go 代码包含程序启动时应运行的 `main` 函数。

```go
package main
```

在编写任何内容之前，让我们先谈谈我们将如何存储和返回视频。我们网站上的视频不仅仅是一个片段；它还有标题、长度和上传日期。我们将为每个视频分配一个唯一的 ID，对应 videos 目录下的子目录。这将位于视频文件内部，以及其他存储任何附加信息的文件。

Go 没有错误捕获语法；相反，错误作为普通值传递。

目前，我们将创建一个结构体（struct）来编码视频。我们将它来固定视频的 ID 标题。

```go
type Video struct {
	id    string
	title string
}
```

你会注意到这与 C 中创建结构体的方式有几处不同。值得注意的是，在 Go 中变量的类型有多种声明方式。这类似于 Haskell、Ada 或 Rust 等语言的语法，在这些语言中我们会写 `ID string`；而我们使用冒号。

我们将名为 `videodata.txt` 的标题文件存储在视频目录下。让我们写一个函数，接收一个 ID 并返回一个 Video 结构体，其中通过查找 `videodata.txt` 文件来填充 `Title` 字段。

## 图 1

```go
func loadVideo(id string) (*Video, error) {
	filename := id + "/videodata.txt"
	videoData, err := ioutil.ReadFile(filename)
	if err != nil {
		return nil, err
	}
	title := string(videoData)
	return &Video{id: id, title: title}, nil
}
```

上述 Go 中的错误检查并不涉及（某种）。这是用 Go 编写的函数示例。你会注意到 Go 使用 `func` 返回值，并且在类型（在此处是结构体指针）处 `return`。这里是 Go 语法的其他示例；例如我们经常使用 `:=` 来创建和初始化变量。变量的类型是推断的。该行表明函数可以返回多个值，我们在 Go 中使用了 `:=`。

```go
func loadVideo(id string) (*Video, error) {
	filename := id + "/videodata.txt"
	videoData, err := ioutil.ReadFile(filename)
	if err != nil {
		return nil, err
	}
	title := string(videoData)
	return &Video{id: id, title: title}, nil
}
```

然后，我们将返回错误：

```go
func loadVideo(id string) (*Video, error) {
	filename := id + "/videodata.txt"
	videoData, err := ioutil.ReadFile(filename)
	if err != nil {
		return nil, err
	}
	title := string(videoData)
	return &Video{id: id, title: title}, nil
}
```

`nil` 值被用来显示视频的缺失。Go 没有特殊的捕获语法；相反，错误作为普通值传递。在这种情况下我们说：如果有错误，则为 `Video` 结构体返回 `nil`。我们也应该修改返回语句，以便在一切顺利时返回 `nil`，如下所示：

```go
return &Video{id: id, title: title}, nil
```

完整的函数如图 1 所示。为了使其正确，我们还需要做最后一件事，即在顶部添加 `package main`。这是因为我们使用了 `ioutil` 库中的 `ReadFile` 函数。

```go
package main

import "io/ioutil"
```

## 设置 Web 服务器

现在我们已经创建了处理请求的基础，让我们专注于设置 Web 服务器。首先，我们将创建一个在程序启动时运行的 `main` 函数：

第一个语句在下面的代码中显示了路径 `/watch`（未见函数）。这样分组 `import` 语句被认为是更好的做法：

```go
import (
  "fmt"
  "io/ioutil"
  "log"
  "net/http"
)

func main() {
    http.HandleFunc("/watch", handler)
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

- 在编程语言中，哪些包依赖哪些包是困难的。在 C++ 中，很难知道某行代码需要哪个包，或者代码包含了它并不意味着它没有被使用。Go 提供了一种在早期解决这些问题的方法，这样以后就不会困惑。

- 在 Go 中，未使用的 `import` 不仅是浪费，还会导致编译器拒绝程序。通过这种方式，我们确保导入的包是运行程序所需的，以保持二进制文件尽可能小。

- 另一个重要特性是 Go 禁止循环依赖，防止导致可执行文件体积更大的循环。

- 最后，Go 处理二进制的方式比 C++ 高得多，依赖只加载一次，即使被多个包引用。

![](img/70966a5e893fbac28b7b2b33528eb018_53_1.png)

`handler` 将调用 `http.ListenAndServe`。效果是在当我们位于系统的 8080 端口时，如果打开浏览器并导航到 http://localhost:8080/watch，Go 将调用 handler 函数来确定 HTTP 响应。为了看到运行效果，让我们创建一个 handler 函数的初始版本：

```go
func handler(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "text/html")
    fmt.Fprintf(w, "<h1>Hello World!</h1>")
}
```

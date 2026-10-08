

## 使用 Beautiful Soup 爬取维基百科

## 收尾工作

08 在我们的脚本遍历每个页面上的每个链接并达到它能达的最大深度后，它将尝试退出。在代码中 `init` 函数（磁盘和在线版本）的第 34 行，我们注册了 `cleanUp` 函数在程序退出时执行；`cleanUp` 的任务是遍历我们下载的文档，并检查我们在页面中下的每个链接是否确实指向一个我们可以使用的的文件。如果无法将文件中的链接与地址列表匹配，将将其删除。一旦完成，我们就拥有了一个完全便携的维基百科片段，可以随带使用。

06 复制到文件 之后，我们将解析出的内容放入一个全新的 HTML 文件

```python
doctype = "!DOCTYPE html"
head = "<head<meta charset='UTF-8'/></title>" + fileName + "</title>"
f = open(storeFolder + "/" + fileName.replace('_', '_') + ".html", 'w')
f.write(doctype + "<html>\n" + head + "<body><h1>" + content + "</h1></body></html>")
f.close()
```

```python
def cleanup(soup):
    print("\n正在移除指向未保存页面的链接\n")
    for deepPage in deepestAddresses:
        rf = open(storeFolder + "/" + deepPage, 'r')
        deepSoup = BeautifulSoup(rf.read(), 'html5lib', from_encoding='UTF-8')
        for link in deepSoup.find_all('a'):
            pageStored = False
            for addr in addresses:
                if addr == link:
                    pageStored = True
            if pageStored == False:
                if '#' is not in link:
                    del deepLinks[link['href']]
                elif '#' in link and len(link.split('#')) > 1 or ':' in link:
                    del deepLinks[link['href']]
            wf = open(storeFolder + "/" + deepPage, 'w')
            wf.write(deepSoup)
            wf.close()
```

07 清理 一旦每个页面都已解析并存储，我们将遍历并尝试移除任何死链接

08 初始化 这是我们初始化脚本的方式

```python
print("Complete")
if __name__ == "__main__":
    init()
```

![](img/c72194f2c3aec198936695a665a5167c_76_0.png)

## 使用 Python 创建

享受编程的乐趣

![](img/c72194f2c3aec198936695a665a5167c_77_0.png)

## 使用 Python 创建

使用 Python 发挥创意并编写游戏
还有比玩一个自己编写的游戏更令人满足的呢？在本节中，我们将向你展示如何实现这一点。我们将从一个借助 Kivy (p.80) 制作的简单井井棋游戏开始，然后进阶克隆经典的喜爱游戏——乒乓球 (Pong, p.86)。接着，是时候尝试制作一个带有复古画面的受《太空入侵者》启发的游戏了 (p.88)。最后，你将学习如何制作一个精版的“自选冒险”游戏 (p.98)。

## 享受编程的乐趣

## 使用 Python 创建

![](img/c72194f2c3aec198936695a665a5167c_78_0.png)

“制作一个可玩的游戏并没有你想象的那么困难”

## 使用 Python 创建

## 使用 Kivy 构建井井棋

你可能需要的...

**Python**
www.python.org/doc

## 使用 Kivy 构建井井棋

通过在100多行 Python 代码中创建井井棋，轻松熟悉 Kivy 的原理...

Kivy 是一个为 Python 设计的跨平台图形框架，用于创建新的多触摸用户界面。它的应用程序不仅可以在 Linux、OS X 和 Windows 等传统桌面平台运行，还可以在 Android、iOS 以及树莓派等设备上运行。这意味着你可以使用 Requests、SQLAlchemy 甚至 NumPy 等 Python 库来开发跨平台应用。访问原生 API。另一个优秀特性是 Kivy 优化的图形管线，允许实现高级视觉效果，尽管基础 API 非常简单。

Kivy 是一组 Python/Cython 模块，可以通过 pip 轻松地安装，但你需要一些依赖项。它使用 Pygame 作为渲染后端（尽管其 API 未暴露），使用 Cython 进行图形编译，使用 Gstreamer 处理多媒体。这些应该可以通过你的发行版或 pip 获取。在满足这些依赖项后，你应该通过正常指令安装 Kivy。当前版本是 1.8.0，相同的代码支持 python2 和 python3。本教程的代码与版本无关，运行在 python2.7 和 python3 中。

```bash
pip install kivy
```

如果你在 pip 上遇到任何问题，可以使用发行版提供的 easy_install。你可以在 Kivy 网站找到更多信息。Kivy 应用通过实例化和运行 'App' 类启动，这是初始化窗口并提供![](img/c72194f2c3aec198936695a665a5167c_79_png)

## 使用 Kivy 构建井井棋 使用 Python

创建我们 GUI 的入口。我们可以开始制作最简单的 Kivy 应用：

```python
from kivy.app import App

class TicTacToeApp(App):
    pass

if __name__ == "__main__":
    TicTacToeApp().run()
```

你可以轻松运行它，你的应用将启动并获得一个空白窗口。太兴奋了！我们可以用 Kivy 组件构建自己的 GUI。每个组件都是具有特定行为的简单元素，从标准 GUI 功能（例如 Button, Label）到子组件布局（例如 BoxLayout, GridLayout），再到更复杂的硬件交互任务（例如 FileChooser, VideoPlayer）。重要的是，Kivy 的组件设计为易于组合——包括想象中的每一个组件，组件保持简单，但我们将在教程中看到一些![](img/c72194f2c3aec198936695a665a5167c_80_png)

```python
def build(self):
    return Label(text='Hello World!',
                 font_size=100,
                 color=(r, g, b, a))
```

'build' 方法在 'App' 时被调用，返回值就是 App 的根。在我们的情况下它是一个 Label，我们设置了几个属性——'text'、'font_size' 和 'color'。所有组件都有控制外观的不同属性，可以动态更新，在这里我们只看到一次：

- 注意，属性不仅仅是 Python 属性，而是 Kivy 内部的属性。这些访问方式像普通属性，但通过挂钩 Kivy 的事件系统提供了额外功能。
- 我们将看到创建属性的示例，如果你要在 Kivy 的事件和绑定中使用你的变量，也应该这样做。
- 你只需要显示一些简单的文本，所以再次运行程序检查这是否有效。如果任何参数不清楚，请尝试实验。

```python
from kivy.uix.label import Label
```

我们将通过返回 'Label' 作为应用的根组件来显示它。每个应用都有一个根组件，顶层文本，它会自动调整大小以填充窗口。稍后我们将看到如何通过添加更多组件来构建 GUI，但现在通过向 'App' 添加一个新方法来设置根组件就足够：

## 使用 Python 创建

## 使用 Kivy 构建井井棋

我们的组件：井井棋

由于 Kivy 没有井井棋，我们必须自己制作！我们将创建一个新的组件类来包含这些子组件。这个示例演示了前者，通过声明每个实例化的 'TicTacGrid' 都应该将其 'cols' 属性设置为 3，为 'TicTacGrid' 组件创建了一个规则。

```python
from kivy.uix.gridlayout import GridLayout
class TicTacGrid(GridLayout):
    pass
```

我们将稍后使用更多布局功能，但现在回到 Python 在你的井井棋网格中创建按钮。现在这显然没有做什么，除了它继承了 Kivy GridLayout 组件的所有行为——我们需要告诉它有多少列，但随后它将安排任何组件以整齐的行形式排列。井井棋需要三列和九个子组件。

```python
from kivy.uix.button import Button
from kivy.properties import ListProperty
```

```python
class GridEntry(Button):
    coords = ListProperty([0, 0])
```

在这里我们引入 Kivy 语言 (kv)，一种用于创建 Kivy 树的特殊领域特定语言。它简单但消除了许多管理 UI 所需的样板代码——作为类比，你可能会认为它是 HTML/CSS 之于 JavaScript。Python 给了我们做任何事情的动态权力，但如果我们只想声明 UI 的基础结构，可能永远不需要 Kivy 语言，你完全可以在纯 Python 中实现同样的功能。

这种继承自 Kivy 的组件，与鼠标或触摸交互，在切换时分发事件。我们可以挂钩这些事件，在用户按下按钮时调用自己的函数，并设置按钮的 'text' 属性以显示 'X' 或 'O'。我们为组件创建了一个新的 Kivy 属性，'coords'——稍后我们将展示这有多用。这与在 `GridEntry.__init__` 中通过编写 `self, coords = [0, 0]` Python 属性几乎相同。

Kivy 提供了使用 kv 所需的所有工具，最简单的方法将其写在一个根据你的 App 类命名的文件中。也就是说，我们应该将以下内容放在名为 'tictacttoe.kv' 的文件中：

对于 'TicTacGrid'我们将使用 kv 语言样式化我们的新类，但这次我们可以看到一些有趣的。

```kv
<TicTacGrid:
cols: 3
```

```kv
<GridEntry>:
font_size: self.height
```


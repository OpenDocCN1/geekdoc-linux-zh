
你可以轻松运行它，你的应用将启动并获得一个空白窗口。太兴奋了！我们可以用 Kivy 组件构建自己的 GUI。每个组件都是具有特定行为的简单元素，从标准 GUI 功能（例如 `Button`, `Label`）到子组件布局（例如 `BoxLayout`, `GridLayout`），再到更复杂的硬件交互任务（例如 `FileChooser`, `VideoPlayer`）。重要的是，Kivy 的组件设计为易于组合——包括想象中的每一个组件，组件保持简单，但我们将在教程中看到一些

```python
def build(self):
    return Label(text='Hello World!',
                 font_size=100,
                 color=(r, g, b, a))
```

`build` 方法在 `App` 时被调用，返回值就是 App 的根。在我们的情况下它是一个 `Label`，我们设置了几个属性——`text`、`font_size` 和 `color`。所有组件都有控制外观的不同属性，可以动态更新，在这里我们只看到一次：

- 注意，属性不仅仅是 Python 属性，而是 Kivy 内部的属性。这些访问方式像普通属性，但通过挂钩 Kivy 的事件系统提供了额外功能。
- 我们将看到创建属性的示例，如果你要在 Kivy 的事件和绑定中使用你的变量，也应该这样做。
- 你只需要显示一些简单的文本，所以再次运行程序检查这是否有效。如果任何参数不清楚，请尝试实验。

```python
from kivy.uix.label import Label
```

我们将通过返回 `Label` 作为应用的根组件来显示它。每个应用都有一个根组件，顶层文本，它会自动调整大小以填充窗口。稍后我们将看到如何通过添加更多组件来构建 GUI，但现在通过向 `App` 添加一个新方法来设置根组件就足够：

# 使用 Python 创建

## 使用 Kivy 构建井井棋

我们的组件：井井棋

由于 Kivy 没有井井棋，我们必须自己制作！我们将创建一个新的组件类来包含这些子组件。这个示例演示了前者，通过声明每个实例化的 `TicTacGrid` 都应该将其 `cols` 属性设置为 3，为 `TicTacGrid` 组件创建了一个规则。

```python
from kivy.uix.gridlayout import GridLayout

class TicTacGrid(GridLayout):
    pass
```

我们将稍后使用更多布局功能，但现在回到 Python 在你的井井棋网格中创建按钮。现在这显然没有做什么，除了它继承了 Kivy `GridLayout` 组件的所有行为——我们需要告诉它有多少列，但随后它将安排任何组件以整齐的行形式排列。井井棋需要三列和九个子组件。

```python
from kivy.uix.button import Button
from kivy.properties import ListProperty
```

```python
class GridEntry(Button):
    coords = ListProperty([0, 0])
```

在这里我们引入 Kivy 语言 `kv`，一种用于创建 Kivy 树的特殊领域特定语言。它简单但消除了许多管理 UI 所需的样板代码——作为类比，你可能会认为它是 HTML/CSS 之于 JavaScript。Python 给了我们做任何事情的动态权力，但如果我们只想声明 UI 的基础结构，可能永远不需要 Kivy 语言，你完全可以在纯 Python 中实现同样的功能。

这种继承自 Kivy 的组件，与鼠标或触摸交互，在切换时分发事件。我们可以挂钩这些事件，在用户按下按钮时调用自己的函数，并设置按钮的 `text` 属性以显示 `X` 或 `O`。我们为组件创建了一个新的 Kivy 属性，`coords`——稍后我们将展示这有多用。这与在 `GridEntry.__init__` 中通过编写 `self, coords = [0, 0]` Python 属性几乎相同。

Kivy 提供了使用 kv 所需的所有工具，最简单的方法将其写在一个根据你的 App 类命名的文件中。也就是说，我们应该将以下内容放在名为 `tictacttoe.kv` 的文件中：

对于 `TicTacGrid` 我们将使用 kv 语言样式化我们的新类，但这次我们可以看到一些有趣的。

```kv
<TicTacGrid:
cols: 3
```

```kv
<GridEntry>:
font_size: self.height
```

## 使用 Kivy 构建井井棋游戏

# 使用 Python 创建

从 Python 中创建这些绑定（除了稍后使用的 `bind` 方法外），通常并不像直接引用我们想要绑定的属性那样方便。

我们显示了它们，并知道它们会自动排列成我们之前设置的具有数字列的网格。

现在，我们必须将我们的根组件（从 `App.build` 返回）替换为 `TicTacToeGrid`，这样我们就能看到应用的样子了。

让我们向 `TicTacToeGrid` 中填充 `GridEntry` 小组件。

```python
class TicTacToeGrid(GridLayout):
    def __init__(self, *args, **kwargs):
        super(TicTacToeGrid, self).__init__(*args, **kwargs)
        for row in range(3):
            for column in range(3):
                grid_entry = GridEntry(
                    coords=(row, column))
                grid_entry.bind(on_release=self.button_pressed)
                self.add_widget(grid_entry)
```

```python
def build(self):
    return TicTacToeGrid()
```

通过此，你可以再次运行 Python 文件并享受你的新程序。一切正常，单个 `Label` 被替换为一个由九个按钮组成的网格，每个按钮都可以点击（它会自动改变），并且你会看到来自你绑定的输出信息。

我们可以通过修改 Button 的其他属性来定制外观，但现在我们让它们保持原样。

```python
def button_pressed(self, instance):
    print('button clicked!'.format(instance.coords))
```

有人获胜了吗？
我们需要跟踪棋盘的状态以检查是否有人获胜，我们可以通过多个 Kivy 属性来实现。

这里引入了一个新概念：当我们实例化 `GridEntry` 小组件时，我们能够简单地通过作为关键字参数（kw）传递来设置它们的 `coords` 属性。这是一个 Kivy 属性自动处理的小功能。

```python
from kivy.properties import (ListProperty, NumericProperty)
```

我们使用 `bind` 方法在每当 `GridEntry` 小组件触发 `on_release` 事件时调用 `button_pressed` 方法。每当用户释放 `GridEntry` 按钮时，这种操作会自动发生。我们还可以绑定到 `on_press`（在按钮首次被点击时触发），或者绑定到按钮的任何 Kivy 属性（当属性修改时动态触发）。

```python
class TicTacToeGrid(GridLayout):
    status = ListProperty((0, 0, 0, 0, 0, 0, 0))
    current_player = NumericProperty(1)
```

我们通过 `add_widget` 方法将每个 `GridEntry` 小组件添加到我们的 `Grid` 中。这意味着每一个都是 `TicTacToeGrid` 的子组件，因此它将...

这添加了一个状态列表来表示谁玩过棋，并给当前玩家分配了一个数字（1 代表 `O`，-1 代表 `X`）。

通过将这些放入我们的状态列表中，我们就能知道某行、某列或对角线的和是否为 +3，从而有人获胜。现在我们可以在进行移动时更新我们的图形网格。

# 使用 Python 创建

## 使用 Kivy 构建井井棋游戏

```python
def button_pressed(self, button):
    player = {'O': 'O', 'X': 'X'}
```

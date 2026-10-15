
现在我们显然再次这样做，只是它继承了 `GridLayout` 组件的行为，即我们需要告诉它它有多少列，但然后它将

Python 书籍

108

## 使用 Python 创建

![](img/3c5b3591dd9ac4cceb489cee11bd7908_108_0.png)

`kv` 语言带有所有需要的工具。

如之前所示，`kv` 语法定义了 `GridEntry` 组件应该如何构建，通过设置 `'font_size'` 属性来更改 `label` 中的文本。`Kivy` 自动处理这一点，它将链接到它并完美匹配。我们没有在 Python 中做此更改（而不是使用 `'bind'` 方法），而是通过引用 `kv` 语言中的属性。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_108_1.png)

井字游戏现在接受任何组件来适应 O 或 X，交替地管理尽可能多的行。井字-grid 需要一个简单的 `kv` 语言来制作规则。`Kivy` 给了我们做任何事情的权力，但这种权力伴随着编写 GUI 的困难。虽然你不需要 `kivy` 语言，你可以在 Python 中做相同的事情。当我们实例化 `'GridEntry'` 组件时，引入了新概念。我们通过简单地将其作为 `kwarg` 使用 `'coords'`。`Kivy` 带有所有需要的工具；简单的方法是在 `App` 类中编写它。我们将使用 `'bind'` 方法来捕捉 `grid` 的 `'button'` 方法，它在用户按下按钮时触发。然后 `'GridEntry'` 绑定到 `'bind'`，每当属性变化时它就会触发。

```python
from kivy.properties import ListProperty
```

这是 `TicTacToe` 的基本语法：

```kv
cols: 3
```

我们使用 `'add_widget'` 方法将 `'GridEntry'` 组件添加到我们的 `grid` 中。这就是它的工作方式，它将自动排列成列数为 3 的 `grid`。

```python
from kivy.properties import ListProperty, NumericProperty
```

`class Grid(ListProperty):`

这添加了表示谁玩过的 `status` 列表和一个表示当前玩家的整数（1 代表 X，-1 代表 O）。通过将这些放入 `status` 列表中，我们将谁在行、列或对角线上获胜。我们然后更新 `grid` 并显示胜利者。

你可以再次运行你的应用看看效果，并通过点击每个按钮更新 `status`，取决于该轮谁的操作。不仅如此，每个回合在移除现有标记后的移动移动都会更新我们的 `status`。

这个计划玩游戏，但缺少一个关键元素：一个在你获胜时显示的弹出窗口！我们需要添加一些代码来检查游戏是否结束。K 属性有其他有用的功能，它们会自动更改。如果需要，我们可以创建一个 `'on_status'` 方法并在 `Kivy` 事件系统中分发事件。编写在 Python 和 `kv` 语言中属性变化时触发的代码非常容易。我们可以利用此每次检查 `status` 列表。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_109_0.png)

带有添加的游戏，使 `grid` 变成方形并扩展界面，当玩家填充了行、列或对角线时执行特殊操作。

```python
def on_status(self, instance, value):
    self.status = value
```

- 对于每一行、每一列和对角线
可以很短，让我们看看发生了什么：

```python
sums = [
    (self.status[0]+self.status[1]+self.status[2]),
    (self.status[3]+self.status[4]+self.status[5]),
    (self.status[6]+self.status[7]+self.status[8]),
    (self.status[0]+self.status[3]+self.status[6]),
    (self.status[1]+self.status[4]+self.status[7]),
    (self.status[2]+self.status[5]+self.status[8]),
    (self.status[0]+self.status[4]+self.status[8]),
    (self.status[2]+self.status[4]+self.status[6])
]
```

# 如果一个玩家填满了线，和 可以为 -3

```python
if 3 in sums:
    print('X wins')
elif -3 in sums:
    print('O wins')
elif 0 not in self.status:
    print('Draw...')
```

这涵盖了获胜或平局的基础，但它只将结果呈现给 `stod`。我们可能想要重置网格以便玩家再次玩，显示结果的图形化指示（图 10）。

最后，我们可以使用 `on_status` 方法重置网格并在 `ModalView` 中显示胜利者。

```python
from kivy.modalview import ModalView
```

这是一个在组件树其他部分之外绘制自身的弹出窗口。当用户点击或点击退出时，它会自动关闭。

```python
winner =
if 3 in sums:
    winner = 'X'
elif -3 in sums:
    winner = 'O'
elif 0 not in self.status:
    winner = 'Draw'
```

```python
if winner:
    popup = ModalView(size_hint=(0.5, 0.5))
    victory_label = Label(text=winner)
```

Python 书 109

```python
def build(self):
    return TicTacToe()
    # Replaces the label
```

## 使用 Python 创建

```python
font_size=20
popup.popup(victory_label)
pop.bind(widget,on_destroy=self.reset)
pop.open()
```

## 尝试不同的组件类型以查看其他组件的行为

这大部分使用了我们已经涵盖的相同思路，只是在 `'ModalView'` 窗口中添加了 `'Label'` 组件的使用，然后通过另一个属性 `on_destroy` 让它在所有内容之上处理其自身和子元素，`on_destroy` 是 `'ModalView'` 在关闭时触发的事件。最后，在这种情况下，我们在组件上使用了 `size_hint` 属性，这使得 `'ModalView'` 的大小与窗口成比例——而对于 `'ModalView'`，你可以调整窗口大小以并看到它是如何保持这些属性的。通过与 `size_hint` 属性绑定实现的另一个技巧是在内部管理的。

![](img/3c5b3591dd9ac4cceb489cee11bd7908_110_0.png)

```python
class TicTacToeGrid(Grid,layout):
    def __init__(self, *args, **kwargs):
        super(TicTacToeGrid, self).__init__(*args, **kwargs)
        for row in range(3):
            for col in range(3):
                grid_entry = GridEntry(coords=(row, col))
```

这是一个完成的程序！我们现在只能玩打字游戏，但我们的程序会自动告诉我们谁赢了，并重置棋盘再次游戏。只需运行你的程序并享受数小时的乐趣！

```python
def button_pressed(self, instance):
    # 打印输出以查看发生了什么
    print("{} clicked!".format(instance.coords))
```

## 实验时间

这是对 `Kivy` 某些功能的快速浏览，但它展示了如何思考构建一个 `Kivy` 应用程序。我们的程序构建在单个事件之上，当我们使用 `'on_status'` 或当它们改变时（`on_release`）时，通过绑定 `Kivy` 属性规则来相互交互。我们将简要跳过 `Kivy`，体验它是如何自动在属性之间创建绑定的。

```python
def button_pressed(self, button):
    # 创建标签和颜色
    player = {'O': 'X', 'X': 'O'}
    colors = {'O': (0, 0, 1), 'X': (0, 1, 0), (r, g, b)}
```

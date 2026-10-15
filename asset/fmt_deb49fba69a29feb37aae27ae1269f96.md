
# 使用 Python 开发 Web 应用

# 介绍 Python

查看管理员站点源代码

它是

| 问题 (Issue) | 描述 (Description) | 状态 (Status) | 所有者 (Owner) |
| --- | --- | --- | --- |
| 1 | 有一个问题 | 新 | ana |
| 2 | 网络未连接 | 已接受 | mars |
| 3 | 银河系有些 | 已开始 | ludfisher |
| 4 | 今天移动 | 已开始 | dumb |
| 5 | 有三个缺失 | 已开始 | ludfisher |

```html
<table class="options">
  <tr>
    <td>问题 (Issue)</td>
    <td>描述 (Description)</td>
    <td>状态 (Status)</td>
    <td>所有者 (Owner)</td>
  </tr>
  {% for issue in info.queryset %}
  <tr>
    <td>{{ issue.id }}</td>
    <td>{{ issue.description }}</td>
    <td>{{ issue.status }}</td>
    <td>{{ issue.owner }}</td>
  </tr>
  {% endfor %}
</table>
```

```html
<div id="content">
  {%block block %}
  {% endblock %}
</div>
```

## 使用 Python 为 Android 构建应用

整个游戏。我们专门创建了 `FloatLayout` 的一个子类，因为这种布局能够根据其自身的位置和大小，对其子元素进行定位和缩放——无论我们在哪里运行它，或者如何调整窗口大小，它都能相应地填充所有的游戏对象。

组件画布（widget canvases），我们在这里用它们来绘制每个组件形状：

介绍可以设置的不同 Python 属性，即矩形的 `pos` 和 `size`，你可以在线查看 Kivy 文档以获取所有可能性。最大的优势在于，虽然我们仍然声明了简单的画布指令，但 `kv` 语言可以检测到我们引用了哪些 Kivy 属性并自动跟踪它们；当这些属性更新时（组件移动或调整大小），画布指令也会随之移动！

```kv
<Player>
canvas:
    Color:
        rgba: 1, 1, 1, 1
```

```kv
Rectangle:
    pos:self.pos
    size:self.size
```

接下来，我们可以使用 Kivy 的图形指令在我们的组件上绘制各种形状。我们将演示如何将一个简单的矩形移动到它们的位置，你可能还喜欢研究更多高级选项。在 Python 文件中，我们可以通过在任何组件的画布上声明它来找到任何指令，如图 03 所示。这将绘制一个在实例化时与玩家具有相同位置和大小的红色矩形——遗憾的是，这产生了一个问题，因为绘制是静态的。当我们以后移动玩家组件时，红色矩形将留在原地，而组件在处于其正确位置时将是不可见的。

```kv
<Base>
canvas:
    Color:
        rgb: 1, 0.55, 0
```

```kv
Rectangle:
    pos:self.pos
    size:self.size
```

图 01

```python
evenfrom kivy.app import App
from kivy.uix.widget import Widget
from kivy.uix.floatlayout import FloatLayout
from kivy.uix.modalview import ModalView
```

```python
## 我们在上面预定义的属性
Rectangle:
    pos:self.pos
    size:self.size
Color:
    rgb: 0.1, 0.1, 0.1
rectangle:
    [self.x,self.y,self.width,self.height]
```

```python
__init__ = '0.1' # 后用于 Android 编译
```

```python
class BreakoutApp(App):
    pass
```

```python
BreakoutApp.run()
```

我们可以通过保留画布指令的引用并反复更新它们的属性来跟踪玩家从而修复这个问题，但有一种更简单的方法可以完成这一切——我们可以使用上次介绍的 Kivy 语言。它在绘图上有一种特殊的语法。

画布声明是特殊的，尽管我们可以随所欲地编写任何画布指令。不要混淆，画布不是一个组件，也不是像 `Line` 那样的图形指令。这是画布特有的特殊语法。所有指令都具有

图 02

```python
from kivy.properties
import(ListProperty,
        NumericProperty,
        ObjectProperty,
        StringProperty)
```

![](img/f16311c48f0c39ab87b1836be5339b9e_32_0.png)

## 介绍 Python

## 使用 Python 为 Android 构建应用

```python
class Game(FloatLayout):
    def __init__(self, **kwargs):
        # 将包含一切
        jump, 'y': 0.05 + 0.09*y
        blocks = ListProperty([])
        super(Player, self).__init__(**kwargs)
        player = ObjectProperty()
        jump())
        self.__init__(*kwargs) ## 游戏的实例 append(block)
        ball = ObjectProperty() with self. self.add_
        游戏的 Ball 实例 canvas: Color(1, 0, 1) widget(block)
```

```python
class Player(Widget): # A
    moving padding
    position = = NumericProperty(0.5)
    direction = = StringProperty('none')
    class Ball(Widget): # A
        bouncing ball
        # pos_hints 用于
        按比例定位，
        # 见下文
        pos_hint_x = NumericProperty(0.3)
        pos_hint_y = 
        proper_size = NumericProperty(0.8)
        velocity = = ListProperty([0.1, 0.5])
        class Block(Widget): #
            每个块去
            销
            colour = ListProperty([1, 0, 0])
```

![](img/f16311c48f0c39ab87b1836be5339b9e_33_0.png)

你可能注意到我们有一个 `Block` 的一个 'Color' 指令来清空属性。这意味着我们可以随时更改该属性来更新块的颜色，或者在这种情况下，给每个块赋予随机颜色（图 04）。在这里，我们创建了想要添加的组件并使用 `add_widget` 将它们添加到图形中。屏幕上的根组件是 `Game` 的实例，每个块都被添加以显示。其中唯一的新奇点是每个 `Block` 都被赋予了一个 `pos_hint`。它具有这种特殊属性，并被像我们的 `Game` 这样的 `FloatLayout` 使用，以相对于宽度和高度设置它们的位置。你现在可以运行应用了，你会发现它们的大小没有手动设置，所以它们重叠了。我们可以通过设置它们的属性来修复这个问题。

```python
class Game(FloatLayout):
    def setup_blocks(self):
        for i in range(10):
            block = Block(pos_hint={'x': random.random(), 'y': random.random()})
```

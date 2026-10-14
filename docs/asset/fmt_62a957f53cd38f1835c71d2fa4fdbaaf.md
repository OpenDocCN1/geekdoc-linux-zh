
`g = Game()`

`g.setup_blocks()`

`return g`

在这里我们创建了需要的组件并将其 `add_widget` 到图形根节点上。我们在屏幕上的根组件是 `Game` 的实例，它被添加到窗口中。

新之处是每个色块都被赋予了 `pos_hint`，这里是我们处理这个特殊属性的方法，它被 `FloatLayout` 使用：像 `Game` 一样，我们将它们的位置设置为布局。

字典用于处理各种参数，但在情况下，'x' 和 'y' 是相对于父容器宽度和的高度。

你现在可以运行应用了，它会在启动前进入 `Game`。屏幕将显示三种可能的碰撞模式之一，在发布后，你会注意到它们都重叠了。

这处理了所有游戏组件在布局中的定位和大小问题。`Ball`（球）和 `Player`（玩家）将使用我们设置的属性，因此只需设置三个属性并让布局自动更新位置就能移动它们。

这还使用了一个额外的属性来保持圆形而不是矩形，因为另一种方案可能会看起来有点奇怪。

我们几乎已经完成了应用图形的最终细节！

你现在可以再次运行游戏了，并能看到所有图形每秒都在工作，更新碰撞情况。还没有东西在移动，除了 `FloatLayout`：如果你缩放游戏/窗口大小，一切都应该保持比例。

现在我们必须添加机制。对于像这样的游戏，我们希望每秒运行多次，更新组件位置并执行与球的碰撞（图 05）。

`Clock` 可以按间隔一次性或重复地调度任何函数。一个函数更新自其上次调用以来的时间 `dt`，我们通过在语言中创建的事件将 `dt` 传递给 `Ball` 和 `Player`。

到此时，我们已经添加了处理键盘输入的第一步，通过按下窗口在每次按键时调用 `Player` 的方法。然后我们可以通过添加触摸/鼠标输入添加此按键处理程序来关闭 `Player` 类。

```python
class Player(Widget):
    def on_down(self, touch):
        self.direction = 'right' if touch.x > self.parent.width/2 else 'left'
        self.center_x =
```

```python
class Ball(Widget):
    def on_down(self, touch):
        self.direction = 'none'
```

```python
def on_key_down(self, key, keyargs):
    if key == 'right':
        self.direction = 'right'
    elif key == 'left':
        self.direction = 'left'
    self.direction = 'none'
```

```python
def update(self, dt):
    self.dir_dict = {'right': 1, 'left': -1}
```

图 04

```python
'none': None
self.position += 0.5 * dt * dir_dict[self.direction]()
```

```python
import random
```

这些 `on_touch` 处理程序是 Kivy 处理触摸或鼠标输入的方法，它们在检测到输入时自动调用，你可以根据需要执行任何操作。在这种情况下，我们将 `Player` 的 `direction` 属性设置为键盘或触摸输入，并在调用 `update` 方法时使用此来移动玩家。我们也可以为球添加报告。

```python
class Block(Widget):
    def __init__(self, **kwargs):
        super(Block, self).__init__(**kwargs)
        self.color = random.choice([
            (0.75, 0.25, 0.2), (0.28, 0.63, 0.28), (0.25, 0.28, 0.70)
        ])
```

图 05

球通过强制速度指向背挡板的方向来从每面墙反弹——如果它击中挡板，还会带有额外的推力反弹。它还处理与色块的任何碰撞或任何胜/负条件，但在球击中玩家身体时会尝试拦截游戏。

```kviv
<Player:
    size_hint: 0.0, 0.05
    # canvas 部分
```

这应该处理失败的情况，显示一个带有消息和重试按钮的弹出窗口。最后，我们应该在球击中色块时销毁它们。

```kviv
<Ball:
    size_hint: 0.1, 0.125
    pos_hint: {'x': self.position.x, 'y': self.position.y}
    size_hint: None
    size: self.parent.width, 0.3*self.parent.width
    # canvas 部分
```

```python
from kivy.clock import Clock
from kivy.core.window import Window
from kivy.utils import platform
```

这涵盖了所有最后的条件，通过比较位置和大小与 Kivy 内置的 `collide_widget` 方法进行碰撞。方向将取决于球如何穿透，因此我们将告诉它如何修复。所以这里，你可以调用 `run()` 来玩你的简单游戏。现在它非常简单，但希望你可以为行为添加许多其他细节，甚至是一个带有菜单和设置的完整游戏界面。

```python
class Game(Layout):
    def update(self, dt):
        self.ball.update(dt)
        self.player.update(dt)
```

我们只是在展示一段你可以为 Android 制作游戏的代码？Kivy 可以接收任何应用并将其转换为在 Android 上运行的 Android 应用。然而，Kivy 可以访问 Android 的功能。

```python
def stop(self):
    Clock.unschedule(update)
```

这处理了所有最后的情况，通过与 Kivy 内置的 `collide_widget` 方法比较位置和大小进行碰撞。方向将取决于球如何穿透，因此我们将告诉它如何修复。所以这里，你可以调用 `run()` 来玩你的简单游戏。现在它非常简单，但希望你可以为行为添加许多其他细节，甚至是一个带有菜单和设置的完整游戏界面。

```python
class Game(Layout):
    def update(self, dt):
        self.ball.update(dt)
        self.player.update(dt)
```

我们只是在展示一段你可以为 Android 制作游戏的代码？Kivy 可以接收任何应用并将其转换为在 Android 上运行的 Android 应用。然而，Kivy 可以访问 Android 的功能。

```python
def stop(self):
    Clock.unschedule(update)
```

## 将您的 APK 放到 Play 商店

了解如何对发布版 APK 进行数字签名并将其上传到您选择的应用商店

- 构建并签名您的密钥
- 首先我们需要创建一个数字密钥，然后使用命令对您特殊的 Android 发布版本进行数字签名，并按照它们提供的说明进行操作。
- 创建自己的数字密钥
- 您可以选择自己的名称，而不是密码。
- 使用 keystore，例如 `keystore-release.keystore`
- `--alias test-alias --keyalg RSA`
- 以发布模式编译您的应用
- `build android release`
- 使用您的新密钥签名 APK
- `SHA1DIGEST_SHA1`
- `--keystore keystore-release.keystore --alias test-alias --unsigned-apk.apk`
- 对 APK 压缩文件进行对
- `--build-path /path/to/build/android/ --sdk-v2/tools/zipalign -v 4 -f /bin/Kivydebug-0.1-release.apk /bin/Kivydebug-0.1-release.apk`

```python
self.parent.do_layout()
self.parent.destroy_blocks(self)
class Game(BoxLayout):
```

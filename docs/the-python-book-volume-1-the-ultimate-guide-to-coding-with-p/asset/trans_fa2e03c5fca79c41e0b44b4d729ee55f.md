

```python
class Ball(Widget):
    def update(self, dt):
        self.pos_hint_x += self.velocity[0] * dt
        self.pos_hint_y += self.velocity[1] * dt
        if self.right > self.parent.right:  # Bounce from right
            self.velocity[0] = -1 * abs(self.velocity[0])
        if self.x < self.parent.x:  # Bounce from left
            self.velocity[0] = abs(self.velocity[0])
        if self.top > self.parent.top:  # Bounce from top
            self.velocity[1] = -1 * abs(self.velocity[1])
        if self.y < self.parent.y:  # Lose at bottom
            self.parent.lose()  # Not implemented yet
        self.bounce_from_player(self.parent.player)

    def bounce_from_player(self, player):
        if self.collide_widget(player):
            self.velocity[1] = abs(self.velocity[1])
            self.velocity[0] += (
                0.1 * ((self.center_x - player.center_x) /
                       player.width))
```

```python
class GameEndPopup(ModalView):
    message = StringProperty()
    game = ObjectProperty()

class Game(Widget):
    def lose(self):
        self.stop()
        GameEndPopup(message='[color=#ff0000]You lose![/color]',
                     game=self).open()

    def win(self):  # Not called yet, but we'll need it later
        self.stop()
        GameEndPopup(message='[color=#00ff00]You win![/color]',
                     game=self).open()
```

```python
<GameEndPopup>:
    size_hint: 0.8, 0.8
    auto_dismiss: False  # Don't close if player clicks outside
    BoxLayout:
        orientation: 'vertical'
        Label:
            text: root.message
            font_size: 60
            markup: True
            halign: 'center'
        Button:
            size_hint_y: None
            height: sp(80)
            text: 'Play again?'
            font_size: 60
            on_release: root.game.start(); root.dismiss()
```

这里你需要一些基础依赖，可以很轻松地通过发行版的常规仓库安装。主要需要的是 OpenJDK7、zlib、最新版的 Cython 以及 Git。如果你使用的是 64 位发行版，你还需要 zlib、libstdc++ 以及 libgcc 的 32 位兼容库。然后你可以继续下载并安装 buildozer：

```bash
git clone git://github.com/kivy/buildozer
cd buildozer
sudo python2.7 setup.py install
```

完成这部分后，你就可以进入你的 Kivy 应用目录，并需要将主代码文件命名为 ‘main.py’，这是 Android APK 所期望的入口点。然后：

```bash
buildozer init
```

这会创建一个 ‘buildozer.spec’ 文件，一个包含 Buildozer 创建 APK 所需所有信息的设置文件，从名称和版本到特定的 Android 构建选项。我们建议你浏览整个文件以了解有哪些可用选项，但大多数默认设置都很好，我们建议更改的唯一地方是（图 11）。还有各种其他选项你经常会想要设置，但目前都不是特别关键，所以你可以立即让 Buildozer 构建你的 APK 并开始使用！

```bash
buildozer android debug
```

这需要一些时间，所以请耐心等待，它会顺利完成。第一次运行时，它会下载 Android SDK 和 NDK，这两者都很大（至少数百兆字节），但对构建至关重要。它也需要时间来构建这些并编译 APK 的 Python 组件。其中很多只需要做一次，以后如果你更改 buildozer.spec，重建需要几分钟；如果你只更改了代码，则只需要几秒钟。

生成的 APK 是一个调试版 APK，你可以安装并使用它，但如果你想完全数字签名以便发布到 Play 商店，则需要额外步骤。这并不难，Buildozer 可以完成部分工作，但你可以在线查看文档以获取完整细节。

假设一切顺利（应该会！），你的 Android APK 将位于新创建的 'bin' 目录中，名称为 'KivyBreakout-0.1-debug.apk'。你可以用任何方式将其发送到手机（例如邮件），不过在安装前你可能需要在设置中启用从未知来源安装应用程序。


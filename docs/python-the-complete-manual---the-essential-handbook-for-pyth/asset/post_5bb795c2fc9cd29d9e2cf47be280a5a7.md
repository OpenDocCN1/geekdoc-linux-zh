
# Introducing Python

## Build an app for Android with Python

ball hits the bottom of the player screen, so let's now add some game end code to handle all of this (Fig. 08). And add the code in Fig. 09 to 'breakout.py'. This should fully handle the loss or win, providing a pop-up message with an appropriate message and providing a button to try again. Finally, we have to handle destroying balls when the ball hits them (Fig. 10).

This fully covers all last conditions, checking collision via kivy's `build_collide_method` that compares their bounding boxes (pos and size). The bounce will depend on how far the ball has penetrated, as we will tell it hit with the Block.

So there you have, you can run the code to play your simple Breakout. It's very simple right now, but hopefully you can see of different ways to add extra behaviour to types of blocks and power-ups—you could add a lives system, more sophisticated paddle/ball interaction, or build a full game interface with a menu and settings screen.

We're just finishing showing one cool thing that you can do—compile your game for Android! Generally speaking taking any Kivy app and turn it into an Android APK that will run on any of your Android devices. You can even access the normal Android API to access hardware or OS features such as vibration, sensors or native notifications.

We'll build Android using the Buildtool, and a Kivy sister project wrapping other build tools to create different systems. This takes care of downloading and running the Android build tools (SDK, NDK, and Kivy's Python-for-android) to create the APK.

```python
size_hint: None, None
proper_size: min(3*self.parent.height,3*self.parent.width)
size: self.proper_size,self.proper_size
# canvas part
```

Fig 06

```python
from kivy.clock import Clock
from kivy.core.window import Window
from kivy.utils import platform
```

```python
class Game(FloatLayout):
    def update(self, dt):
        self.ball.update(dt) # Not defined yet
        self.player.update(dt) # Not defined yet
```

Fig 04

```python
import random

class Ball(Widget):
    def __init__(self,**kwargs):
        super(Ball,self).__init__(**kwargs)
        self.colour = random.choice((0.78,0.63,0.28),(0.25,0))
    def start(self,*args):
        Clock.schedule_interval(self.update, 1./60.)
```

Fig 05

```kvivy
<Widget>:
    size_hint: 0.09, 0.05
    # canvas part
<Player>:
    size_hint: 0.1, 0.25
    position: {'x': self.position,'y': 0.1}
    # canvas part
<Ball>:
    size_hint: {'x': self.pos_hint_x,'y': self.pos_hint_y}
```

```python
def reset(self):
    for block in self.blocks:
        self.remove_widget(block)
    self.blocks = []
    self.setup_()
    self.ball.velocity = [random.random(),0.5]
    self.player.position = 0.5
```

```python
class BreakoutApp(App):
    def build(self):
```

![](img/c72194f2c3aec198936695a665a5167c_35_0.png)

# Build an app for Android with Python

# Introducing Python

Fig 09

```python
g = Game()
if platform() != 'android':
    Window.bind(on_key_down=g.player.on_key_down)
    if self:
        Window.bind(on_key_up=g.player.on_key_up)
Clock.once(g.start, 0)
return g

def bounce_from_player(self, player):
    self.velocity[0] *= -0.1 * (self.center_x - player.width)/2
```

```kvivy
<GameEndPopup>:
    size_hint: 0.8, 0.8
    auto_dismiss: False
    # Don't close if player clicks out
    BoxLayout:
        orientation: 'vertical'
        Label:
            text: root.message
```

![](img/c72194f2c3aec198936695a665a5167c_36_0.png)

```python
class Ball(Widget):
    def update(self, dt):
        self.pos_hint_x += self.velocity[0] * dt
        self.pos_hint_y += self.velocity[1] * dt
        if self.right > parent.width: # Bounce from right
            self.velocity[0] = -1 * abs(self.velocity[0])
        if self.x < parent.x: # Bounce from left
            self.velocity[0] = 1 * abs(self.velocity[0])
        if self.top > parent.top: # Bounce from top
            self.velocity[1] = -1 * abs(self.velocity[1])
        if self.y < parent.y: # Bounce at bottom
            self.velocity[1] = 1 * abs(self.velocity[1])
        # Not implemented yet
        self.bounce_from_player(self,parent.player)
```

![](img/c72194f2c3aec198936695a665a5167c_36_1.png)

```python
class GameEndPopup(ModalView):
    message = StringProperty()
    game = ObjectProperty()
```

```kvivy
'center':
Button:
    size_hint: None
    height: 60
    markup: True
    halign: 'center'
    text: 'Play again?'
```

```python
class Game(Widget):
    def stop(self):
        self.stop_game()
    popup = GameEndPopup(
        message=['color=#ff0000]You lose![/color]'],
        game=self)
    popup.open()
```

Here you will need base dependencies, which can be installed with ease by using your normal repositories. The main ones to use are OpenJDK, Cython, and zlib, as you need them to build the APK.

```python
class Ball(Widget):
    def update(self, dt):
        self.pos_hint_x += self.velocity[0] * dt
        self.pos_hint_y += self.velocity[1] * dt
        if self.right > parent.width: # Bounce from right
            self.velocity[0] = -1 * abs(self.velocity[0])
        if self.x < parent.x: # Bounce from left
            self.velocity[0] = 1 * abs(self.velocity[0])
        if self.top > parent.top: # Bounce from top
            self.velocity[1] = -1 * abs(self.velocity[1])
        if self.y < parent.y: # Bounce at bottom
            self.velocity[1] = 1 * abs(self.velocity[1])
        # Not implemented yet
        self.bounce_from_player(self,parent.player)
```

```python
class GameEndPopup(ModalView):
    message = StringProperty()
    game = ObjectProperty()
```

```kvivy
'center':
Button:
    size_hint: None
    height: 60
    markup: True
    halign: 'center'
    text: 'Play again?'
```

```python
class Game(Widget):
    def stop(self):
        self.stop_game()
    popup = GameEndPopup(
        message=['color=#ff0000]You lose![/color]'],
        game=self)
    popup.open()
```

# Introducing Python

## Build an app for Android with Python

To sign your APK, you will need a digital key. You can create one using `keytool`:

```bash
keytool -genkey -v -keystore release.keystore -alias release -keysize 2048 -validity 10000 -type RSA
```

Once you have the key, you can sign the APK using `jarsigner`:

```bash
jarsigner -v -keystore release.keystore -alias release release.apk-signed
```

Finally, you must align the APK using `zipalign`:

```bash
zipalign -v -4 4 release.apk-signed release-aligned.apk
```

Then you can use `buildozer` to build your project:

```bash
buildozer android debug
```

This takes care of downloading and running the Android build tools (SDK, NDK, and Kivy's Python-for-android) to create the APK.

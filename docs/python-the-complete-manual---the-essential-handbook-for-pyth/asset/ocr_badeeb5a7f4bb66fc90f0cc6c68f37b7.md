# Introducing Python

# Build an app for Android with Python

ball hits the bottom of the player screen, so let's now add some game end code to handle all of this (Fig. 08). And add the code in Fig. 09 to 'breakout.file'.nThis should fully handle the loss or win, providing a pop-up message with an appropriate message and providing a button to try again. Finally, we have to handle destroying balls when the ball hits them (Fig. 10).
This fully covers all last conditions, checking collision via kivy's build_collide_method that compares their bounding boxes (pos and size). The bounce will depend on how far the ball has penetrated, as we will tell it hit with the Block.
So there you have, you can run the code to play your simple Breakout. It's very simple right now, but hopefully you can see of different ways to add extra behaviour to types of blocks and power—you could add a lives system, more sophisticated paddle/ball interaction, or build a full game interface with a menu and settings screen.
We're just finishing showing one cool thing that you can do—compile your game for Android! Generally speaking taking any Kivy app and turn it into an Android APK that will run on

of your Android devices. You can even access the normal Android API to access hardware or OS features such as vibration, sensors or native notifications.
We'll build Android using the Buildtool, and a Kivy sister project wrapping other to build tools to create different systems. This takes care of downloading and running the Android build tools (SDK, NDK, and Kivy's Python-for create the APK.

```
size_hint: None, None proper_size:
min(03*self.parent.height,03*self.parent.width)
size: self.proper_size,self.proper_size
# canvas part
```

Fig 06

```
from kivy.clock import
from kivy.core.window
from kivy.utils import platform
```

class Game(FloatLayout):

```
def update(self, dt):
self.ball.
update(dt) # Not defined yet
self.player.
update(dt) # Not defined yet
```

Fig 04

import random

```
class Ball(Widget):
def __init__(self,**kwargs):
super(Ball,self).__init__(**kwargs)
self.colour = random.choice((0.78,0.63,0.28),(0.25,0))
def start(self,*args):
Clock.schedule_ninterval(self.update,1.60).
```

Fig 05

```
<Widget>nsize_hint: 0.09, 0.05
# canvas part
<Player>nsize_hint: 0.1, 0.25
position: {'x': self.position,'y': 0.1}
# canvas part
<Ball>
size_hint: {'x': self.pos_hint_x,'y': self.pos_hint_y}
```

```
def reset(self):
 block in self.blocks:
self.remove_widget(block)
self.blocks = []
self.setup_
self.ball.velocity = [random.random(),0.5]
self.player.position = 0.5
```

```
class BreakoutApp(App):
def build(self):
```

![](bbox=[0.295, 0.923, 0.335, 0.963])
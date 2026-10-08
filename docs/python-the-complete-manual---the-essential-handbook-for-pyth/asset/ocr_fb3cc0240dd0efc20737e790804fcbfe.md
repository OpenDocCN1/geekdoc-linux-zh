# Build an app for Android with Python

# Introducing Python

Fig 09

```
g = Game()
if platform() != 'android':
    def bounce_
from_player(self, player):
        Window.
        bind(on_key_down=g.player.on_key_down)
        if self:
            bind(on_key_up=g.player.on_key_up)
            Window.
            velocity[1] = abs(self.velocity[1])
            g.reset()
Clock.once(g.start, 0)
        return g
        self.
velocity[0] *= -0.1 * (self.center_x - player.width)/2
```

```
<GameEndPopup>
size_height: 0.8, 0.8
auto_dismiss: False
# Don't close if playernclicks out
BoxLayout:
orientation:
'vertical':
Label:
text: root:
```

![](bbox=[0.105, 0.354, 0.355, 0.414])

```
class Ball(Widget)
    update(self, dt):
        self.pos_hint_x += self.velocity[0] * dt
        self.pos_hint_y += self.velocity[1] * dt
        if self.right > parent.width: # Bounce from right
            self.
velocity[0] = -1 * abs(self.velocity[0])
        if self.x < parent.x: # Bounce from left
            self.
velocity[0] = 1 * abs(self.velocity[0])
        if self.top > parent.top: # Bounce from top
            self.
velocity[1] = -1 * abs(self.velocity[1])
        if self.y < parent.y: # Bounce at bottom
            self.
velocity[1] = 1 * abs(self.velocity[1])
        # Not implemented yet
self.bounce_from_player(self,parent.player)
```

![](bbox=[0.375, 0.424, 0.625, 0.484])

```
c l a s
GameEndPopup(ModalView):
    message =
StringProperty()
    game =
ObjectProperty()
```

```
'center':
Button:
size_height:
height: 60
markup:
halign:
'again?':
_size:
text: 'Play'
```

```
class Game(Widget):
    def stop(self):
        self.stop()
GameEndPopup(
    message=['color=#ff0000]You
lose![/color]'],
    game=self.open())
```

Here you will need
base dependencies, which
can be installed with ease
by using your's normal
repositories. The main ones to use
are OpenJDK,7lib, the up-to-date
Cython, and if you are using
a64-bit binary you need
libraries for zlib, libc++, as
alibgc. You can then go out and
download and install Builderz:

```
def win(self):
    Not called yet, but we'll
need it later
    self.stop()
    GameEndPopup(
        message=['color=#ff0000]You
win![/color]'],
        game=self.open())
```

```python
if (pyxel.frame, count + self.offset) > 60 < 30:
    self.x += ENEMY_SPEED
    self.dir = 1
else:
    self.x -= ENEMY_SPEED
    self.dir = -1

self.y += ENEMY_SPEED

if self.y > pyxel.height - 1:
    self.alive = False
```

```python
def draw(self):
    pyxel.rect(self.x, self.y, 0, 8, 0, self.dir, self.h)
# 这一系列类最后一个，用于绘制标题和我们的玩家：
class Blast:
    def __init__(self, x):
        self.x = x
        self.y = y
        self.radius = BLAST_START_RADIUS
        self.alive = True
```

```python
def update(self):
    self.radius += 1

if self.radius > BLAST_END_RADIUS:
    pyxel.circle(self.x, self.y, self.radius, BLAST_COLOR, IN)
    pyxel.circle(self.x, self.y, self.radius, BLAST_OUT, OUT)
```

这些就是我们设置的所有游戏元素，现在我们可以使用 `pyxel` 模块开始编写应用程序窗口了。教程中的其余代码功能将在后续介绍，让我们创建这个类：

```python
class App:
    def __init__(self):
        pyxel.init(120, 160, caption='Shooter Game')
        # 当然，我们可以创建任何喜欢的内容，这些内容将出现在我们游戏窗口的标题中。
```

我们将使用 `pyxel` 图像集来创建我们的精灵：

```python
pyxel.image(0).set(
    0,
    0,
    "00088000",
    "00ee1200",
    "08b2b180",
    "02882820",
    "00222200",
    "0012d2d0",
    "02080000",
    "80008000",
)
```

击杀丑陋的外星会导致爆炸。

![](img/2f8aba538b6f14f57de8cb694470acb2_73_0.png)

```python
pyxel.image(0).set(
    8,
    B
)
```

声音也是如此：

`pyxel.sound(0).set("a3a2c4a","p","7","s","s","10")`

图像集和声音完全自定义自定义，需要对 `pyxel` 游戏引擎进行进一步实验。

## 背景信息

```python
# 设置场景并绘制背景以及我们的玩家：
self.scene = TITLE
self.score = 0
self.background = Background(0)
self.player = Player(pyxel.width/2)
```

```python
pyxel.run(self.update, self.draw)
# 这将更新 - 我们绘制到屏幕上的所有内容 - 以确保玩家在变化时看到最新版本：
def update(self):
    if pyxel.btn(pyxel.KEY_Q):
        self.player.quit()
    self.background.update()
    if self.scene == TITLE:
        self.update_title()
    elif self.scene == ENEMY:
        self.update_enemy()
    elif self.scene == GAMEOVER:
        self.update_gameover()
    self.score += 1
```

更新标题函数非常简单：

```python
def update_title(self):
    if pyxel.btn(pyxel.KEY_ENTER):
        self.scene = PLAY
```

另一方面，更新主游戏内容稍微复杂一些：

```python
def update_play(self):
    if pyxel.frame % 6 == 0:
        enemy.random(pyxel.width - WIDTH)
    for b in bullet_list:
        if (a.x + a.w > b.x and a.x < b.x + b.w and a.y + a.h > b.y and a.y < b.y + b.h):
            a.alive = False
            bullet_list.append(Blast(a.x + ENEMY_WIDTH/2, a.y))
    player.pixel(1,1)
    self.score += 10
    for enemy in enemy_list:
        if player.x + player.w > enemy.x and player.x < enemy.x + enemy.w
```

# 编写一个太空侵陆者 CODING ACADEMY

![](img/2f8aba538b6f14f57de8cb694470acb2_74_0.png)

最后，我们需要编写绘制函数。绘制它们很容易，可以保持简单，所以这些是程序中最短的函数：

```python
def draw(self):
    pixel.cls(0)
```

```python
self.background.draw()
```

```python
if self.scene == SCENE_TITLE:
    self.draw_title(scene)
elif self.scene == SCENE_PLAY:
    self.draw_play(scene)
elif self.scene == SCENE_GAMEOVER:
    self.draw_gameover()
```

```python
pixel.text(39, 4, "SCORE (%d)", self.score, 7)
```

我们还需要绘制标题、播放场景和“游戏结束”：

```python
def draw_title_scene(self):
    pixel.text(35, 66, "Start Shooter", pyxel.frame % 10)
```

这是显示在屏幕上的文本，但我们可以更改文本以适应：“Shooter - Press Enter to go”。例如，最后的函数产生子弹、敌人和爆炸用于游戏和游戏结束：Pyxel 详细介绍了如何使用游戏引擎。参考 https://github.com/kita/pyxel

```python
def draw_gameover(self):
    self.draw(bullet_list)
    self.draw(enemy_list)
    self.draw(blast_list)
    self.draw(bullet_list)
    self.draw(enemy_list)
```

最后，游戏结束界面的文本再次进行了自定义：

```python
pixel.text(43, 66, "GAME OVER", 8)
pixel.text(126, 106, "PRESS ENTER", 13)
```

这是确保此处缩进的最后一行。此外，使用的 `App` 类正在运行和关闭。现在按 F5 保存我们的程序，如果你想计划，应该有一个复古射击游戏。使用方向键射击那些讨厌的...

![](img/2f8aba538b6f14f57de8cb694470acb2_74_1.png)

```python
and self.player.y + h == enemy and enemy.y > self.player.y:
    enemy.alive = False
```

```python
list.append(Blast(self.player.x + WIDTH / 2, self.player.y + HEIGHT / 2))
    pixel.play(1, 1)
```

```python
cleanup(enemy_list)
cleanup(bullet_list)
cleanup(blast_list)
```

发生了很多事情。我们按比例生成敌人，在它们被销毁时创建爆炸，并创建精灵（资源）当它们不再时。我们需要更新我们的游戏结束场景：

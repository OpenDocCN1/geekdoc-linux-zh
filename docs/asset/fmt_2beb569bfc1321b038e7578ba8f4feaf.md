
在初始化时，我们使用循环和`random`模块随机化星星星的位置，并将它们添加到星星星列表中。

我们还添加了函数来更新背景中的星星星。

# 玩家一游戏类

接下来我们需要引入我们的玩家角色：

```python
class Player:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.w = PLAYER_WIDTH
        self.h = PLAYER_HEIGHT
        self.alive = True
```

```python
    def update(self):
        if pyxel.btn(pyxel.KEY_LEFT):
            self.x -= PLAYER_SPEED

        if pyxel.btn(pyxel.KEY_RIGHT):
            self.x += PLAYER_SPEED

        if pyxel.btn(pyxel.KEY_UP):
            self.y -= PLAYER_SPEED

        if pyxel.btn(pyxel.KEY_DOWN):
            self.y += PLAYER_SPEED
            self.x = min(self.x, pyxel.width - self.w)
            self.x = max(self.x, 0)
            self.y = min(self.y, pyxel.height - self.h)
```

## 小贴士

你可以为你的射击游戏创建一个独立的可执行版本。运行`pyxel install pntylaster`获取依赖项，排序，然后使用`pyxel-shooter`来运行它。

```python
    if pyxel.btn(pyxel.KEY_SPACE):
        Bullet(
            self.x + PLAYER_WIDTH - BULLET_WIDTH/2,
            self.y
        )
```

```python
    def draw(self):
        pyxel.rect(self.x, self.y, 0, 0, 0, self.w, self.h)
```

在初始化时设置`x`和`y`坐标。我们从之前设置的全局变量中获取宽度和高度，重要的是，我们决定玩家角色初始为存活状态。与其他类一样，我们设置了一个函数来绘制和更新我们的玩家角色。当更新按键被按下时，它是我们在开始时决定的速度基础上的。

已经准备好了，让我们在玩家类中为游戏设置好子弹：

```python
class Bullet:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.w = BULLET_WIDTH
        self.h = BULLET_HEIGHT
        self.alive = True
```

```python
    def update(self):
        self.y -= BULLET_SPEED

        if self.y + pyxel.height < 0:
            self.alive = False
```

```python
    def draw(self):
        pyxel.rect(self.x, self.y, 0, 0, 0, self.w, self.h)
```

我们需要一个敌人类，使用面向对象编程方法的妙处在于，我们可以实例化多个相同事物的实例（对象），而不需要重复任何代码。

```python
class Enemy:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.w = ENEMY_WIDTH
        self.h = ENEMY_HEIGHT
        self.dir = 1
        self.alive = True
        self.offset = random() * 60
        enemy_list.append(self)
```

```python
    def update(self):
        if (pyxel.frame_count + self.offset) % 60 < 30:
            self.x += ENEMY_SPEED
            self.dir = 1
        else:
            self.x -= ENEMY_SPEED
            self.dir = -1

        if self.y > pyxel.height - 1:
            self.alive = False

    def draw(self):
        pyxel.blit(self.x, self.y, 0, 0, 0, "enemy", self.dir, 0)
```

我们的玩家控制屏幕底部的火箭，射击外星人。

# 分数

这一系列类中的最后一个是字符：

```python
class Blast:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.radius = BLAST_START
        self.alive = True
        blast_list.append(self)

    def update(self):
        self.radius += 1

        if self.radius > BLAST_END:
            self.alive = False

    def draw(self):
        pyxel.circle(self.x, self.y, self.radius, BLAST_COLOR, IN)
        
        pyxel.circle(self.x, self.y, self.radius, BLAST_START, OUT)
```

设置所有元素后，我们可以编写应用程序以确保在场景切换时看到最新版本。代码是清晰的：

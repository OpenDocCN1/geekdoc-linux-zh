
```python
class Game(object):
    def __init__(self):
        pygame.init()
        pygame.font.init()
        self.clock = pygame.time.Clock()
        self.font = pygame.font.Font('data/Orbitracer.ttf', 50)
        self.screen = pygame.display.set_mode([RES])
        self.time = pygame.time.get_ticks()
        self.refresh_rate = 60
        self.level = 50
        self._player = pygame.sprite.Group()
        self.alien = pygame.sprite.Group()
        self.bullet = pygame.sprite.Group()
        self.missile = pygame.sprite.Group()
        self.barrier = pygame.sprite.Group()
        self.ship = pygame.sprite.Group()
        self.intro = pygame.image.load('data/start_screen.jpg').convert()
        self.background = pygame.image.load('data/start_background.jpg').convert()
        pygame.display.set_caption('Pivaders - ESC to exit!')
        self.alien = pygame.image.load('data/ship.png').convert_alpha()
        self.alien_color = pygame.COLOR(WHITE)
        self.ani_pos = 5
        self.ship_sheet = pygame.image.load('data/ship_sheet.png').convert_alpha()
        self.Player = pygame.sprite.Group()
        self.alien_pos = False, 0, 64
        self.animate = False
        self.explosion = False
        self.explosion = pygame.image.load('data/explosion.png').convert_alpha()
        self.explosion = self.explosion.subsurface(0, 0, 79, 96)
        self.alien_explosion = pygame.image.load('data/alien_explosion.png').convert_alpha()
        self.alien_explosion = self.alien_explosion.subsurface(0, 0, 94, 98)
        self.alien_explosion = False
        self.alien_pos = 0
        pygame.mixer.music.load('data/sound/10_Arpanauts.ogg')
        pygame.mixer.music.set_volume(.7)
        self.bullet_fx = pygame.mixer.Sound('data/sound/mediatix_pc-bitcrunched-lazer-beam.ogg')
        self.explosion_fx = pygame.mixer.Sound('data/sound/timgolly-0-bit-explosion.ogg')
        self.explosion_fx.set_volume(0.5)
        self.explode_alien = []
```

# 使用 Python 创建

## Pygameaders 第 2 部分：图形与声音

### 加载精灵图集

07 由于我们继承了 `Sprite` 类来创建 `Player` 类，我们可以通过更改 `pygame` 轻松地改变玩家的外。首先，我们需要使用 `pygame.image.load()` 加载精灵图集。由于我们是用透明背景制作的，可以在行末尾使用 `convert_alpha()` 以确保帧能够正确显示（无任何背景）。然后我们使用 `subsurface` 将 `PlayerImage` 设置为图集中间的精灵，其初始大小为 5。更改此值将改变绘制到屏幕上的图像：'0' 会让它完全向左倾斜；'1' 则向右。

```python
GameState.end_game = False
GameState.start_screen = True
GameState.vector = 0
GameState.shoot_bullet = False
```

```python
def control(self):
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            GameState.start_screen = False
            GameState.end_game = True
        if event.type == pygame.KEYDOWN \
            and event.key == pygame.ESCAPE:
                if GameState.start_screen:
                    GameState.end_game = True
                    self.kill_all()
        if GameState.start_screen:
            keys = pygame.key.get_pressed()
            if keys[pygame.K_LEFT]:
                GameState.vector = -1
                self.animate_left = True
                self.animate_right = False
            elif keys[pygame.K_RIGHT]:
                GameState.vector = 1
                self.animate_right = True
                self.animate_left = False
```

### 动画图

08 在 `Game` 类初始化代码列表稍靠后的位置，我们为玩家设置了两个标记：`animate_left` 和 `animate_right`。正如你在 `Game` 类的 `Control` 方法中看到的，当我们想要发生动画时，使用这些标记为 `True` 或 `False`。它还允许我们自动将精灵恢复到自然静止状态（否则飞船在停止后将继续像在向左飞行一样）。

```python
GameState.vector = 0
self.animate_right = False
self.animate_left = False
```

```python
if keys[pygame.K_SPACE]:
    if GameState.start_screen:
        GameState.start_screen = False
        self.lives = 2
        self.make_player()
        self.make_defenses(2)
        self.make_alien_wave()
```

```python
GameState.shoot_bullet = True
self.bullet_fx.play()
```

### 动画方法

09 我们在玩家代码中使用了标记：`animate_player()`。在这里我们使用嵌套语句来控制动画并物理地设置玩家图像。它规定，如果 `animate_right` 为 `True` 且当前位置不是我们想要的，我们就会增加 `ani_pos` 变量并设置玩家图像。`Else` 语句则将精灵动画回静止状态，相同的逻辑也适用于相反的方向。

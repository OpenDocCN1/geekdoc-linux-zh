
![](img/f16311c48f0c39ab87b1836be5339b9e_92_0.png)

# 使用 Python 创建

## PyInvaders 第 2 部分：图形与音

### 你需要...

- Raspbian
  `www.raspberry.org/downloads`
- Python
  `www.python.org/doc`
- Pygame
  `www.pygame.org/docs`
- 艺术资源
  `opengameart.org`

## PyInvaders 第 2 部分：图形与声音

这次，我们将扩展太空际入侵者克隆游戏，以包含沉浸式的动画和声音。

在上一份指南中，我们在创建基础版太空际入侵者克隆游戏 `PyInvaders` 时玩非常开心。得益于 `Sprite` 类，Pygame 分组、管理和检测碰撞的能力对我们的项目产生了巨大的影响，不仅体现在代码长度上，如果你错过了第一部分，可以通过 `git.io` 找到 `v0.1` 代码，而你可以找到 `v0.2` 版本，包含了所有的图像、音乐和音效。

为了让你的项目易于管理且直观，我们将一些动画方法集成到 `Game` 类中，并选择使用精灵（sprite）。这不仅让绘制屏幕变得容易，还能控制数量和关卡，这对于树莓派尤为重要。希望你喜欢使用这些技术制作动画和声音！

![](img/f16311c48f0c39ab87b1836be5339b9e_93_0.png)

### 安装依赖

### 下载 PyInvaders

你将从练习中获得更多并使用它创建自己的动画和声音。无论你只是想简单地运行代码还是想更好地理解基础游戏，两个要求都是安装了最新的 `Pygame`。版本控制帮助程序员保存更改。

```bash
git pull https://github.com/user/pyinvaders
```

在 `PyInvaders` 中有一个第二个文件夹。它包含了主游戏文件，你可以在这里运行应用程序。在 `data` 文件夹中，你会找到图形和声音，以及我们用于标题屏幕的字体。要进行测试，只需按方向键移动左右并按空格键射击。可以使用 `Escape` 键退出。这就是 `PyInvaders`。

![](img/f16311c48f0c39ab87b1836be5339b9e_93_1.png)

## 使用 Python 创建

### 动画 & 音（从第 87 行开始）

```python
class Game(object):
    def __init__(self):
        pygame.init()
        pygame.font.init()
        self.clock = pygame.time.Clock()
        self.game_font = pygame.font.Font(
            'data/orbitracer.ttf', 50)
        self.intro_font = pygame.font.Font(
            'data/orbitracer.ttf', 72)
        self.screen = pygame.display.set_mode([RES])
        self.refresh_rate = pygame.time.get_ticks()
        self.rounds_won = 0
        self.level = 50
        self.score = 0
        self.lives = []
        self.player_group = pygame.sprite.Group()
        self.alien_group = pygame.sprite.Group()
        self.bullet_group = pygame.sprite.Group()
        self.missile_group = pygame.sprite.Group()
        self.barrier_group = pygame.sprite.Group()
        self.sprite_list = pygame.sprite.Group()
        self.intro_screen = pygame.image.load(
            'data/graphics/start_screen.jpg').convert()
        self.background = pygame.image.load(
            'data/graphics/Space_background.jpg').convert()
        pygame.display.set_caption('PyInvaders - ESC to exit')
        self.alien = pygame.image.load(
            'data/graphics/ships.png').convert_alpha()
        self.alien_col = COLORKEY(WHITE)
        self.ani_pos = [5, 50]
        self.ship_sheet = pygame.image.load(
            'data/graphics/ship_final.png').convert_alpha()
        self.Player = Player(self, self.ship_sheet, self.surface,
            0, 79, 64)
        self.animate_rate = False
        self.animate = False
        self.explosion = pygame.image.load(
            'data/graphics/explosion.png').convert_alpha()
        self.explosion = self.explosion.subsurface(
            0, 0, 79, 98)
        self.alien_explosion = pygame.image.load(
            'data/graphics/explosion.png').convert_alpha()
        self.alien_explosion = self.alien_explosion.subsurface(
            0, 0, 94, 98)
        self.alien_explosion = False
        self.alien_pos = [0, 0]
        pygame.mixer.music.load('data/sound/10_Arpeggauts.ogg')
        pygame.mixer.music.set_volume(0.7)
        self.bullet_fx = pygame.mixer.Sound(0.5)
        self.explosion_list = []
```

04 与上个月教程中的游戏相比，你会发现它现在更加动态。当你改变方向并旋转时，飞船现在会向弯倾斜。当你击中外星飞船时，它会发生几帧动画爆炸，你的飞船也应该产生较小的爆炸。激光和爆炸音效也会在动画发生时出现。

### 寻找用于动画的图像

05 在编写任何代码之前，是时候设置组来使用精灵了；这些精灵可以加载一次，也可以用 Pygame 创建。我们需要几个代表每一帧的单独尺寸和间距的图像“帧”。我们在 `opengart.com` 找到了我们的素材。

### 调整资源

06 虽然在网上找到的资源可以直接使用，但你可能想将其导入到 GIMP 等图像编辑软件中以根据你的需求进行配置。我们从一张帧宽度和高度的表开始，然后复制了它的另一侧。最终我们在一个文档中得到了 11 帧相同尺寸和宽度的图像。像素级的尺寸和宽度是关键，因此我们可以将其乘以下一帧。

## 使用 Python 创建

## Pivaders 第 2 部分：图形与声音

### 加载精灵集

由于我们继承了 `Sprite` 类来创建 `Player` 类，我们可以通过更改 pygame 轻松地改变玩家的外。首先，我们需要使用 `pygame.image.load()` 加载精灵集。由于我们是透明背景制作的，因此我们在行末尾添加了 `convert_alpha()` 以确保精灵帧正确显示（没有任何背景）。然后，我们使用 `subsurface` 将初始 `Player` 图像设置为图集的中间。我们定义了 `pos`，其初始值为 5。更改此值将改变绘制的图像：'0' 会使其向左倾斜；'11' 则完全完全在右侧。

```python
GameState.end_game = False
```

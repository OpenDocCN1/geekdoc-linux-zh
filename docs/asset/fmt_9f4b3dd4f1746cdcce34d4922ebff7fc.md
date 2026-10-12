
```python
class Game:
    def __init__(self):
        pygame.init()
        self.font = pygame.font.SysFont('arial', 24)
        self.time = pygame.time.get_ticks()
        self.data = pygame.image.load('background.png')
        self.screen = pygame.display.set_mode((600, 400))
        self.time = pygame.time.get_ticks()
        self.score = 0
        self.level = 1
        self.levelup = 5
        self.all = pygame.sprite.Group()
        self.enemies = pygame.sprite.Group()
        self.alien_group = pygame.sprite.Group()
        self.bullet_group = pygame.sprite.Group()
        self.missile_group = pygame.sprite.Group()
        self.all_sprite = pygame.sprite.Group()
        self.intro_screen = pygame.image.load('intro.png')
        self.background = pygame.image.load('gameover.png')
        pygame.display.set_caption('Invaders to exit')
        self.player = player()
        self.all.add(self.player)
        self.score = True
        self.game_over = False
        self.shot_bullet = True

    def update(self):
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                self.game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_SPACE:
                    self.game_over = False
                if event.key == pygame.K_n:
                    self.level += 1
                    self.score = False
            if self.score == False:
                self.shot_bullet = False
            if self.game_over == True:
                self.shot_bullet = True
            if self.game_over == False:
                self.score = True
        self.all.update()
        self.enemies.update()
        self.alien_group.update()
        self.bullet_group.update()
        self.missile_group.update()
```

# 整洁的代码

清晰标记经常使用的全局变量使代码更易读，当我们想要更改对象大小时，只需要在这里操作，并在处处生效。

# 组

创建组的长列表使得我们每次创建一个对象时都可以轻松地进行测试和绘制。

# 控制

处理键盘输入是一个重要的方法。它检查我们是否在屏幕上进行游戏。

# 雨中的子弹

`Ammo` 类用于分发一些属性和对象，此方法检查是否有必要。

![](img/5ff17f0221cc9f68eff9bca50f6afb_66_0.png)

![](img/5ff17f0221cc9f68eff9bca50f6afb_66_1.png)

![](img/5ff17f0221cc9f68eff9bca50f6afb_66_2.png)

![](img/5ff17f0221cc9f68eff9bca50f6afb_66_3.png)

# 教程

入侵者：太空入侵者克隆

## 03 测试

安装好 `Pygame` 并项目克隆到你的机器上（你也可以在这个网站找到 zip 包——只需解压并复制到你的文件夹），你可以进行快速驱动以确保一切都就绪。现在你可以从终端运行程序，使用空格键开始游戏，使用方向键左右移动。对于那些设计为改变任何内容的常量，你可以有一个宠物类。从该类中你可以创建猫（喵喵）和狗（汪汪）。它们在许多方面是不同的，但都拥有相同的父类。我们对 `Ammo` 类正是这样做，用它来创建子弹和敌人。它们移动的方向相反，但从根本上是一样的。

## 04 创建你自己的类

一旦你达到了高分（生存结束），就是时候实现你自己的版本了。你将通过遵循示例和弄懂内容中学到很多。对于想制作自己项目的人，创建一个新文件夹并使用任何 `IDE`（`IDLE` 等）来创建并保存你的 `.py` 文件。

## 05 类 - 部分 1

类是你想要创建的对象的蓝图。在我们玩的游戏中，屏幕中间有许多类的实例，或者说多个副本（在 `make_player` 方法中）。玩家继承了 `Sprite` 类的许多属性，以及在你创建的类的第一行中找到的新方法。你可以在 `www.pygame.org/wiki/Sprite` 阅读更多关于 `Sprite` 类的信息。

## 07 类 - 部分 2

在入侵者游戏中，类创建的属性是类使用的简单变量。对于每个弹（或子弹），你还会注意到所有类都有一个 `update()` 方法，该方法在我们创建的移动循环的每次迭代中被调用（调用 `update`）。在子弹的情况下，它移动到屏幕顶部或底部，我们销毁它（如果它没有左移）。

## 08 全局变量

一旦确定了需要的变量，我们将它们存储在大写字母中。这些变量是常量（或全局变量）。它们是需要使用但在代码中引用的数字、颜色、尺寸和分辨率。你还需要不同类的多个数字——

## 09 游戏

我们的最后一个类是游戏所有主要功能发生的地方，但记住，它只是一个方法列表——在调用它们之前，什么都不会发生。主类是游戏所在地。我们使用 `Pygame` 编写射物，并使用 `gameState` 类控制诸如玩家移动（方向）以及我们是否需要重启屏幕。

## 10 主循环

类中有许多方法（函数），每个都设计用于控制游戏设置的特定方面。游戏每轮发生的实际逻辑包含在类末尾的 `main_loop` 方法中。从那里，你将能够看到在结束游戏前每秒更新 20 次的各种变量和函数。

## 编写太空入侵者游戏 (Space Invaders)

类本质上是你打算创建的对象的蓝图

```python
pygame.display.flip()
self.control()
def __init__(self):
    self.player = Player()
    self.player_group.add(self.player)
    self.sprite_list.add(self.player)
    self.all_sprites.add(self.player)
    self.refresh_sprites()
    pygame.screen.blit(self.image, (0, 0))
    self.clock.tick(self.frame_rate)
```

### 刷新

你应该考虑帧之间更新状态的方式，背景移动对于动画至关重要。

### 死亡还是胜利

这里回答了两个关键的问题——玩家死了，还是你赢得了这一回合？

```python
def draw(self):
    if self.alive():
        self.screen.blit(self.game_font.render(
            "The war was lost!", True, (255, 0, 0))
        ), (250, 250))
        self.screen.blit(self.game_font.render(
            "YOU WON!", True, (0, 255, 0))
        ), (250, 300))
```

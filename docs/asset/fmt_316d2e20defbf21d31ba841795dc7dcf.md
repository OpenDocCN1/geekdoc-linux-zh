
```python
self.lives -= 1

def next_round(self):

    for actor in [self.missile_group,

                  self.barrier_group, self.bullet_group]:

        i.kill()

    self.alien_wave(self.level_up)

    self.make_defenses()

    self.level_up += 50

def main_loop(self):

    while not GameState.end_game:

        while not GameState.start_screen:

            GameState.game_time = pygame.time.get_ticks()

            GameState.alien_time = pygame.time.get_ticks()

            self.control()

            self.make_missile()

            for actor in [self.player_group, self.bullet_group,

                          self.alien_group, self.missile_group]:

                for i in actor:

                    i.update()

            if GameState.shoot_bullet:

                self.make_bullet()

            self.calc_collisions()

            if self.is_dead() or self.defenses_breached():

                GameState.start_screen = True

            if self.win_round():

                self.next_round()

            self.refresh_screen()

        self.splash_screen()

    pygame.quit()
```

### 生死存亡
可能最重要的两个问题在这里得到了解答——玩家是否死亡或你是否赢得了这一轮？

获取代码：`bit.ly/11k9f2x`

### 主循环
这是我们应用程序的核心部分。此循环每秒执行 20 次。它需要逻辑清晰且易于其他编码者理解。

### 开始游戏
我们最后做的就是创建一个 `Game` 对象并调用主循环。除了我们的常量之外，这是唯一位于类外部的代码。

```python
if __name__ == '__main__':
    pv = Game()
    pv.main_loop()
```

![](img/3b256f430f51c98f1315671f6e4eec19_123_0.png)

## 第二部分：为Pivaders添加动画和声音

在用仅300行Python代码编写了一个太空入侵者克隆之后，现在我们将其扩展为包含动画和声音。

### 资源

- Raspbian：`www.raspberrypi.org/downloads`
- Python：`www.python.org/doc`
- Pygame：`www.pygame.org/docs`
- 美术资源：`opengameart.org`

在上一个教程中，我们非常愉快地创建了基础太空入侵者克隆——Pivaders。这个项目的一个关键挑战是让代码量保持在可控范围内——仅300行Python。如果没有利用Pygame强大的功能集，这个目标很可能至少会被超出两倍。

得益于`Sprite`类，Pygame能够对精灵进行分组、管理和碰撞检测，这给我们的项目带来了很大不同，不仅在代码长度上，也在简洁性上。如果你错过了项目的第一部分，可以通过 `git.io/cBVTBg` 在GitHub上找到v0.1代码清单；而包含我们使用的所有图像、音乐和音效的v0.2版本，可以在 `git.io/80Sk-w` 找到。即使在Pygame提供的清晰框架内工作，添加动画和声音的方式仍然有成百上千种。我们本可以创建十多个类来创建和管理单个图像的容器，或者读取一个精灵表（一张包含许多较小独立图像的大图），然后将其绘制（或blit）到屏幕上。为了简洁和性能，我们将一些动画方法集成到了`Game`类中，并选择使用精灵表。这不仅使绘制到屏幕变得非常容易，还能控制资源数量并保持高性能，这对树莓派来说尤为重要。

#### 01 设置依赖

正如我们在上一个教程中建议的那样，如果你下载代码（`git.io/80Sk-w`），并在为你的Pygame项目创建自己的动画和声音时作为参考，你会从练习中获益更多。无论你只是想简单地预览和游玩，还是想通读代码以更好地理解基本游戏创建，你仍然需要满足一些基本依赖。这里两个关键需求是Pygame和Git，它们在最新版的Raspbian系统中默认都已安装。不过，如果你不确定是否已安装，请在命令行中输入以下命令：

```
sudo apt-get install python-pygame git
```

## Pivaders.py 代码清单（从第86行开始，续下页）

```python
class Game(Object):

    def __init__(self):

        pygame.init()

        pygame.font.init()

        self.clock = pygame.time.Clock()

        self.game_font = pygame.font.Font('data/Orbitron.ttf', 28)

        self.intro_font = pygame.font.Font('data/Orbitron.ttf', 72)

        self.screen = pygame.display.set_mode(RES, RES[])

        self.time = pygame.time.get_ticks()

        self.refresh_rate = 50; self.rounds_won = 0

        self.level_up = 50% self.score ) convert

        self.lives = 2

        self.player_group = pygame.sprite.Group()

        self.alien_group = pygame.sprite.Group()

        self.bullet_group = pygame.sprite.Group()

        self.missile_group = pygame.sprite.Group()

        self.barrier_group = pygame.sprite.Group()

        self.all_sprite_list = pygame.sprite.Group()

        self.intro_screen = pygame.image.load('data/intro.jpg').convert()

        self.background = pygame.image.load('data/graphics/Space-Background.jpg').convert()

        pygame.display.set_caption('Pivaders - ESC to exit')

        self.game_mode = 'start'

        Alien.image = pygame.image.load('data/graphics/SpaceShip16.png').convert()

        Alien.image.set_colorkey(WHITE)

        self.ani_pos

        self.ship_sheet = pygame.image.load('data/graphics/ship_sheet_final.png').convert_alpha()

        Player.image = self.ship_sheet.subsurface(self.ani_pos[0, 0, 64, 64])

        self.ani_right = False

        self.animate_left = False

        self.explosion_sheet = pygame.image.load('data/graphics/explosion_new1.png').convert_alpha()
```

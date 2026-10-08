
# 使用 Python 创建

![](img/e016e192a91ffc1a9e474690a590742f_115_0.png)

# 第二部分：为 Pivaders 添加动画和音效

在仅用 300 行 Python 代码编写了一个太空侵略者（Space Invaders）克隆版之后，现在我们要扩展它，加入动画和音效。

# 资源

- **Raspbian：** www.raspberrypi.org/downloads
- **Python：** www.python.org/doc
- **Pygame：** www.pygame.org/docs
- **美术资产：** opengameart.org

我们非常享受创建基础太空侵略者克隆版 Pivaders 的过程，这承接了上一篇教程。该项目的一个关键挑战在于保持代码规模的可管理性——仅 300 行 Python 代码。如果没有借助 Pygame 强大的功能集，这一目标很可能至少会超出两倍。Pygame 中 Sprite 类在分组、管理和碰撞检测方面的能力，不仅缩短了代码长度，还极大地简化了项目结构，对我们来说意义重大。如果你错过了项目的第一部分，可以通过 git.io/cBVtBG 在 GitHub 上找到 v0.1 的代码列表，而包含我们使用的所有图像、音乐和音效的 v0.2 版本则位于 git.io/BQsk-w。

即便在 Pygame 提供的明确框架内工作，我们仍有成千上万种方法来添加动画和音效。我们可以创建数十个类中的任意一个来创建和管理单个图像的容器，或者读取精灵表（sprite sheet，即包含许多较小独立图像的单张大图），然后将其绘制（或 blit）到屏幕上。

为了保持简洁和性能，我们将几种动画方法整合到了 Game 类中，并选择使用精灵表。这不仅使绘制到屏幕上变得容易，还能控制资产数量，保持较高的性能水平，这对于树莓派（Raspberry Pi）来说非常重要。

## 01 设置依赖项

正如我们在上一个教程中建议的那样，如果你下载我们在网上提供的代码（git.io/BQsk-w）并将其作为参考，同时为你自己的各种 Pygame 项目下载动画和音效，你会从练习中获得更多收获。无论你只是想要简单地预览和游玩，还是希望逐步阅读代码以更好地理解基础游戏创建，你仍然需要满足一些基本依赖项。这里有两个关键需求：Pygame 和 Git，它们在最新的 Raspbian 安装中都是默认安装的。如果你不确定是否已安装它们，请在命令行中输入以下内容：

```bash
sudo apt-get install python-pygame
git
```

从第 86 行开始（续至下一页）

# Pivaders.py 代码列表

```python
class Game(object):

    def __init__(self):
        pygame.init()
        pygame.font.init()
        self.clock = pygame.time.Clock()
        self.game_font = pygame.font.Font('data/Orbiters.ttf', 29)
        self.intro_font = pygame.font.Font('data/Orbiters.ttf', 72)

        self.screen = pygame.display.set_mode(RES[1])
        self.time = pygame.time.get_ticks()
        self.refresh_rate = 26; self.round_mode = 0
        self.level_up = 50; self.score = 0
        self.lives = 2

        self.player_image = pygame.image.load('data/graphics/ship.png').convert()
        self.alien_group = pygame.sprite.Group()
        self.bullet_group = pygame.sprite.Group()
        self.missile_group = pygame.sprite.Group()
        self.barrier_group = pygame.sprite.Group()

        self.all_sprite_list = pygame.sprite.Group()
        self.missile_screen = pygame.image.load('data/graphics/start_screen.jpg'), convert()
        self.background = pygame.image.load('data/graphics/Space-Background.jpg').convert()

        pygame.display.set_caption('Pivaders  -  ESC to exit!')
        pygame.mouse.set_visible(0)

        Alien_image = pygame.image.load('data/graphics/Snapchip2.png').convert()
        Alien_image.set_colorkey(WHITE)

        self.ship_sheet = pygame.image.load('data/graphics/ship_sheet_final.png').convert_alpha()
        Player_image = self.ship_sheet.subsurface((0, 64, 64))

        self.animate_right = False
        self.animate_left = False
        self.explosion_sheet = pygame.image.load('data/explosion/explosion_new1.png').convert_alpha()
        self.explosion_image = self.explosion_sheet.subsurface(0, 0, 96, 96)

        self.alien_explosion = pygame.image.load('data/graphics/alien_explosion.png')
        self.alien_explose_graphics = self.alien_explosion_sheet.subsurface(0, 0, 96, 96)

        self.explose = False
        self.explose_pos = 0; self.alien_explose = False
        self.alien_explose_pos = 0
        pygame.mixer.music.load('data/sound/10_Arpantns.ogg')
        pygame.mixer.music.play(-1)
        pygame.mixer.music.set_volume(0.0)

        self.bullet_fx = pygame.mixer.Sound('data/sound/Medium-3-10_introclear-lean.ogg')
        self.explosion_fx = pygame.mixer.Sound('data/sound/timbrany_3.bit-explosion.ogg')
        self.explosion_fx.set_volume(0.6)

        self.explodey_alien = []
        GameState.end_game = False
        GameState.start_screen = True
        GameState.vec = 0
        GameState.shoot_bullet = False

    def control(self):
        for event in pygame.event.get():
            if event.type == pygame.QUIT():
                GameState.start_screen = False
                GameState.end_game = True

            if event.type == pygame.KEYDOWN \
and event.key == pygame.K.ESCAPE:
                if Game.start_screen:
                    GameState.start_screen = False
                    GameState.end_game = True
                    self.kill_all()
                else:
                    GameState.start_screen = True

        self.keys = pygame.key.get_pressed()
        if self.keys[pygame.K.LEFT]:
            GameState.vector -= 1
            self.animate_left = True
            self.animate_right = False
        elif self.keys[pygame.K.RIGHT]:
            GameState.vector += 1
            self.animate_right = True
            self.animate_left = False
        else:
            GameState.vector = 0
            self.animate_right = False
            self.animate_left = False

        if self.keys[pygame.K.SPACE]:
            if GameState.start_screen:
                GameState.start_screen = False
                self.lives = 2
                self.score = 0
                self.make_player()
                self.make_defense()
                self.bullet_fx.play()
            else:
                GameState.shoot_bullet = True
                self.bullet_fx.play()

    def animate_player(self):
        if self.animate_right:
            if self.an_pos <= 10:
                self.anim_image = self.ship_sheet.subsurface(
                    (self.an_pos*16, 0, 64, 64))
                self.an_pos += 1
            else:
                if self.an_pos > 37:
                    self.an_pos = 1
                    self.anim_image = self.ship_sheet.subsurface(
                        (self.an_pos*16, 0, 64, 64))
        if self.animate_left:
            if self.an_pos >= 14:
                self.an_pos = 1
                self.anim_image = self.ship_sheet.subsurface(
                    (self.an_pos*16, 0, 64, 64))
            else:
                if self.an_pos <= 5:
                    self.an_pos = 37
                    self.anim_image = self.ship_sheet.subsurface(
                        (self.an_pos*16, 0, 64, 64))

    def player_explosion(self):
        if self.explose:
            if self.explose_pos < 8:
                self.explosion_image = self.explosion_sheet.subsurface(
                    (self.explose_pos*16, 79, 96, 96))
                self.player_pos -= 1
                self.screen.blit(self.explosion_image, self.player.rect, -10, self.player.rect, y - 30)
            else:
                self.explose = False
                self.explose_pos = 0

    def alien_explose(self):
        if self.alien_explose:
            if self.alien_explose_pos < 9:
                self.alien_explode_graphics = self.alien_explosion_sheet.subsurface(
                    (self.alien_explose_pos*16, 54, self.alien_explose_pos*16+8, 54))
                self.screen.blit(self.alien_explose_graphics, self.explodey_alien[0](self.alien_explose_pos - 1), 0, self.explodey_alien[1] - 80)
            else:
                self.alien_explose = False
                self.alien_explose_pos = 0
                self.explodey_alien = []

    def splash_screen(self):
        while GameState.start_screen:
            self.screen.blit(self.intro_screen, [0, 0])
            self.screen.blit(self.intro_font.render('Pivaders', 1, WHITE), (250, 120))
            self.screen.blit(self.intro_font.render('PRESS SPACE TO PLAY', 1, WHITE), (274, 192))
            self.display.flip()
            pygame.time.wait(15)
            self.clock.tick(self.refresh_rate / 2)

    def make_player(self):
        self.player = Player()
```

Ship_sheet（精灵表）

通过使用 'ani_pos' 变量，我们将玩家图像设置为精灵表的一小段。改变该变量的值即可改变显示的图像。

fx.play()

我们已经在按下空格键时加载了所需的音效。现在我们只需要在按下空格键时调用它即可。

设置标志

我们在 control 方法中添加了 'animate_left' 和 'animate_right' 布尔标志。当它们为真时，实际的动画代码会通过一个独立的方法被调用。
